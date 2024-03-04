# D10 Nested Hosting

We have been using a nested hosting pattern for all of our sites at University of Colorado Boulder. This means that we own the domain "www.colorado.edu" and all of our sites are appended to that as distinct paths.

## How D7 Worked

In Drupal 7 we were able to rewrite the site's domain and path in each site's web/sites/default/settings.php file. The path, in D7 Express, is defined in the variable `$cu_path`, and the domain and path are combined to form another variable: `$base_url`, which always follows the `https://www.colorado.edu/<cu_path>` pattern, which is then used to form links and many similar things correctly so that the site functions as expected.

## That Works In D10, Too, Right?

Actually, this doesn't work in Drupal 10 as it does not allow the sites domain and similar to be overwritten in the settings.php file, which is probably a good thing. In fact, a special module needs to be created to take care of this. Thankfully, Pantheon has created just such a module -> [pantheon_domain_masking](https://github.com/pantheon-systems/pantheon_domain_masking).

## Setup for a nested D10 Site

Normally we have a developoment site that a customer has used to build their site. When this customer is ready to have it published we 'launch', which is the process of making it available as a nested colorado.edu site. This involves copying files and the database from the development site as well as the steps below, that are the focus here.

1. make sure you include the pantheon_domain_masking module in your composer.json file
2. create the site on Pantheon in the regular way (make sure to use the correct upstream etc)
3. Run the following drush commands (via terminus for example):
    1. `pm:enable pantheon_domain_masking`
    2. `config:set pantheon_domain_masking.settings enabled --yes`
    3. `config:set pantheon_domain_masking.settings domain www.colorado.edu --yes`
    4. `config:set pantheon_domain_masking.settings subpath <cu_path> --yes`
    5. `config:get pantheon_domain_masking.settings`
        - this last command is to check that the settings are correct.

## AGCDN Settings

- log into the [AGCDN Dashboard](https://agcdn.ps-pantheon.com/acdn-management/) using you CU identikey and password
- wait a few moments for the page to load
- click 'edit' for the `req_metadata_v1_01` item in the list and wait again for a few moments for it to load correctly.
- scroll to the bottom of the page and click 'add'
- type `colorado-edu-allenvs/<cu_path>/*` and click 'enter'
- type `dm=<site_name>.agcdn.colorado.edu|preset=drupal8
    - even though our codebase is D10 or later, ther preset is **_supposed_** to be 'drupal8'
- click 'save' and wait 5 minutes or so, maybe less, and check if your site is available at https://www.colorado.edu/<cu_path>