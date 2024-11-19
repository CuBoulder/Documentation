# Make a Web Express Release

Currently, Web Express is on a 1 week release schedule.

The code base for Web Express is spread accross multiple repositories in CU's github organization. In addidtion we have a two repos for development and production upstreams that are used to create sites on Pantheon using Composer.

To cut a new release we need to work in 3 repos:

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

## changes to the upstreams

TODO: What does Michael do here?