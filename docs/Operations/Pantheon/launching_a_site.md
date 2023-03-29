# Launching A Site

Launching is our word for publishing a site to the *production* www.colorado.edu domain. There are two kinds of site launches:

1. launching a brand new site
2. launching an new/updated site to a previously launched/published site already in production.

In general you will need the following information:

- the SITE_NAME of the *development* site requesting to be launched
- the database and files backups for the *development* site. You can get urls for those like this:
    - `terminus backup:create SITE_NAME.live`
    - `terminus backup:get --element=files`
    - `terminus backup:get --element=database`
- an approved site path for the launched *production* site (for case number 1. above)
- a new *production* site name (Again, for case number 1. above. If case number 2. you should already know the production site's name)
  - this is derived from the site path
  - for example 'lab/somelab' will be named 'ucb-lab-somelab'

## process

if case number 2. above, skip to step 5. You will not be creating a new production site, but rather using a site already in production.

1. [create a site](Pantheon-creating_a_site) using the new production site name
    - skip steps 5. and 6.
2. `terminus plan:set NEW_SITE_NAME "plan-basic_small-contract-annual-1"`
3. `terminus domain:add NEW_SITE_NAME.live NEW_SITE_NAME.agcdn.colorado.edu`
    - this connects these two domains together so that the site path can be added to the agcdn in order to be accessed at www.colorado.edu/SITE_PATH
4. update the site's web/sites/default/settings.php file with the production site's path:
    - in this file add or update the line setting the site's path to `$conf["cu_path"] = "THE_APPROVED_SITE_PATH";`
5. import database and files from development site to new site:
    - if this is case number 2., from above, be sure to back up the production site before importing the development site's files and database.
        - `terminus backup:create PROD_SITE_NAME.live`
    - `terminus import:files PROD_SITE_NAME.live FILES_URL_YOU_GOT_EARLIER`
    - `terminus import:database PROD_SITE_NAME.live DATABASE_URL_YOU_GOT_EARLIER`
6. [configure](Pantheon-configuring_a_site) the production site
7. Add the site to the agcdn
    - TODO: docs for this!
