# How do I update a my GitHub forked repository from the master version?
> In your local clone of your forked repository (ds-projects), you can add the original GitHub repository (https://github.com/alhaol/ds-projects.git) as a "remote".
Then you can **fetch** all the branches from that upstream repository, and **rebase** your work to continue working on the upstream version. In terms of commands that might look like:
> 
**Add the remote, call it "upstream"**
```sh
git remote add upstream https://github.com/alhaol/ds-projects.git
```
**Fetch all the branches of that remote into remote-tracking branches**
```sh
git fetch upstream
```
**Make sure that you're on your master branch (master or main > Check your branches names):**
```sh
git checkout main
```

**Rewrite your master branch so that any commits of yours that aren't already in upstream/master are replayed on top of that other branch:**
```sh
git rebase upstream/master
```

**If you've rebased your branch onto upstream/master you may need to force the push in order to push it to your own forked repository on GitHub. You'd do that with:**

```sh
git push -f origin
```

# More details

##The Setup

Before you can sync, you need to add a remote that points to the upstream repository. You may have done this when you originally forked.
Tip: Syncing your fork only updates your local copy of the repository; it does not update your repository on GitHub.


```sh
$ git remote -v
# List the current remotes
origin  https://github.com/user/repo.git (fetch)
origin  https://github.com/user/repo.git (push)

$ git remote add upstream https://github.com/otheruser/repo.git
# Set a new remote

$ git remote -v
# Verify new remote
origin    https://github.com/user/repo.git (fetch)
origin    https://github.com/user/repo.git (push)
upstream  https://github.com/otheruser/repo.git (fetch)
upstream  https://github.com/otheruser/repo.git (push)

```
##Syncing

There are two steps required to sync your repository with the upstream: first you must fetch from the remote, then you must merge the desired branch into your local branch.

```sh
$ git fetch upstream
# Grab the upstream remote's branches
remote: Counting objects: 75, done.
remote: Compressing objects: 100% (53/53), done.
remote: Total 62 (delta 27), reused 44 (delta 9)
Unpacking objects: 100% (62/62), done.
From https://github.com/otheruser/repo
 * [new branch]      master     -> upstream/master

```
We now have the upstream's master branch stored in a local branch, upstream/master

```sh
$ git branch -va
# List all local and remote-tracking branches
* master                  a422352 My local commit
  remotes/origin/HEAD     -> origin/master
  remotes/origin/master   a422352 My local commit
  remotes/upstream/master 5fdff0f Some upstream commit
```

##Merging

Now that we have fetched the upstream repository, we want to merge its changes into our local branch. This will bring that branch into sync with the upstream, without losing our local changes.

```sh
$ git checkout master
# Check out our local master branch
Switched to branch 'master'
```
```sh
$ git merge upstream/master
# Merge upstream's master into our own
Updating a422352..5fdff0f
Fast-forward
 README                    |    9 -------
 README.md                 |    7 ++++++
 2 files changed, 7 insertions(+), 9 deletions(-)
 delete mode 100644 README
 create mode 100644 README.md
```
If your local branch didn't have any unique commits, git will instead perform a "fast-forward":

```sh
$ git merge upstream/master
Updating 34e91da..16c56ad
Fast-forward
 README.md                 |    5 +++--
 1 file changed, 3 insertions(+), 2 deletions(-)
 ```
 
 If you want to update your repository on GitHub, follow the instructions on 
 https://docs.github.com/en/free-pro-team@latest/github/using-git/pushing-commits-to-a-remote-repository#pushing-a-branch
