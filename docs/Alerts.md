# Alerts

This site is a non-express, custom site that is hosted on Pantheon. In order to execute the directions in this file you will need to install Pantheon's [Terminus](https://pantheon.io/docs/terminus/install) command line tool. Please do that first. Also, you will need a token from Pantheon to be able to login and interact with this site. Follow [this](https://pantheon.io/docs/machine-tokens) procedure to create one if you do not have one already.

This documentation assumes that you are using a terminal/command line app and that you know how to navigate around and use git using it.

## Login

- To do anything with sites on Pantheon via Terminus you will first need to login:
```
terminus auth:login --machine-token=YOUR_MACHINE_TOKEN
```

## Get Site Code Via Git

1. Each site on Pantheon has its own git repository so getting the site's code to make changes is pretty simple. First you need to ask for the git connection information. 
```
terminus connection:info ucb-alerts.dev
```

2. Navigate to the desired location for the alerts' code
3. Clone usb-d9-alerts down by pasting the git command into your terminal and then cd into the new directory.
```
git clone ssh://SOMETHING_VERY_LONG ucb-alerts
cd ucb-alerts
```

## Performing Updates

1. Perform initial backups
```
terminus backup:create ucb-d9-alerts.dev --element all
terminus backup:create ucb-d9-alerts.prod --element all
```

2. Rune composer update to update packages listed in composer.json file
```
composer update
```

3. Add, commit, and push updates to repo
```
git add -A
git commit -m "Composer update"
git push
```

5. Perform DB updates and clear cache
```
terminus remote:drush -- updb -y
terminus remote:drush -- cr
```

6. Log in and confirm updated site is working as expected.
```
terminus remote:drush -- uli
```

7. Perform final backups
```
terminus backup:create ucb-d9-alerts.dev --element all
terminus backup:create ucb-d9-alerts.prod --element all
```
