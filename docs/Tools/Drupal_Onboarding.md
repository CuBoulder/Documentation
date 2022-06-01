# Drupal Onboarding

## Introduction

### What is Drupal?

[Drupal](https://www.drupal.org/about) is a content management system (CMS) similar to Wordpress, Wix, Squarespace, etc. This software allows users to organize and create content on a site without any coding experience. What sets Drupal apart from the others is the ability to customize the CMS and add complex features.

### How is Drupal used at CU?

Our sites use Drupal to allow users to create their own websites. We create new features for Drupal so our users can have the tools they need to create the content for their sites. For example, https://colorado.edu is built using Drupal.

---

## Setting up a Local Enviroment for Drupal

### Installing Composer

We use [Composer](https://getcomposer.org/) php package manager to install Drupal and all of its dependencies. Package managers make installing and updating software packages easier and more organized. Examples include npm for Node, pip for Python, and brew for MacOS.

Run `which composer` to check if composer is installed. If it's not installed, [install composer](https://getcomposer.org/download/)

### Intalling Lando & Docker

Lando is a local environment tool that runs on Docker to create a container for a website. Open terminal and type `which lando`. If a path is printed, then you already have lando installed and can go to the next step. Otherwise, follow the steps to [install Docker](https://docs.docker.com/desktop/mac/install/) and then [install Lando](https://docs.lando.dev/basics/installation.html#macos). Both of these are needed to launch your own nextpress project template!

### Drush

[Drush](https://www.drush.org/latest/) is a command line utility for interacting with a Drupal site. It’s extremely useful and learning the commands will make development much faster. Since the dev site is using Lando, we must prefix all drush commands with lando, as you will see in some commands in the nextpress section.

---

## Site Development

### Contributing Code - Nextpress

We use our [nextpress project template](https://github.com/CuBoulder/nextpress-project-template) to quickly get a development version of nextpress (Drupal running off a Lando container in Docker) running. DO NOT use this branch in production! The production composer.\* files can be found on the production branch.

### Nextpress Installation

```
composer -V             # verify that your machine has composer 2.x installed

git clone https://github.com/CuBoulder/nextpress-project-template <project-name>

cd <project-name>

open .lando.yml file and replace the name value on line 1 with your project name.
This is what docker will use to build your container, so be sure to make the project name unique from other containers.

lando start             # this command will take a while if it's the first it's being run
lando install-site      # this installs Drupal

```

Other useful commands:

```
lando info   ##Prints info about your app including urls to visit your page, database info and more

lando drush pmu simplesamlphp_auth 	 ## allows local logins and disables SSO

```

Enable Debugging with Twig, allowing you to see what Twig templates need to be created for your new page

```
cd sites/default && sudo cp default.services.yml services.yml   ## creates a services.yml file

sudo chown <USERNAME> services.yml     ## May be needed to change read/write access of your new services.yml file
```

In your newly created services.yml file, change debug to `debug:true` and save. This will allow you to Inspect the webpage with your Browser Dev Tools to begin planning your templates.

Run `lando info` to see where your new site is hosted! See the above useful commands for allowing local logins, twig debugging, then sign in with the default credentials and you're all ready to get building!

### Site Building

The Admin Interface is where users can make changes to their site. You can do everything from installing modules, creating content, and configuring themes and more.You can access the admin pages by using the Admin Toolbar on the left side of the site.

So far, there is no content on the site. Start by adding a page by clicking on the `Add Content > Basic Page Button`.
Fill out the fields and click save.

Content for Drupal is separated into Content Types. On this installation, the types are Article, Basic Page, and Person. Content Types organize the types of information that could live on a site.

Now we are going to configure some of the site settings. Using the admin toolbar, go to `Configuration > System > Basic Site Settings`.

In the Slogan Form input, type `Strategic Relations and Communications`. Below that, in the Default Front Page input, type `/node/1` as the path to be used for the front page. Click the `Save Configuration` button. Going back to the site, you can see the added tagline and frontpage!

### Installing A Module

Modules extend the functionality of the site. Installing a module is done in two parts, adding the composer package, and enabling it on the site itself. We are going to install the Conditional Fields module. You can find more modules on the [Drupal Website](https://www.drupal.org/project/project_module). In the project root, run the following:

```
composer require ‘drupal/conditional_fields:^4.0@alpha’
```

After the composer.\* files have been updated, go back to the site and go to `Extend > Overview` using the Admin Toolbar. Find the Conditional Fields module in the list and check the box. Click Install at the bottom of the page. You will get a success status message if the module was installed.

### Installing a Module from GitHub

Contributed modules come from [Packagist](https://packagist.org/), the main composer repository. However, CU has modules that live on Github. To add a module from Github, you have to add the repository and the package manually. In composer.json, there is a list of Github repositories in the repositories section. In the require section, the syntax is the package name with the version of dev-main.

### Theme Development

[Themes](https://www.drupal.org/docs/theming-drupal) give a site its look. The theme installed by default is the CU Boulder site theme. In the `/themes` directory of your `nextpress project` you will both contributed and our custom CU Boulder theme which includes CSS, JS, Twig Templates, external libraries like BootStrap and FontAwesome and more! Here is where you will build out Twig templates, build CSS and JS files for your pages, and link those newly created files to our `ucb2021_base.libraries.yml`

### Module Development

[Modules](https://www.drupal.org/docs/creating-modules) extend the functionality of the site by adding custom PHP code. For example, the very popular Webform Module allows users to create and track forms. Modules follow a strict OOP paradigm and often will extend existing Plugins and Controllers. They may contain configuration in the form of .yml files that can add various features such as menu links, routes, and permissions. They may also implement hooks, which are functions that can alter or extend the existing behavior of the site.

Much of module development is looking at existing module source code and using them as an example for creating your own.

---

## Site Development

### Nested Repositories within NextPress

Starting the app for the first time will install all the composer dependencies and clone down all of the CU Boulder modules. Even though the modules are composer packages, they are cloned with git so we can do development work on them. These modules include `ucb2021_base`, `ucb2021_profiles`, `ucb_custom_paragraphs`, `ucb_custom_page_types`, and `ucb_shortcodes`.

### Branching with Nextpress

In order to test a PR or to develop for a new issue/feature/bug, you will need to switch to the appropriate branches on each repository. Depending on the ticket assigned for review or developement, your work may touch one or more of these repos.

The repos you may need to check are:

- `themes/custom/ucb_base`
- `modules/custom/ucb_custom_page_types`
- `modules/custom/ucb_custom_paragraphs`
- `modules/custom/ucb_shortcodes`
- `profiles/custom/ucb2021_profile`

Make sure your repos are up to date before creating a branch with `git fetch -a` and then checkout the available branches with `git branch -a` in the above repo locations within the nextpress project to confirm your local project is up to date with the remote repo with the most current available remote branches. Run a `git status` to make sure you are up to date, `git pull` any changes if not.

To checkout to a branch for code review, run the following on each repo that may have new code, which includes the 5 above repos:

```
git checkout -b <LOCALBRANCHNAME> origin/<REMOTEBRANCHNAME>
```

### Pushing Code

Once you have something ready for commit, or you have code that is tested, working, and ready for a pull request-- the code push process works as you would expect. In each of the repos that resides in our nextpress project, we will need to push that new code to its respective remote repository. Do not push to nextpress remote repo, just the afformentioned custom repositories that reside within your nextpress project.

`cd` into any repository that you have been working in. You can run `git status` in each custom repo to see what files were modified. `git add <filename>` any files you have changed that are included in the ticket, and `git push` to the respective branch in that remote repository.

---

## Setting up your IDE for Drupal

The following sections are a list of Drupal community reccommended IDE extensions that may help with your Drupal development. They are not required to install, but may make some aspects of development easier for you.

### VS Code

The following is a list of recommended official and contributed extensions that will allow you to configure Visual Studio Code for Drupal PHP and JavaScript development. A community-curated list of extensions can be found at viatsko/awesome-vscode.

- [phpcs](https://marketplace.visualstudio.com/items?itemName=ikappas.phpcs): provides integration for PHP CodeSniffer (phpcs) code linting.
- [phpcbf](https://github.com/soderlind/vscode-phpcbf): This extension provides the PHP Code Beautifier and Fixer (phpcbf) command for Visual Studio Code.
- [PHP DocBlocker](https://marketplace.visualstudio.com/items?itemName=neilbrayfield.php-docblocker): provides auto-complete for PHP docblocks.
- [Empty Indent](https://marketplace.visualstudio.com/items?itemName=DmitryDorofeev.empty-indent): removes indent of empty lines on save.
- [PHP Debug](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug): provides launch configuration support for XDebug. Requires XDebug.

#### Intellisense Extensions

The intellisense extension you may want to use may vary based on your license requirements and Drupal web site. See below.

- [PHP Intelephense](https://marketplace.visualstudio.com/items?itemName=bmewburn.vscode-intelephense-client): provides support for PHP code completion and intellisense that supports any PHP file extension (module, inc, etc...).
- [PHP Intellisense](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-intellisense): provides support for PHP code completion and intellisense, but only for files using the PHP extension.

#### Twig Extensions

The following extensions are especially helpful for Twig template development.

- [Twig Language](https://marketplace.visualstudio.com/items?itemName=mblode.twig-language): Syntax highlighting, Snippets, Emmet, Pretty Diff Formatting, Hover,HTML intellisense
- [Twig Language 2](https://marketplace.visualstudio.com/items?itemName=mblode.twig-language-2): All of the features of Twig Language 1 but without HTML Intellisense

---

### PHPStorm

[PHPstorm](http://www.jetbrains.com/phpstorm/) is an innovative, Java-based integrated development environment (IDE) engineered by JetBrains for PHP and web developers.

A full walkthrough of configuring PHPStorm is located [here](https://www.drupal.org/docs/develop/development-tools/configuring-phpstorm)
