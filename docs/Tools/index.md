# Tools

We are provided a Macbook Pro for our work here at CU Boulder. These docs are meant for macOS. If you prefer another OS this documention may not be accurate.

## Most common tools

Here is a basic list of tools and technologies that we use frequently:

### **Version control**

- git

### **IDEs**

- [Visual Studio Code](https://code.visualstudio.com/)
  - free and very capable
  - most of us here use it
- [JetBrains](https://www.jetbrains.com/)
  - not free but great IDEs
  - PhpStorm
  - PyCharm
  - WebStorm
  
There are others worth consideration but the above are used by team members and have been proven to work well for us.

### **languages**

- PHP
- [Composer](https://getcomposer.org/)
  - PHP package management
- Python
- [pip](https://pip.pypa.io/en/stable/)
  - Python package management
- [venv](https://docs.python.org/3/library/venv.html)
  - used for creating virtural environments for local Python development (included with Python now)
- [Node](https://nodejs.org/en/)
  - mainly used for running automated tests via Playwrite
  - you might use it for command line apps or APIs, too
- [Npm](https://www.npmjs.com/)
  - for node/javascript package management
- Javascript
- CSS
  - for a few of its modern features check [this](https://css-tricks.com/whats-new-since-css3/) out
- HTML
  - this includes templating languages [Twig](https://twig.symfony.com/) (PHP) and [Jinja](https://jinja.palletsprojects.com/en/3.1.x/) (python)

### **Frameworks**

- [Drupal](https://drupal.org)
  - although this is commonly referred to as a CMS, it is perhaps more accurately described as a Content Management Framework
- [Symfony](https://symfony.com/)
  - PHP framework that Drupal is built on top of
  - although you might not often use it directly, it would be good to get to know it
- [FastAPI](https://fastapi.tiangolo.com/)
  - Python framework for building API's and applications

### **Development stacks**

We need working LAMP stacks for our Drupal projects. This is largely provided for by Lando (see below). Non-Drupal projects, for example and API built with Python, can normally be developed on our macs directly, with the understanding that their production environments will likely be Linux based.

#### **_databases_**

Although Lando more or less takes care of setting up databases, there may be a specific need in a project for you set one up yourself.

Typically we use:

- mariaDb
- mysql
- sqlite

## Beginning set up

There are 2 technologies that we use for installing and/or using these languages: Homebrew and Lando. Generally, we do not need to install Xcode, however we will need to get access to the "Command Line Tools", commonly bundled with XCode.

### Command Line Tools
Since Apple’s OS X is based on UNIX, you can run many of the UNIX commands on your Mac right from the Terminal app. In order to use these UNIX commands on your Mac, you need to have a utility called “Command Line Tools” installed on your machine. By default, OS X does not ship with this utility installed. One way to install Command Line Tools it is to install Xcode, and it will install these commands as well. However, Xcode is heavy in filesize an often takes hours to fully install on your machine so the full installation is not recommended unless it is absolutely necessary. 

To get Command Line Tools quickly without XCode, open Terminal and run the following command:

```
xcode-select --install
```

You will be prompted asking if you would like to install the command line tools on your machine. Click on the “Install” button.Read the license agreement on the following screen and click on “Agree” to move forward. When the tools are downloaded, click on “Done” in the dialog box to complete the installation. Congratulations, the command line tools are successfully installed without requiring you to install Xcode!

### _homebrew_

[Homebrew](https://brew.sh/) is the 'traditional' route to getting most of the things listed above installed. Copy the snippet on their homepage to install it. Please check out their documentation as well.

To start with, you can install the following items. You can install more as needed for the projects you are working on.

```bash
brew install git
brew install php
brew install composer
brew install python@3.10
brew install node
```

### _Lando_

[Lando](https://lando.dev/) is a container managment tool that really helps software development go smoothly. Basically, it installs Docker and creates a container, with a complete development stack, for your application. This is very convenient for working with Drupal as it handles OS, server, database, and PHP for us.

To install it select the [latest release](https://github.com/lando/lando/releases). The installers are found in the 'assets' section. Download and run the appropriate installer for your computer:

- If you have a new Mx based mac be sure to download the arm .dmg
- If you have an older Intel mac download the x64 .dmg

Be sure to checkout the Lando [documentation](https://docs.lando.dev/) for to get an idea for what it can do.

## Other tool docs

Be sure to check out, and update as needed, the documentation we have for specific tools and how we typically get them set up for our projects.
