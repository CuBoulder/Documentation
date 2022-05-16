# Git Workflow
[Quick Visualization](https://docs.google.com/a/colorado.edu/drawings/d/1RAm8Xrvke9r-N1uMoWq_18XQBFo4fhVZ_lPw7t4k0w0/edit?usp=sharing)

## Permanent Branches

- **Main**
  - Deployed manually to PROD. Commits to this branch are tagged releases. Named master. Tags are in the pattern x.y.z.
- **Dev**
  - Deployed periodically to DEV. Named dev.

## Temporary Branches

- **Release**
  - Deployed manually to TEST. Branched from dev. Named in the pattern release/[x.y.z].
- **Hotfix**
  - Deployed manually to TEST. Branched from main. Named in the pattern hotfix/[issue-key] (issue-key is like FIT-1234).
- **Feature**
  - Not deployed. Branched from dev. Named in the pattern feature/[issue-key].
- **Bug**
  - Not deployed. Branched from release-[x.y.z]. Named in the pattern bug/[issue-key].

## Commands

### **Start a Feature**

```bash
cd [path/to/git/repo]
git fetch --all
git checkout -b feature/[issue-key] dev
git push --set-upstream origin feature/[issue-key]
```

### **Start a Bug**

```bash
cd [path/to/git/repo]
git fetch --all
git checkout -b bug/[issue-key] release/[version.to.release]
git push --set-upstream origin bug/[issue-key]
```

### **Start a Hotfix**

```bash
cd [path/to/git/repo]
git fetch --all
git checkout -b hotfix/[issue-key] [tag.for.last-release]
git push --set-upstream origin hotfix/[issue-key]
```

### **Start a Release**

```bash
cd [path/to/git/repo]
git checkout dev
git pull
git checkout -b release/[version.to.release] dev
git push --set-upstream origin release/[version.to.release]
```

### **Merge a Feature**

```bash
cd [path/to/git/repo]
git fetch
git checkout dev
git pull
git merge --no-ff feature/[issue-key] # Same as merging Github Pull Request
git push origin dev
```

### **Merge a Bug**

```bash
cd [path/to/git/repo]
git checkout release/[version.to.release]
git pull
git merge --no-ff bug/[issue-key] # Same as merging Github Pull Request
git push origin release/[version.to.release]
git checkout dev
git pull
git merge --no-ff bug/[issue-key]  # Same as merging Github Pull Request
git push origin dev
```

### **Merge a Hotfix**

```bash
cd [path/to/git/repo]
git checkout main
git pull
git merge --no-ff hotfix/[issue-key] # Same as merging Github Pull Request
git tag -a [version.to.release]
git push origin main
git push origin --tags
git checkout dev
git pull
git merge --no-ff hotfix/[issue-key]  # Same as merging Github Pull Request
git push origin dev
```

### **Finalize a Release**

```bash
cd [path/to/git/repo]
git checkout main
git pull
git merge --no-ff release/[version.to.release]  # Same as merging Github Pull Request
git tag -a v[version.to.release] -m "release [version.to.release] added"
git push origin --tags
git checkout dev
git pull
git merge --no-ff release/[version.to.release]  # Same as merging Github Pull Request
git push origin dev
```

## Rules of thumb for "Should I merge this?"

- main does not get merged into any other branch.
- Hotfix branches merge into main and dev only.
- Bug branches merge into release and dev only.
- Feature branches merge into dev only.
- dev can be merged into feature branches.

## Reading and Source material

- <http://jeffkreeftmeijer.com/2010/why-arent-you-using-git-flow>
- <https://gist.github.com/JamesMGreene/cdd0ac49f90c987e45ac>
