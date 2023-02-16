# git rebase via merge #

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

Add the directory where the script file "git-rebase-merge" is to your PATH environment variable.

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


# git commit-feature #

When you've completed your work on a repository for a feature or bug or other, it's time to commit your code into a stemming branch from main/master and prepare your pull request. This usually takes a few steps but with this command, it can be done in a single statement.

## Method ##

1. The script makes sure that you are currently on master or main and that you are up to date with remote origin.
2. The script will create and checkout a branch with a specified name.
3. The script will stage all amd commit to the branch with a specified commit message.
4. Optionally, the script will also push your branch to origin.

## Setup ##

Add the directory where the script file "git-commit-feature" is to your PATH environment variable.
Make sure you are on the main/master branch and that you are up to date with origin.
Make sure that all your current changes are the ones you want and final.

## Usage ##

Run:
```bash
git commit-feature -b feature/my-kawaii-feature-branch -m "My kawaii commit message"
```

## Notes ##

Named arguments can also be used with the script as so:
```bash
git commit-feature --branch feature/my-kawaii-feature-branch --message "My kawaii commit message"
```

If you want to immediately push your branch to origin once this is done, add the -f or --force-push parameter to the command:
```bash
git commit-feature --branch feature/my-kawaii-feature-branch --message "My kawaii commit message -f"
```


# git redo-commit #

You've issued your pull request and you have changes to make to get the approval? Instead of adding a commit and pushing it, use this script to redo the commit so you can keep all your changes in a single commit.

## Method ##

1. The script will reset a your branch a certain number of commits. By default, 1. Specify another number using the -n or --number parameter.
2. The script will stage and commit all your changes, with the same commit message as the latest commit in the original branch.
4. Optionally, the script will also push your branch to origin.

## Setup ##

Add the directory where the script file "git-redo-commit" is to your PATH environment variable.
Make sure you are on the branch where you want to redo the commit.
Make sure that all your current changes are the ones you want and final.

## Usage ##

Run:
```bash
git redo-commit
```

## Notes ##

To redo many commits into one commit, use the -n or --number parameter to specify how many commits should be reset.
To force push your branch to remote at the end of the operation, use the -f or --force-push parameter.

To reset two commits and push to origin:
```bash
git redo-commit -n 2 -f
```
