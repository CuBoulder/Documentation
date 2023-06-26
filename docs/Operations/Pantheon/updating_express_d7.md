# Updating Express D7

Pantheon makes use of the 'upstream' repository design and flow for working with a web site's codebase. The basic idea is that many sites can use the same git repository for their codebases. This is a great idea but our implementation actually uses 2 git repositories, both of which are hosted on GitHub, instead of just one.

1. https://github.com/pantheon-systems/drops-7/tree/default
    - this is the Drupal 7 codebase maintained by Pantheon
2. https://github.com/CuBoulder/pantheon-upstream-express-production/tree/master
    - known as d7 Web Express
    - this is a mono-repo of the drops-7 repo above and our custom code and applications based on the Drupal 7 framework which is found in `/web/profiles/express`.

## 3 reasons to update

1. There was an update to the drupal 7 core repo (drops-7)
2. The Web Express code base was updated
    - as a rule there is no longer any active development done in d7 express. Updates are only made to fix bugs etc.
    - the actively developed version of Web Express
3. Both of the above.

## Where make changes to Web Express

- Make an issue, if not already present, and a branch in the Web Express repo and carry out your work in it.
- The Web Express code is found in the `/web/profiles/express` directory. Please do not make changes in any other directory.
- Upon completion, create a PR targeting the `master` branch (Pantheon only accepts code from master branches of upstreams) and choose your reviewers.
- You are done. The reviewers will merge the code and prepare a new release.

## Update Drupal 7 code

1. In the Web Express repo create an issue called `drupal/DRUPAL_VERSION_NUMBER`
2. Clone the Web Express repo from above and create a branch with the same name as the newly created issue.
1. Clone the drops-7 repo given above.
4. Copy the `web/profiles/express` from Web Express in to drops-d7 at the same location
5. Delete everything in Web Express repo
6. Copy the entire drops-7 repo into Web Express repo
7. Add and commit Web Express changes with a message "updating Drupal 7 Core to version VERSION_NUMBER"
8. Push changes up to Web Express GitHub repo and create a PR that targets the master branch. Add reviewers.
9. You are done.

## Make an express release
(TODO: describe where to update Express version numbers and related data)

- There should be a pr in a development branch that targets `master` branch. After reviewing this pr simply merge it into master.
- You are done. Pantheon will see the change to this repo and you will be able to update each site's codebase via Pantheon's tools [(see below)](#start_an_update).

## Start An Update

We update our sites based on update groups (TODO: Is this still accurate?) and use tools to automate this process. However, it is easy to update sites individually through Pantheon's dashboard.

1. Log in to Pantheon and navigate to the site you with to update with changes to our codebase.
2. Go to the "Dev" tab in the top left of the window and select the "Code" option in the left sidebar.
3. You should see that there is a code update to make. Go ahead and make it, opting in for any database updates if needed/asked.
4. Repeat this step in the Test and Live tabs
5. That should be it!