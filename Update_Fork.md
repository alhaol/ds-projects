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
**Make sure that you're on your master branch:**
```sh
git checkout master
```

**Rewrite your master branch so that any commits of yours that aren't already in upstream/master are replayed on top of that other branch:**
```sh
git rebase upstream/master
```

