# Creating a Site

you will need a number of things to create a new site:

- terminus [installed](Pantheon-index#user-content-terminus)
- the site name

    - if this is a new site intended for site owners/editors to develop it does not need to be the final name used for a launched site.

- the name or id of an upstream

    - you can get this by running `terminus upstream: list --org="university of Colorado Boulder"` and copying the desired upstream's name or id

## **Site Creation Process**

There are many steps involved in creating a site on Pantheon. Most of these steps use the terminus cli, so open up your terminal! Some of these steps take several minutes or more to complete. Terminus prints out helpful progress messages, but be prepared to spend +- 25 minutes to create a site.

1. `terminus auth:login --machine-token=WEBSUPPORT_MACHINE_TOKEN`
2. `terminus site:create --org="University of Colorado Boulder" -- SITE_NAME SITE_NAME UPSTREAM`
3. Get the git repo for the site (only available on the dev environement) 

    1. `termiinus connection:info SITE_NAME.dev --format=json`
    2. copy the git command and run it in the directory where you want to save the code
    3. copy our D7-WebExpress settings.php file into the `web/sites/default` directory
    4. add, commit, and push the code back up to pantheon

4. deploy the updated codebase to test and live:

    - `terminus env:deploy -- SITE_NAME.test`
    - `terminus env:deploy -- SITE_NAME.live`

5. install the site (we only make use of the live site environment so we only need to install the site there)

    - `terminus remote:drush SITE_NAME.live -- si express -y`

6. [configure](Pantheon-configuring_a_site) the site

    - use the (configure a site)[Pantheon-configuring_a_site] docs to set site variables and enable/disable modules (be sure to follow the order of enabling/disabling given there!)
    - use `terminus remote:drush SITE_NAME.live -- vset VARIABLE_NAME VARIABLE_VALUE` for setting site variables
    - use `terminus remote:drush SITE_NAME.live -- en MODULE_NAME` to enable modules
    - use `terminus remote:drush SITE_NAME.live -- dis MODULE_NAME` to disable modules

### **YOU DID IT <|:-)**

The site is now available at `https://live-SITE_NAME.pantheonsite.io`
