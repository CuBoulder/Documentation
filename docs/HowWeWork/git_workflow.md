# Git Workflow

Development work should generally be associated with a GitHub issue. Each issue gets its own short-lived branch, commits reference the issue number, and completed work is merged through a GitHub Pull Request.

## Start a Branch

Before beginning work, make sure there is a GitHub issue describing the change.

The preferred way to create a branch is directly from the GitHub issue:

1. Open the issue in GitHub.
2. Find the **Development** section in the right sidebar.
3. Select **Create a branch**.
4. Name the branch using the issue number:

```text
issue/#<number>
```

For example:

```text
issue/#123
```

5. Select the option to work on the branch locally.
6. Run the Git commands provided by GitHub to check out the new branch.

Creating the branch from the issue connects the branch to the issue in GitHub and keeps the work associated with the original request.

### Creating a Branch Manually

If needed, a branch can also be created locally from the repository's default branch:

```bash
git switch main
git pull
git switch -c "issue/#123"
git push -u origin "issue/#123"
```

Replace `123` with the GitHub issue number. If the repository uses a default branch other than `main`, use that branch instead.

## Commit Changes

Stage your changes:

```bash
git add -A
```

Commit them with a short description of the change. Include the GitHub issue number at the beginning of the commit message:

```bash
git commit -m "#123 Updated block styles for Article List Block"
```

Using `#<issue number>` references the GitHub issue associated with the work and makes it easier to trace commits back to the reason the change was made.

Commit messages should briefly explain what changed rather than simply repeating the issue title.

For example:

```bash
git commit -m "#123 Added a new View mode for Discovery"
git commit -m "#123 Changed Site Manager permissions to allow Layout Builder"
git commit -m "#123 Removed stray configuration for Trash module"
```

Multiple commits can reference the same issue.

## Push Changes

After committing, push the branch to GitHub:

```bash
git push
```

If the branch was created locally and has not been pushed before:

```bash
git push -u origin "issue/#123"
```

After the upstream branch has been configured, future updates only require:

```bash
git push
```

## Create a Pull Request

When the work is ready for review, open a Pull Request in GitHub from the issue branch into the repository's default branch.

For example:

```text
issue/#123 → main
```

If the branch was created from the GitHub issue, GitHub will associate the branch and Pull Request with that issue.

The Pull Request should include enough information for another developer to understand what changed and anything they should verify during review.

When appropriate, the Pull Request description can also use GitHub's closing syntax:

```text
Resolves #123
```

or:

```text
Fixes #123
```

When the Pull Request is merged into the default branch, GitHub will automatically close the referenced issue.

## Updating Your Branch

If the default branch changes while you are working, update your local copy before bringing those changes into your branch:

```bash
git switch main
git pull
git switch "issue/#123"
git merge main
```

Resolve any conflicts locally, test the result, commit if necessary, and push the updated branch.

## After a Pull Request Is Merged

Once the Pull Request has been merged, the issue branch is no longer needed.

Switch back to the default branch and update it:

```bash
git switch main
git pull
```

The local issue branch can then be deleted:

```bash
git branch -d "issue/#123"
```

The remote branch can also be deleted through GitHub after the Pull Request is merged.

## General Guidelines

* Create a GitHub issue before beginning development work whenever possible, or use an existing ticket if one exists.
* Use one branch per issue.
* Name branches `issue/#<number>`, such as `issue/#123`, even across repos. 
* Create branches from the repository's default branch.
* Reference the issue in commit messages using `#<number>`.
* Push work to the issue branch rather than directly to the main branch.
* Use Pull Requests for review and merging.
* Delete issue branches after their Pull Requests have been merged.
* Keep branches focused on the issue they were created to address.
