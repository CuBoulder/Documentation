# Project Management

We use github for our project management, as well as code management, in a _Kanban-esque_ fashion. You will need a github account. Once you do you will get an invitation to join our organization and gain access to our repositories and project boards.

## projects

There are 2 main projects that we use for project management:

1. [Development](https://github.com/orgs/CuBoulder/projects/16)
2. [Operations](https://github.com/orgs/CuBoulder/projects/15)

Both of them have the same basic outline of 5 columns. As we plan and work on issues the cards on this board are moved around, which changes issue status to match the column.

1. Backlog
    - work items that we are not actively working on but know we will at some point
    - commonly, new issues go straight into this column
2. Todo
    - work items taken from the backlog or entered entered as needed into this one
    - these are issues that are not yet assigned but have been planned as current priorities
    - if you do not have an issue to work on, this is where you go to look for one
3. In Progress
    - you will make a branch based on dev to begin work on these issues
    - these should all have an assignee
    - the issues currently being worked on
    - keep notes on your work in these issues
4. In Review
    - when you think you are done your issue card goes in this column
    - create a PR and link it to your issue
    - make sure you add reviewers to the pr
    - use the pr for notes related to code review
5. Done
    - work on these issues is completed and the code is merged into dev

## Project decisions

In our weekly project management meetings we any of the following:

1. Populate the Backlog
2. Take issues from Backlog to Todo
3. Assign work in Todo to team members

Also, individually or in conversations outside of our project management meetings you can:

1. Move an issue that is assigned to you into In Progress when you start work on it
2. Create a linked pr and move the issue to In Review when you think you are done and want it to be reviewed
3. If you are done with your issues and are looking for more work, grab an unassigned issue from Todo, asssign it to yourself and move it into In Progress to start working on it

## Documentation

Always document what you have been working on in your issues by adding notes liberally as well as informative commit messages. **Good descriptions in your prs are required** as that is what we take to create regular changelogs to document our accomplishments as well as periodic releases.
