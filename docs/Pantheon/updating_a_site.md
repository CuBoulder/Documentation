# Updating Sites On Pantheon

Pantheon uses the concept of an "upstream", which is basically a remote git repository that holds a site's codebase.

## our upstreams upstreams

1. We have one upstream in production and this is Web Express. It is no longer being developed but we do maintain it for fixing bugs, applying Drupal 7 security updates, and other similar changes. These changes are the only reason we will need to update sites using Web Express (D7).

2. The other upstream we use is pantheon-upstream-tiamat-development (Tiamat is our working codename for us to use in the absence of an actual project name). The reasons for updating sites using this upstream are the same as with Web Express (D7) but also to include recent additions by our development team.

### Web Express (D7)

Our old, legacy, code base is called Web Express. The upstream for it is found [here](https://github.com/CuBoulder/pantheon-upstream-express-production). Most of the sites we have on Pantheon (as of 6/2022) are using this code base. If you look at the code in github you will see that it contains just about everything you need. Any changes to the codebase will be made in this repository. Pantheon should notice these changes and, after the changes are made to the master branch in github, all you need to do is:

```bash
terminus upstream:updates:apply -- <sitename>.<env>
```

### Tiamat (D9)

This is the code under active development that will soon replace Web Express. The upstream is really just a couple [composer.json](Tools-index#user-content-languages) files.

steps:

1. get the site's code
    - `terminus connection:info <sitename>.dev`
    - copy and run the 'git command'
2. run `composer update`
3. git add, commit, and push back up to origin master (on Pantheon)
    - the changed composer.lock file will kick off the installation of the new packages etc
4. push code changes to the desired envs (if the site is not only on dev)
    - `terminus env:deploy <sitename>.<env>`
    - you will have to first deploy to test and then live
5. For each env you will also need to update features so that the any configuration included in the site's update will be implemented.
    - `terminus remote:drush <sitename>.<env> -- features-import-all -y`  
    (this does not seem to work as the needed content types still do not show in the site's UI)
    - `terminus remote:drush <sitename>.<env> -- cr`
