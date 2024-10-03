# Creating a Site

you will need a number of things to create a new site:

- terminus [installed](Pantheon-index#user-content-terminus)
- the site name
    - We have naming conventions for our site names. Please be sure to follow them. Firstly, see [this page](https://www.colorado.edu/webcentral/get-help/url-standards) for general conventions and then replace any '/' with '-'. In addition, each type of site needs a particular prefix:
        - a development site uses the prefix `ucbdev-`
        - training sites use `ucbtraining-`
        - a site that we host on Pantheon that shows up on colorado.edu as a subdomain (www.SUBDOMAIN.colorado.edu) uses `ucbsub-`
        - a D10 production site uses `ucbprod-`
        - previous D7 production sites used `ucb-` as a prefix
    - If this is a new site intended for site owners/editors to develop it does not need to be the final name used for a launched site. Just make a easily decipherable name. We create a new site upon site launch with a name that follows url guidelines and that site owners have agreed to.

- the name or id of an upstream

    - you can get this by running `terminus upstream: list --org="university of Colorado Boulder"` and copying the desired upstream's name or id

## **Site Creation Process**

There are many steps involved in creating a site on Pantheon. Most of these steps use the terminus cli, so open up your terminal! Some of these steps take several minutes or more to complete. Terminus prints out helpful progress messages, but be prepared to spend +- 25 minutes to create a site.

1. `terminus auth:login --machine-token=WEBSUPPORT_MACHINE_TOKEN`
2. `terminus site:create SITE_NAME SITE_NAME UPSTREAM --org="University of Colorado Boulder"`
    - for D7 sites use `pantheon_upstream_express_production` for the upstream
    - for D10 sites use `tiamat_production` for the upstream
    - be sure to use the correct site name pattern -> TODO: NAMING CONVENTIONS DOCUMENTATION

3. Get the git repo for the site (only available on the dev environement)

    1. `termiinus connection:info SITE_NAME.dev --format=json`
    3. copy the git command and run it in the directory where you want to save the site's code
    2. copy the saml private directory to the site's root level directory (should be one level above the `web` directory)
    4. __ONLY FOR D7 SITES__: copy our D7-WebExpress settings.php file into the `web/sites/default` directory (our D10 sites no longer need such a settings file)
    5. add, commit, and push the code back up to pantheon

4. install the site

    - for D7: `terminus remote:drush SITE_NAME.live -- si express -y`
    - for D10: `terminus remote:drush SITE_NAME.live -- si boulder_profile -y`

5. initialize and deploy code and database to test and live environmets:

    - `terminus env:deploy -- SITE_NAME.test`
    - `terminus env:deploy -- SITE_NAME.live`

6. [configure](Pantheon-configuring_a_site) the site

    - **FOR D10 SITES**
        - At this point all default configuration is taken care of in the install profile.

    - **FOR D7 SITES**

        - use the (configure a site)[Pantheon-configuring_a_site] docs to set site variables and enable/disable modules (be sure to follow the order of enabling/disabling given there!)
        - use `terminus remote:drush SITE_NAME.live -- vset VARIABLE_NAME VARIABLE_VALUE` for setting site variables
        - use `terminus remote:drush SITE_NAME.live -- en MODULE_NAME` to enable modules
        - use `terminus remote:drush SITE_NAME.live -- dis MODULE_NAME` to disable modules

### **YOU DID IT <|:-)**

The site is now available at `https://live-SITE_NAME.pantheonsite.io`. You should be able to login using saml and invite users and more.
