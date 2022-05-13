# Pantheon Hosting

As of May 2022 all of our production sites are hosted on [Pantheon](https://pantheon.io).
There are a few basic concepts that are good to write about here, but for anything else please look at their [docs](https://pantheon.io/docs).

## overview of pantheon services

There is quite alot that we are receiving from hosting our sites on Pantheon. All developers here at University of Colorado Boulder should have accounts set up on Pantheon so you can create/edit/manage sites as allowed by your role there.

### environments for each site

Each site has 3 environments:

1. dev
2. test
3. live

In addition each site can have up to 10 [multidev environements](https://pantheon.io/docs/multidev) that can be used to develop fix a particular site without effecting any of the 3 listed above or a workflow that may have been built around them.

Each environment has its own database, files, and code base. The live environment is where production sites live. Therefore this is where site owners and editors sign in and develop their sites meaning that the database here is the most important and up to date.

Urls for sites on pantheon follow the pattern `https://<env>-<sitename>.panteonsite.io`. In addition, once a site is 'launched' the live environment is linked to colorado.edu's base url like so: `https://www.colorado.edu/<sitepath>`

### pantheon dashboard

To interact with sites you can log in to access University of Colorado Boulder's [dashboard](https://dashboard.pantheon.io/organizations/81be1591-5c06-4339-827f-d9a3605288be) and look around there.

## terminus

But for development Pantheon has built a tool called [Terminus](https://pantheon.io/docs/terminus). Click the link there to see how to install it if you do not have it already and also to check out its documentation.

After installing terminus be sure to set up a machine token and ssh key as described in the installation docs Once that is done before you run commands with terminus you will have to authenticate:
```
terminus auth:login --machine-token=YOUR_MACHINE_TOKEN
```

## getting a site's code with git

Each site env on Pantheon is also a git repository. However we are given direct via git access only to the dev environment. This is just fine as we would not want to work directly on a live site's code in most cases.

After you login (described above):

1. Navigate, in your terminal app, to the directory you want the code base to be.
2. run `terminus connection:info <sitename>.dev`
    - the output from this command will include a 'git clone' line that you can copy and paste back into your terminal to clone the repo to your computer
3. `cd` into the site's newly cloned diirectory.
4. That is it, you have the code!

## agcdn

This is Pantheon's 'Advanced Global Content Delivery Network'. Basically, it is their implementation of Fastly.

The importance of the AGCDN to us is that the domain `www.colorado.edu` is pointed at it and therefore any launched site (a site we want to be accessed via that domain) must be added to this AGCDN first. To learn how to do this, read [launching a site](wiki/Pantheon-launching-a-site).
