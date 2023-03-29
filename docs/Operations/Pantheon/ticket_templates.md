# Ticket Templates

This is a collection of templates to aid in creating common support tickets on Pantheon. It is best to open a ticket by going to the support section from the specific site's dashboard. You can do it from CU Boulder's org dashboard but you MUST be very specific about the site you want something changed for.

## add new site to agcdn

This ticket will be created when a site needs to be 'launched' (published  the www.colorado.edu url). This site will not have an sid from atlas as it was never hosted at CU. Before you open this ticket be sure that the site referred to in this ticket:

1. is created by the websupport user
2. it has been deployed to the live environment
3. the agcdn domain has been added to the live environment

--> see [creating a new site](Pantheon-creating_a_site)

When opening the support ticket simply select the most relevant options from the select boxes etc. Replace SITE_NAME and SITE_PATH. SITE_NAME should start with 'ucb', SITE_PATH is what we want appended to 'www.colorado.edu' to access this site.

### _**template**_

Please apply the following change in University of Colorado - CU Boulder AGCDN

Add in req_metadata_v1_01 dictionary:

```
colorado-edu-allenvs/SITE_PATH/*: dm=SITE_NAME.agcdn.colorado.edu|preset=drupal7
```

## add site from on permise hosting to agcdn

This ticket will be created when a site needs to be 'launched' (published  the www.colorado.edu url). This site will have been migrated from CU hosting and should have an atlas sid. Before you do this be sure that the site referred to in this ticket:

1. is created by the websupport user
2. it has been deployed to the live environment
3. the agcdn domain has been added to the live environment

--> see [creating a new site](Pantheon-creating_a_site)

When opening the support ticket simply select the most relevant options from the select boxes etc. Replace SITE_NAME, SITE_PATH, and ATLAS_SID in the template with the relevant values. SITE_NAME should start with 'ucb', SITE_PATH is what we want appended to 'www.colorado.edu' to access this site, and ATLAS_SID is the sid created for each site by atlas for CU hosting.

### _**template**_

Please apply the following change in University of Colorado - CU Boulder AGCDN

Add in req_metadata_v1_01 dictionary:

```
colorado-edu-allenvs/SITE_PATH/*: dm=SITE_NAME.agcdn.colorado.edu|preset=drupal7
colorado-edu-allenvs/ATLAS_SID/*: sc=301|t=/SITE_PATH$wildcard
```

Add in internal_paths dictionary:

```
/ATLAS_SID: /SITE_PATH
```
