# Tools

We are provided a Macbook Pro for our work here at CU Boulder. These docs are meant for macOS. If you prefer another OS this documention may not be accurate.

## Most common tools

Here is a basic list of tools and technologies that we use frequently:

### Version control

- git

### languages

- PHP
- Composer
  - PHP package management
- Python
- pip
  - Python package management
- venv
  - used for creating virtural environments for local Python development (included with Python now)
- Node
  - mainly used for running automated tests via Playwrite
  - you might use it for command line apps or APIs, too
- Npm
  - for node/javascript package management
- Javascript
- CSS
  - for a few of its modern features check [this](https://css-tricks.com/whats-new-since-css3/) out
- HTML
  - this includes templating languages Twig (PHP) and Jinja(python)

## Frameworks

- **Drupal**
  - although this is commonly referred to as a CMS, it is perhaps more accurately described as a Content Management Framework
- Symfony
  - PHP framework that Drupal is built on top of
  - although you might not often use it directly, it would be good to  
- FastAPI
  - Python framework for building API's and applications
- Vue
  - web components
  - cool front-end applications

## Development stacks

We need working LAMP stacks for our Drupal projects. This is largely provided for by Lando (see below)

### databases

Although Lando more or less takes care of setting up databases, there may be a specific need in a project for you set one up yourself.

Typically we use:

- mariaDb
- mysql
- sqlite

## Set up

There are 2 technologies that we use for installing and/or using these languages: Homebrew and Lando.

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

Lando is a container managment tool that really helps a lot of software development go smoothly. Basically, it installs Docker and creates a container, with a complete development stack, for your application. This is very convenient for working with Drupal as it handles OS, server, database, and PHP for us.

Install it and then checkout the documentation for getting a Drupal instance up and running.
