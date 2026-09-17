# Git Workflow

## General Guidelines

### Development
- <strong>Do not work directly on main.</strong>
- Create or identify an existing GitHub issue before beginning development work.
- Use one branch per issue. Try not to do everything at once, unless appropriate.
- Try to name issue branches using the issue number: `issue/#123`
- Keep each branch focused on the work described in its GitHub issue. Don't let the branch's scope creep.
- Try to use clear, descriptive commit messages that explain what changed. For example, `Updated Article List Block CSS` is more useful than `update`.
- Push changes to the issue branch you're working from, <strong>not directly to main</strong>.
- You can reference the issue number in commit messages using #<number>.
- Avoid long-lived development branches when possible. Branches should exist only for as long as the associated work is active.

### Pull Requests
- Once work is completed, you may open a Pull Request.
- Keep Pull Requests focused on the issue they address. Unrelated work should generally be handled in a separate issue and branch.
- Make sure your branch is up to date with the default branch when needed, especially before merging. 
- Resolve merge conflicts and verify the changes before requesting Review or completing another team member's Pull Request.
- Make sure your PR passes the automatic linter checks before requesting Review.
- You can use GitHub's closing syntax to automatically close out Issues: `Resolves #123` , `Closes #123`, `Fixes #123` will all automatically close as completed the tagged Issues once the Pull Request is merged
- After reviewing a pull request, the reviewer should delete Issue branches after they have been merged.
