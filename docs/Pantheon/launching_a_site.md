# Launching A Site

Launching is our word for publishing a site to the www.colorado.edu domain. To do this you will need:

- the sitename of the site requesting to be launched
- the database and files backups for the requesting site
- an approved site path for the launched site
- a new site name
  - this is derived from the site path
  - for example 'lab/somelab' will be named 'ucb-lab-somelab'

## process

1. [create a site](Pantheon-creating_a_site) using the new site name
2. `terminus plan:set NEW_SITE_NAME "plan-basic_small-contract-annual-1"`
3. `terminus domain:add NEW_SITE_NAME.live NEW_SITE_NAME.agcdn.colorado.edu`
    - this connects these two domains together so that the site path can be added to the agcdn
4. import database and files from development site to new site
    - Documentation needed for this!
5. `terminus site:info NEW_SITE_NAME`
    - copy the site id from the output of this command
6. copy the site id, NEW_SITE_NAME, and SITE_PATH and [create a ticket](Pantheon-ticket_templates#user-content-add-site-to-agcdn) to add this site to the agcdn so it will be available at `www.colorado.edu/SITE_PATH`
    - this has typically taken 1 business day for Pantheon to complete
