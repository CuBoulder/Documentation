# Creating A Site

you will need a number of things to create a new site:

1. terminus [installed](wiki/Pantheon-index#user-content-terminus)
2. the site name
    - if this is a new site intended for site owners/editors to develop it does not need to be the final name used for a launched site.
3. the name or id of an upstream
    - you can get this by running `terminus upstream: list --org="university of Colorado Boulder"` and copying the desired upstream's name or id

## process

1. `terminus auth:login --machine-token=WEBSUPPORT_MACHINE_TOKEN`
2. `terminus site:create --org="University of Colorado Boulder" -- SITE_NAME SITE_NAME UPSTREAM`
3. Initialize all environments:
    1. `terminus env:deploy -- SITE_NAME.test`
    2. `terminus env:deploy -- SITE_NAME.live`
4. The site is now available at `https://live-SITE_NAME.pantheonsite.io`
