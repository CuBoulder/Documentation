# Drupal Onboarding

## Introduction

### What is Drupal?

[Drupal](https://www.drupal.org/about) is a content management framework which allows developers to create a custom web Content Management System (CMS).  

### Web Express
Web Express is the main web CMS solution created, developed and maintained by the SRC Development and Operations team to allow for the creation of web sites and content on the primary CU Boulder domain (https://www.colorado.edu).  Web Express is built on top of the Drupal framework and utilizes code developed by the core Drupal team, other open-source contributors as well as many custom modules developed by the CU Boulder team.    

The goal of Web Express is to faciliate the creation of content that can be published in a secure, branded and accessible manner for anyone who has a buisiness need to publish content on https://www.colorado.edu.

---

## Setting up a Local Enviroment for Drupal

### Installing Composer

We use [Composer](https://getcomposer.org/) php package manager to install Drupal and all of its dependencies. Package managers make installing and updating software packages easier and more organized. Examples include npm for Node, pip for Python, and brew for MacOS.

Run `which composer` to check if composer is installed. If it's not installed, [install composer](https://getcomposer.org/download/)

### Installing DDEV & OrbStack

For local Drupal development, we use **DDEV** with **OrbStack**.

[OrbStack](https://orbstack.dev/) provides the container runtime, while [DDEV](https://ddev.com/) manages the local Drupal environment, including PHP, the database, web server, and project URLs.

To check whether DDEV is installed, run:

```bash
which ddev
```

If nothing is returned, install [OrbStack](https://orbstack.dev/) first, then [DDEV](https://ddev.readthedocs.io/en/stable/users/install/ddev-installation/).

Useful commands:

```bash
ddev start
ddev describe
ddev stop
```

`ddev describe` shows the project's local URLs, services, ports, and environment details.

### Drush

[Drush](https://www.drush.org/latest/) is a command line utility for interacting with a Drupal site. It’s extremely useful and learning the commands will make development much faster. Since the dev site is using Lando, we must prefix all drush commands with lando, as you will see in some commands in the Sandpoint section.

```bash
ddev drush cr
ddev drush cim
ddev drush updb
```
---

## Site Development

### Contributing Code - Sandpoint (boulder_base)

We use our [D11 Sandpoint project template](https://github.com/CuBoulder/sandpoint-d11-project-template) to quickly get a development version of Web Express (Drupal running off a DDEV container in OrbStack) running. DO NOT use this branch in production! The production composer.\* files can be found on the production branch.

### Sandpoint Installation

```bash
composer -V             # verify that your machine has composer 2.x installed

git clone https://github.com/CuBoulder/sandpoint-d11-project-template <project-name>

cd <project-name>

ddev start             # initializes your container

ddev composer install # pulls in our theme, profile, and contrib/custom modules
ddev install-site      # runs a script that installs Drupal to your container

```

Other useful commands:

```bash
ddev launch   ## Opens your site in a browser

ddev describe ## Displays the current DDEV project's configuration and status, including URLs, services, ports, and environment details.

```

Enable Debugging with Twig via CLI, allowing you to see what Twig templates need to be created for your new page. You may also configure debug mode via Drupal UI. It is found under Configuration -> Development -> Development Settings -> Twig Development Mode

```bash
cd sites/default && sudo cp default.services.yml services.yml   ## creates a services.yml file

sudo chown <USERNAME> services.yml     ## May be needed to change read/write access of your new services.yml file
```

In your newly created services.yml file, change debug to `debug:true` and save. This will allow you to Inspect the webpage with your Browser Dev Tools to begin planning your templates.

Run `ddev describe` to see where your new site is hosted, or open automatically with `ddev launch` See the above useful commands for allowing local logins, twig debugging, then sign in with the default credentials and you're all ready to get building!

### Site Building

The Admin Interface is where users can make changes to their site. You can do everything from installing modules, creating content, and configuring themes and more.You can access the admin pages by using the Admin Toolbar on the left side of the site.

So far, there is no content on the site. Start by adding a page by clicking on the `Add Content > Basic Page Button`.
Fill out the fields and click save.

Content for Drupal is separated into Content Types. On this installation, the types are Article, Basic Page, and Person. Content Types organize the types of information that could live on a site.

Now we are going to configure some of the site settings. Using the admin toolbar, go to `Configuration > System > Basic Site Settings`.

In the Slogan Form input, type `Strategic Relations and Communications`. Below that, in the Default Front Page input, type `/node/1` as the path to be used for the front page. Click the `Save Configuration` button. Going back to the site, you can see the added tagline and frontpage!

### Installing A Module

Modules extend the functionality of the site. Installing a module is done in two parts, adding the composer package, and enabling it on the site itself. We are going to install the Conditional Fields module. You can find more modules on the [Drupal Website](https://www.drupal.org/project/project_module). In the project root, run the following:

```bash
composer require ‘drupal/conditional_fields:^4.0@alpha’
```

After the composer.\* files have been updated, go back to the site and go to `Extend > Overview` using the Admin Toolbar. Find the Conditional Fields module in the list and check the box. Click Install at the bottom of the page. You will get a success status message if the module was installed.

### Installing a Module from GitHub

Contributed modules come from [Packagist](https://packagist.org/), the main composer repository. However, CU has modules that live on Github. To add a module from Github, you have to add the repository and the package manually. In composer.json, there is a list of Github repositories in the repositories section. In the require section, the syntax is the package name with the version of dev-main.

### Theme Development

[Themes](https://www.drupal.org/docs/theming-drupal) give a site its look. The theme installed by default is the CU Boulder site theme. In the `/themes` directory of your `Sandpoint project` you will both contributed and our custom CU Boulder theme which includes CSS, JS, Twig Templates, external libraries like BootStrap and FontAwesome and more! Here is where you will build out Twig templates, build CSS and JS files for your pages, and link those newly created files to our `boulder_base.libraries.yml`

### Module Development

[Modules](https://www.drupal.org/docs/creating-modules) extend the functionality of the site by adding custom PHP code. For example, the very popular Webform Module allows users to create and track forms. Modules follow a strict OOP paradigm and often will extend existing Plugins and Controllers. They may contain configuration in the form of .yml files that can add various features such as menu links, routes, and permissions. They may also implement hooks, which are functions that can alter or extend the existing behavior of the site.

Much of module development is looking at existing module source code and using them as an example for creating your own.

---

## Site Development

### Nested Repositories within Sandpoint

Starting the app for the first time will install all the composer dependencies and clone down all of the CU Boulder modules. Even though the modules are composer packages, they are cloned with git so we can do development work on them. These modules include `ucb_custom_entities`, `boulder_profile`, and our custom UCB modules such as `ucb_default_content` which are stored within `modules/custom`.

### Branching with Sandpoint

In order to test a PR or to develop for a new issue/feature/bug, you will need to switch to the appropriate branches on each repository. Depending on the ticket assigned for review or developement, your work may touch one or more of these repos.

The repos you may need to check are:

- `themes/custom/boulder_base`
- `modules/custom/ucb_custom_entities`
- `profiles/custom/boulder_profile`
- `modules/custom/**` (For work with custom modules)


Make sure your repos are up to date before creating a branch with `git fetch -a` and then checkout the available branches with `git branch -a` in the above repo locations within the Sandpoint project to confirm your local project is up to date with the remote repo with the most current available remote branches. Run a `git status` to make sure you are up to date, `git pull` any changes if not.

To checkout to a branch for code review, run the following on each repo that may have new code, which includes the 5 above repos:

```bash
git checkout -b <LOCALBRANCHNAME> origin/<REMOTEBRANCHNAME>
```

### Pushing Code

Once you have something ready for commit, or you have code that is tested, working, and ready for a pull request-- the code push process works as you would expect. In each of the repos that resides in our Sandpoint project, we will need to push that new code to its respective remote repository. Do not push to Sandpoint remote repo, just the afformentioned custom repositories that reside within your Sandpoint project.

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
