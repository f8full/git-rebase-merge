## git rebase via merge ##

Have you ever rebased a branch resolving many conflicts on multiple commits?  
Yes, that's a sad story.  
It wouldn't be so sad, if it was a merge instead, because with a merge 
we have to fix only final conflicts in just one step.

## Method ##

So here is an idea on how to make a potentially hard rebase easier:
1. Start a hidden merge
2. Resolve conflicts and save hidden merge result
3. Perform a standard branch rebase, but with automatic conflict resolution
4. Restore hidden result as single additional commit

This script implements this approach as simple dialog and applicable on Linux / Mac / Windows (git-bash).

## Setup ##

First, we have to make this script run as a new custom git command

To do this, we must add the directory where the script file "git-rebase-merge" is to your PATH environment variable.

Next, we have to checkout the branch we want to do the rebase on.

```bash
git checkout feature/my-kawaii-feature-i-want-to-rebase
```

On the script file, the default base branch that the rebase will be based on is named "origin/master".
This can be changed by editing line 9 of the "git-rebase-merge" bash script file.

```bash
default_base_branch='origin/master'
```

## Usage ##

Every time you want to do rebase, just run

```bash
git rebase-merge
```

instead of

```bash
git rebase origin/master
```

## Notes ##

If you want to test this script, just run it on temp branch

```bash
git checkout -b test-of-rebase-via-merge
```

Also you can specify base branch like this:

```bash
git rebase-merge origin/develop
```