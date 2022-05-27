# Drupal Onboarding

## Introduction

### What is Drupal?

[Drupal](https://www.drupal.org/about) is a content management system (CMS) similar to Wordpress, Wix, Squarespace, etc. This software allows users to organize and create content on a site without any coding experience. What sets Drupal apart from the others is the ability to customize the CMS and add complex features.

### How is Drupal used at CU?

Our sites use Drupal to allow users to create their own websites. We create new features for Drupal so our users can have the tools they need to create the content for their sites. For example, https://colorado.edu is built using Drupal.

### What is the LAMP stack?

A lamp stack is a popular web stack for running websites. It consists of Linux (OS), Apache (Web Server), MariaDB (Database), and PHP (Scripting Language). We will need all of these parts to run a Drupal Site. You can swap out parts of the stack, such as Apache for NGINX, but a web server must be present.

---

## Setting up a Local Enviroment for Drupal

By the end of this tutorial, you will be able to:

- Use lando to set up a Drupal 9 site locally
- Install a module
- Create new content on a Drupal site
- Create a module
- Create a subtheme

### Installing Composer

We use [Composer](https://getcomposer.org/) php package manager to install Drupal and all of its dependencies. Package managers make installing and updating software packages easier and more organized. Examples include npm for Node, pip for Python, and brew for MacOS.

Run `which composer` to check if composer is installed. If it's not installed, [install composer](https://getcomposer.org/download/)

### Setting Up Lando

Lando is a local environment tool that runs on Docker to create a container for a website. Open terminal and type `which lando`. If a path is printed, then you already have lando installed and can go to the next step. Otherwise, follow the steps to [install Docker](https://docs.docker.com/desktop/mac/install/) and then [install Lando](https://docs.lando.dev/basics/installation.html#macos)

### Initializing a Lando App

Create a directory we're going to call `d9-onboarding` as a test playground. This directory can go wherever you want your local projects to live; the documents folder, into a organized Code Project folder, wherever you please! In this new directory, create a file called `.lando.yml`. This is the configuration file Lando needs to create a development environment. Copy the following into the file.

```
name: d9-onboarding
recipe: lamp
config:
   php: ‘7.4’
   composer_version: ‘2.1.18’
   webroot: .
   database: maria
   xdebug: false
```

Both `.lando.yml` and Drupal use a data serialization language called YAML, similar to JSON and XML, for managing configuration. YAML files have a .yml extension.

This is the minimum needed to get a lamp stack configured for lando. Next we need to get the Drupal source code.

### Installing Drupal

We are now going to add a `composer.json` and `composer.lock file`, the minimum needed for a composer project. Drupal sites should be composer managed. Run the following two commands below from the project root.

```
curl https://raw.githubusercontent.com/CuBoulder/nextpress-project-template/production/composer.json > composer.json
```

```
curl https://raw.githubusercontent.com/CuBoulder/nextpress-project-template/production/composer.lock > composer.lock
```

Looking at the `composer.json` file, we can see the packages that are required for this website to work. The `composer.lock`file contains information that tells composer specifically what version of each package is required. Now that we have the packages required for our site, we need to install them by running:

```
composer install
```

This command will take a while.

Once that’s finished, a new directory called `vendor` should appear. This is where all of the dependencies live. Do Not modify any contents inside the vendor directory.

Run `lando start` and visit the url that lando gives you.

If everything worked, you will be shown the Drupal installation screen. Fill out the form fields and select the CU Boulder Install Profile for the installation profile. For the database credentials, use:

```
Username: lamp
Password: lamp
Database Name: lamp
Host: database
Port: 3306
```

Uncheck the box for sending email updates.

---

## Site Development

### Site Building

The Admin Interface is where users can make changes to their site. You can do everything from installing modules, creating content, and configuring themes and more.You can access the admin pages by using the Admin Toolbar on the left side of the site.

So far, there is no content on the site. Start by adding a page by clicking on the `Add Content > Basic Page Button`.
Fill out the fields and click save.

Content for Drupal is separated into Content Types. On this installation, the types are Article, Basic Page, and Person. Content Types organize the types of information that could live on a site.

Now we are going to configure some of the site settings. Using the admin toolbar, go to `Configuration > System > Basic Site Settings`.

In the Slogan Form input, type `Strategic Relations and Communications`. Below that, in the Default Front Page input, type `/node/1` as the path to be used for the front page. Click the `Save Configuration` button. Going back to the site, you can see the added tagline and frontpage.

### Installing A Module

Modules extend the functionality of the site. Installing a module is done in two parts, adding the composer package, and enabling it on the site itself. We are going to install the Conditional Fields module. You can find more modules on the [Drupal Website](https://www.drupal.org/project/project_module). In the project root, run the following:

```
composer require ‘drupal/conditional_fields:^4.0@alpha’
```

After the composer.\* files have been updated, go back to the site and go to `Extend > Overview` using the Admin Toolbar. Find the Conditional Fields module in the list and check the box. Click Install at the bottom of the page. You will get a success status message if the module was installed.

### Installing a Module from GitHub

Contributed modules come from [Packagist](https://packagist.org/), the main composer repository. However, CU has modules that live on Github. To add a module from Github, you have to add the repository and the package manually. In composer.json, there is a list of Github repositories in the repositories section. In the require section, the syntax is the package name with the version of dev-main.

### Drush

[Drush](https://www.drush.org/latest/) is a command line utility for interacting with a Drupal site. It’s extremely useful and learning the commands will make development much faster. Since the dev site is using Lando, we must prefix all drush commands with lando.

Try clearing the cache by running `lando drush cr`!

### Theme Development

Themes give a site its look. The theme installed by default is the CU Boulder site theme.

### Enable Twig Debugging

The markup for a Drupal Site uses a PHP templating engine called [Twig](https://twig.symfony.com/). This allows us to write HTML quickly and connect the markup to PHP logic in a fast, safe manner. Enabling Twig debugging will allow us to determine what templates are outputting the markup.

To enable Twig debugging, run the following commands from project root.

```
cd sites/default
sudo cp default.services.yml services.yml
```

You may need to change ownership of this new `services.yml` file. Depending on your computer's user settings & permissions, you may not be able to edit and save changes to your `services.yml` file. If you need to change file ownership, this can be achieved by running the following command with your local user name inserted into the `*USERNAME*` placeholder.

```
sudo chown *USERNAME* services.yml
```

Open services.yml in a text editor of your choice. On line 74, change the line `debug: false` to `debug: true`. Save and exit this file. If you get any permission errors, see above.

Go back to the site and inspect a page with the browser dev tools. You will now see comments in the markup about which templates are being rendered!

### Module Development

Modules extend the functionality of the site by adding custom PHP code. For example, the very popular Webform Module allows users to create and track forms. Modules follow a strict OOP paradigm and often will extend existing Plugins and Controllers. They may contain configuration in the form of .yml files that can add various features such as menu links, routes, and permissions. They may also implement hooks, which are functions that can alter or extend the existing behavior of the site.

Much of module development is looking at existing module source code and using them as an example for creating your own.

---

## Contributing Code - Nextpress

We use our [nextpress project template](https://github.com/CuBoulder/nextpress-project-template) to quickly get a development version of nextpress running. DO NOT use this branch in production! The production composer.\* files can be found on the production branch.

### Nextpress Installation

```
composer -V             # verify that your machine has composer 2.x installed

git clone https://github.com/CuBoulder/nextpress-project-template <project-name>

cd <project-name>

open .lando.yml file and replace the name value on line 1 with your project name

lando start             # this command will take a while if it's the first it's being run
lando install-site      # this installs Drupal

```

Other useful commands:

```
lando info   ##Prints info about your app including urls to visit your page, database info and more

lando drush pmu simplesamlphp_auth 	 ## allows local logins and disables SSO

cd sites/default && sudo cp default.services.yml services.yml   ## creates a services.yml file

sudo chown <USERNAME> services.yml     ## May be needed to change read/write access of your new services.yml file

```

### Site Development

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
