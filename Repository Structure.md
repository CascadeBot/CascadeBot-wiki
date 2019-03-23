Cascade Bot's repository structure is heavily based off of the [git-flow system](https://nvie.com/posts/a-successful-git-branching-model/).

## Branches

- [master](#master-branch)
- [dev](#development-branch)
- [feature/x](#feature-branches)
- [patch/x](#patch-branches)
- [release/x](#release-branches)
- [hotfix/x](#hotfix-branches)

-------

### Master Branch
This branch holds the latest production version of the bot. The production bot will be updated off of this branch exclusively. If any issues arise that need immediate attention, a [hotfix branch](#hotfix-branches) is created to address these issues.

### Development Branch
This branch is where all the non-production work for the bot happens. All other branches other than hotfix branches are to be based off and merged back into this branch. All Pull Requests need to be up to date with this branch otherwise they will be denied.

**Merged into:**
 - Release
 - Master (**Only** while in Alpha/Beta Stage)

### Feature Branches
This type of branch is used to introduce a new feature/command into the bot's codebase. Only the feature intended for this branch should be included in the changes. 

The naming of this branch is `feature/x` where `x` is a short slug describing the feature.

**Based off:** Development

**Merged into:** Development

### Patch Branches
This type of branch is used to change one or more parts of the existing code. 

The naming of this branch is `patch/x` where `x` is a short slug describing the patch.

**Based off:** Development

**Merged into:** Development

### Release Branches
The release branches are forks of the [development branch](#development-branch) and are mainly used to prepare a release. This branch should **not** be used for new features; it should be used for bug-fixes and testing only. The branch name is formatted as `release/x` where `x` would be the expected version.

**Based off:**
- Development

**Merged into:**
- Master
- Development

### Hotfix branches
This type of branch is based directly off of the [master branch](#master-branch) and is used to create a fix for the production bot.

**Based off:** 
 - Master

**Merged into:**
 - Master
 - Development
