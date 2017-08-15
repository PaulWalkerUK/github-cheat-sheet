[![Creative Commons Licence](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)  
This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

# Table of Contents
* [Introduction](#introduction)
* [Create A New Repository](#create-a-new-repository)
* [Cloning A Repository](#cloning-a-repository)
* [Create A New Branch](#create-a-new-branch)
* [Seeing What's Changed](#seeing-whats-changed)
* [Stage A File Ready To Commit](#stage-a-file-ready-to-commit)
* [Commit a file](#commit-a-file)
* [Push a branch up to GitHub](#push-a-branch-up-to-github)
* [Delete A Branch](#delete-a-branch)
* [# Keeping Inline With Upstream](#keeping-inline-with-upstream)

# Introduction
This document will be an "aide memoir" of things that I learn/need to remember about how to use GitHub. Leading up to me creating this document, I found I kept looking up how to do the same things. This is my attempt at generating a cheat sheet for a relative "newbie" to GitHub.

I'm specifically using GitHub for open-source projects. There are some that I've contributed to, some that I've got under my own account, and one that I setup as an "organisation" (though I'm no longer involved).

# Create A New Repository
To create a new repository under your own account:

1. Log in to the GitHub website
2. From your user's [homepage](https://github.com/PaulWalkerUK) click on the [Repositories](https://github.com/PaulWalkerUK?tab=repositories) tab.
3. Click on the [New](https://github.com/new) button.
4. Fill in all the details on this page then click the Create Repository button

This will create a repository on the website. You need to [clone](#cloning-a-repository) it to your desktop before you can do much with it.

# Cloning A Repository
To get a copy of the repository from your account on the website to your desktop so you can work on it:
1. In the Git Shell  Powershell client, navigate to the the parent directory of where you want to clone into. E.g.:

```powershell
C:\> cd e:\Git
E:\Git>
```

2. Enter `git clone` followed by the URL on the repository's main page:

```powershell
E:\Git> git clone https://github.com/PaulWalkerUK/github-cheat-sheet.git
Cloning into 'github-cheat-sheet'...
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
Checking connectivity... done.
E:\Git>
```

3. You can now `cd` into the new directory:

```powershell
E:\Git> cd .\github-cheat-sheet
E:\Git\github-cheat-sheet [master]>
```

# Create A New Branch
It's always best to work on a dedicated branch for each piece of work. This is because after you submit a pull request on a branch, anything else that gets committed to that branch up until the pull request is merged will get included with that pull request. To create a new branch and switch to it:

```
E:\Git\github-cheat-sheet [master]> git checkout -b add-first-steps
Switched to a new branch 'add-first-steps'
E:\Git\github-cheat-sheet [add-first-steps]>
```

Notice the branch name is included in the prompt.

The logic here isn't very intuitive. It seems to be that `checkout` is used to switch branches and `-b` is used to create a *new* branch.

# Seeing what's changed

After making changes, the prompt will change:

```
E:\Git\github-cheat-sheet [add-first-steps +0 ~1 -0]>
```

To see which files have changed, use `git status`:

```
E:\Git\github-cheat-sheet [add-first-steps +0 ~1 -0]> git status
On branch add-first-steps
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

To see the *details* of what's changed, use `git diff`:

```
E:\Git\github-cheat-sheet [add-first-steps +0 ~1 -0]> git diff
diff --git a/README.md b/README.md
index 39404d9..aff977e 100644
--- a/README.md
+++ b/README.md
@@ -1,2 +1,62 @@
-# github-cheat-sheet
-Things I've learnt/need to remember about how to use GitHub
+[![Creative Commons Licence](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/+This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommon+
+# Table of Contents
...
```

# Stage a file ready to commit

Before a file can be committed, it must be *staged*. Do this with `git add`. To add all files, use `git add .`. Note `git status` now shows the files as 'staged':

```powershell
E:\Git\github-cheat-sheet [add-first-steps +0 ~1 -0]> git add .
E:\Git\github-cheat-sheet [add-first-steps +0 ~1 -0]> git status
On branch add-first-steps
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   README.md

E:\Git\github-cheat-sheet [add-first-steps +0 ~1 -0]>
```

# Commit a file

To commit a file, use `git commit`:

```powershell
E:\Git\github-cheat-sheet [add-first-steps +0 ~1 -0]> git commit
[add-first-steps f4bb875] test
 1 file changed, 62 insertions(+), 2 deletions(-)
 rewrite README.md (100%)
```

A text editor will appear for you to enter your commit message


# Push a branch up to GitHub

After committing locally, you need to push the branch to GitHub to see the 
changes on there. To do this, you do:

```powershell
E:\Git\github-cheat-sheet [add-first-steps]> git push
```

If the branch was created locally and doesn't exist on GitHub yet, you'll get an
error the first time you do this:

```powershell
E:\Git\github-cheat-sheet [add-first-steps]> git push
fatal: The current branch add-first-steps has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin add-first-steps
```
In this case, simply run the command it gives you:

```powershell
E:\Git\github-cheat-sheet [add-first-steps]> git push --set-upstream origin add-first-steps
Counting objects: 6, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (6/6), 2.40 KiB | 0 bytes/s, done.
Total 6 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
Branch add-first-steps set up to track remote branch add-first-steps from origin.
To https://github.com/PaulWalkerUK/github-cheat-sheet.git
 * [new branch]      add-first-steps -> add-first-steps
```

# Delete A Branch

After you've finished with a branch, you can delete it. You need to delete it 
locally and on GitHub.

To delete it locally:

```powershell
E:\Git\7zBackup [master ≡]> git branch -d bring-up-to-date
Deleted branch bring-up-to-date (was 1ccb22f).
```

To then delete it remotely:

```powershell
E:\Git\7zBackup [master ≡]> git push origin --delete bring-up-to-date
To https://github.com/PaulWalkerUK/7zBackup.git
 - [deleted]         bring-up-to-date
```

# Keeping Inline With Upstream

We need to keep our fork in sync with changes made to the original, the 
"upstream". Firstly, check to see if `upstream` has been set:

```powershell
E:\Git\7zBackup [master ≡]> git remote -v
Isiweb  https://github.com/Isiweb/7zBackup.git (fetch)
Isiweb  https://github.com/Isiweb/7zBackup.git (push)
origin  https://github.com/PaulWalkerUK/7zBackup.git (fetch)
origin  https://github.com/PaulWalkerUK/7zBackup.git (push)
```

WE can see here, it hasn't, so we need to set it:

```powershell
E:\Git\7zBackup [master ≡]> git remote add upstream https://github.com/Isiweb/7zBackup
```

Now, if we check again:

```powershell
E:\Git\7zBackup [master ≡]> git remote -v
Isiweb  https://github.com/Isiweb/7zBackup.git (fetch)
Isiweb  https://github.com/Isiweb/7zBackup.git (push)
origin  https://github.com/PaulWalkerUK/7zBackup.git (fetch)
origin  https://github.com/PaulWalkerUK/7zBackup.git (push)
upstream        https://github.com/Isiweb/7zBackup (fetch)
upstream        https://github.com/Isiweb/7zBackup (push)
```

To update from upstream, we need to `fetch` then `merge`. To get that back up to 
GitHub, we then `push` it:

```powershell
E:\Git\7zBackup [master ≡]> git fetch upstream
From https://github.com/Isiweb/7zBackup
 * [new branch]      master     -> upstream/master
E:\Git\7zBackup [master ≡]> git checkout master
Your branch is up-to-date with 'origin/master'.
Already on 'master'
E:\Git\7zBackup [master ≡]> git merge upstream/master
Updating 2c7da64..e2de313
Fast-forward
 7zBackup-vars.ps1 |   2 +-
 7zBackup.ps1      | 195 +++++++++++++++++++++++++++++++++++++-----------------
 2 files changed, 137 insertions(+), 60 deletions(-)
E:\Git\7zBackup [master ↑2]> git push
Counting objects: 7, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (7/7), done.
Writing objects: 100% (7/7), 3.46 KiB | 0 bytes/s, done.
Total 7 (delta 4), reused 0 (delta 0)
remote: Resolving deltas: 100% (4/4), completed with 3 local objects.
To https://github.com/PaulWalkerUK/7zBackup.git
   2c7da64..e2de313  master -> master
```