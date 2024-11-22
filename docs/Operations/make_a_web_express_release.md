# Make a Web Express Release

Currently, Web Express is on a 1 week release schedule with updates first to our [development](https://github.com/CuBoulder/pantheon-upstream-tiamat-development) upstream, typically on Wednesdays, and later to [production](https://github.com/CuBoulder/pantheon-upstream-tiamat-production), typically on Fridays. This allows a couple of days for releases to be published to sites using our development upstream for verification by other SRC teams before publishing it to our production sites (everything on colorado.edu).

This workflow requires us to make a new release early to mid-week, somewhat depending on progress of current prs that are desired as a part of the new release. This schedule may be changed to a bi-weekly pace in the future.

The code base for Web Express is spread accross multiple repositories in CU's github organization. In addidtion we have a two repos for development and production upstreams that are used to create sites on Pantheon using Composer.


### cut a new release

We will work in 3 repos:

1. [boulder_base](https://github.com/CuBoulder/tiamat-theme) -- AKA tiamat-theme
2. [ucb_custom_entities](https://github.com/CuBoulder/tiamat-custom-entities) -- AKA tiamat-custom-entities
3. [boulder_profile](https://github.com/CuBoulder/tiamat10-profile/tree/main) -- AKA tiamat10-profile

## run repo actions

In each of the repos listed above:

- click the `Actions` tab in the top menu
- click `Draft new release` in the left sidebar
- click the `Run workflow` button
- enter the version name for this release using the pattern of `YYYYMMDD`
- click `run workflow`

This workflow will create a git tag and branch named `release/YYYYMMDD`, a change log describing the changes included in the release, and a pull request for the release.

#### in tiamat-theme only
>
- clone this repo to your computer
- checkout the new release branch
- open `config/install/boulder_base.settings.yml`
- alter the value for `web_express_version` to match the release name/date
- add/commit/push this change back up the release branch on github

After this review the prs and merge them in if all looks in order.

## during D7 -> D10 migration

- go to [tiamat10-project-template](https://github.com/CuBoulder/tiamat10-project-template)
- clone the code to your local computer (if you have not done so already)
- create a new branch named the new release name (following the `YYYYMMDD` pattern)
- in the root level `composer.json` file go to the `"require"` block and change the `"cu-boulder/boulder_base"`, `"cu-boulder/boulder_profile"`, and `"cu-boulder/ucb_custom_entities"` values to the `"YYYYMMDD"` for this release.
- save the file
- run `composer update`
- git add, commit, and push changes back up to the remote on the new release branch

## changes to the upstreams

Remember from above that we have two upstreams that are used to create sites on Pantheon.

### for development

1. clone the repo locally
2. run `composer update-upstream-dependencies`
3. run `composer update`
4. git add/commit/push, with commit message of the release name/date from above, back up to the master branch

### for production

1. clone the production repo locally
2. copy `./upstream-configuration` directory from development
3. copy `./composer.json` from development
4. copy `./composer.lock` from development
5. git add/commit/push, with commit message of the release name/date from above, back up to the master branch

## Run the update on sites hosted on Pantheon

Now that there is a fresh Web Express release you will probably want to update sites with it! This section will be filled in more but, for now, you need to run the following commands for each site you want to update:

1. `terminus site:upstream:clear-cache SITE_TO_UPDATE
terminus upstream:updates:apply SITE_TO_UPDATE.dev --accept-upstream`
2. `terminus env:deploy SITE_TO_UPDATE.test --yes`
3. `terminus env:deploy SITE_TO_UPDATE.live --yes --updatedb --cc`
4. `terminus remote:drush SITE_TO_UPDATE.live -- cr`
5. `terminus remote:drush SITE_TO_UPDATE.live -- en media_alias_display media_entity_file_replace media_file_delete menu_block ckeditor5_paste_filter scheduler layout_builder_iframe_modal linkit administerusersbyrole google_tag menu_firstchild responsive_preview anchor_link smtp recaptcha_v3 rebuild_cache_access ckeditor5_bootstrap_accordion ucb_drush_commands menu_item_extras ucb_styled_block ucb_linkmod --yes`
6. `terminus remote:drush SITE_TO_UPDATE.live -- features:import cu_boulder_content_types --yes`
7. `terminus remote:drush SITE_TO_UPDATE.live -- config:import --partial --source=/code/web/profiles/custom/boulder_profile/config/install --yes`
8. `terminus remote:drush SITE_TO_UPDATE.live -- updb --yes`
9. `terminus remote:drush SITE_TO_UPDATE.live -- cr`