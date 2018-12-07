# Git Workshop

## What Is Git

* Linus Torvalds
* Version-Control System
* Used for SCM (Source-Control Management)
* Distributed
* "File System"

## Creating a New Repository

```bash
mkdir 20181213_GitWorkshop
cd 20181213_GitWorkshop
```

```bash
mkdir MyRepo
cd MyRepo
git init
```

Result:

```none
Initialized empty Git repository in C:/20181213_GitWorkshop/MyRepo/.git/
```

## Create a File and add it to the Repository

* Show the current repo status
* Create a file `HelloWorld.txt`
* Set the file contents to `Hello World!`
* Show the repo status
* Add the file to the Index
* Show the repo status
* Commit the file to the local repo
* Show the repo status
* Show repo log

```bash
git status
```

Result:

```none
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

```bash
echo "Hello World!" > HelloWorld.txt
git status
```

Result:

```none
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        HelloWorld.txt

nothing added to commit but untracked files present (use "git add" to track)
```

```bash
git add HelloWorld.txt
git status
```

Result:

```none
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   HelloWorld.txt
```

```bash
git commit -m "Add HelloWorld.txt"
```

Result:

```none
[master 0fc8620] Add HelloWorld.txt
 1 file changed, 1 insertion(+)
 create mode 100644 HelloWorld.txt
```

```bash
git status
```

Result:

```none
On branch master
nothing to commit, working tree clean
```

```bash
echo "Hello World 2!" > HelloWorld2.txt
git add HelloWorld2.txt
git commit -m "Add HelloWorld2.txt"
```

Result:

```none
[master a9f956a] Add HelloWorld2.txt
 1 file changed, 1 insertion(+)
 create mode 100644 HelloWorld2.txt
```

## Workspace, Index, Local Repository

* Workspace - The visible files tracked, untracked, and .git
* Index - Staging for changes .git/index
* Local Repository (Object Store) - The local git database .git/objects

![Git Operations](./images/GitOperations.png)

* Make changes in the workspace
* Stage (git add) changes in the Index
* Commit (git commit) changes to the Local Repository

## Viewing Commit History

```bash
git rev-list --all
```

Result:

```none
a9f956afcae5ba1b442fa4834c4912ac7659ca5f
af4eeb918df3f071e2769b4e7d94b8b744ead854
```

```bash
git rev-list --all --pretty
```

Result:

```none
commit a9f956afcae5ba1b442fa4834c4912ac7659ca5f
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:08:20 2018 -0800

    Add HelloWorld2.txt

commit af4eeb918df3f071e2769b4e7d94b8b744ead854
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:07:45 2018 -0800

    Add HelloWorld.txt
```

```bash
git log
```

Result:

```none
commit a9f956afcae5ba1b442fa4834c4912ac7659ca5f (HEAD -> master)
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:08:20 2018 -0800

    Add HelloWorld2.txt

commit af4eeb918df3f071e2769b4e7d94b8b744ead854
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:07:45 2018 -0800

    Add HelloWorld.txt
```

## Revert a Commit

```bash
echo 'Fail' > Fail.txt
git add Fail.txt
git commit -m 'Bad Commit'
git rev-list --all --pretty
```

Result

```none
[master e1d4a93] Bad Commit
 1 file changed, 1 insertion(+)
 create mode 100644 Fail.txt

commit e1d4a934146df81b969576e0a927d6b87ee4a497
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:50:08 2018 -0800

    Bad Commit

commit a9f956afcae5ba1b442fa4834c4912ac7659ca5f
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:08:20 2018 -0800

    Add HelloWorld2.txt

commit af4eeb918df3f071e2769b4e7d94b8b744ead854
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:07:45 2018 -0800

    Add HelloWorld.txt
```

```bash
git revert e1d4a934146df81b969576e0a927d6b87ee4a497 --no-edit
git rev-list --all --pretty
```

Result:

```none
[master f0b59b5] Revert "Bad Commit"
 1 file changed, 1 deletion(-)
 delete mode 100644 Fail.txt

commit f0b59b50bdd96f54d274fd99d40143d60bc1122c
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:55:35 2018 -0800

    Revert "Bad Commit"

    This reverts commit e1d4a934146df81b969576e0a927d6b87ee4a497.

commit e1d4a934146df81b969576e0a927d6b87ee4a497
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:50:08 2018 -0800

    Bad Commit

commit a9f956afcae5ba1b442fa4834c4912ac7659ca5f
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:08:20 2018 -0800

    Add HelloWorld2.txt

commit af4eeb918df3f071e2769b4e7d94b8b744ead854
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:07:45 2018 -0800

    Add HelloWorld.txt
```

## Reset to a commit

```bash
git reset --soft e1d4a934146df81b969576e0a927d6b87ee4a497
git status
git rev-list --all --pretty
```

Result:

```none
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        deleted:    Fail.txt

commit e1d4a934146df81b969576e0a927d6b87ee4a497
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:50:08 2018 -0800

    Bad Commit

commit a9f956afcae5ba1b442fa4834c4912ac7659ca5f
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:08:20 2018 -0800

    Add HelloWorld2.txt

commit af4eeb918df3f071e2769b4e7d94b8b744ead854
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:07:45 2018 -0800

    Add HelloWorld.txt
```

```bash
git reset --hard a9f956afcae5ba1b442fa4834c4912ac7659ca5f
git rev-list --all --pretty
```

Result:

```none
HEAD is now at a9f956a Add HelloWorld2.txt

commit a9f956afcae5ba1b442fa4834c4912ac7659ca5f
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:08:20 2018 -0800

    Add HelloWorld2.txt

commit af4eeb918df3f071e2769b4e7d94b8b744ead854
Author: Mark Kraus <mkraus@linkedin.biz>
Date:   Thu Dec 6 10:07:45 2018 -0800

    Add HelloWorld.txt
```

## Revert vs Reset

* Revert undoes a previous commit as a new commit
* Revert is similar to manually making the changes and creating a new commit
* Revert is non-destructive

* Reset moves back to specific commit
* Reset is similar to wiping the history
* Reset is destructive

## What a Commit Is

* Point-in-time snapshot of the files
* Identified by a sha1 hash
* Hash made from commit metadata (Message, author, time, etc) and the files

![Git Commit](./images/Commit.png)

## Branches: Create, Checkout, Update, Delete

* Create a new branch
* Checkout a new branch
* Switch between branches
* Create a new branch in one command
* List branches
* Update a branch
* Delete branches

### Create a new branch named new branch

```bash
git branch newbranch
git checkout newbranch
```

Result:

```none
Switched to branch 'newbranch'
```

switch back to master

```bash
git checkout master
```

Result:

```none
Switched to branch 'master'
```

### Create a branch and checkout in one command

```bash
git checkout -b newbranch2
```

Result:

```none
Switched to a new branch 'newbranch2'
```

### List branches

```bash
git branch -v
```

Result:

```none
  master     a9f956a Add HelloWorld2.txt
  newbranch  a9f956a Add HelloWorld2.txt
* newbranch2 a9f956a Add HelloWorld2.txt
```

### Update a branch

Add a HelloPlanet.txt file in newbranch2

```bash
echo "Hello Planet!" > HelloPlanet.txt
git add HelloPlanet.txt
git commit -m "Add HelloPlanet.txt"
```

Result:

```none
[newbranch2 ac33cae] Add HelloPlanet.txt
 1 file changed, 1 insertion(+)
 create mode 100644 HelloPlanet.txt
```

```bash
git branch -v
ls
```

Result:

```none
  master     a9f956a Add HelloWorld2.txt
  newbranch  a9f956a Add HelloWorld2.txt
* newbranch2 ac33cae Add HelloPlanet.txt

HelloPlanet.txt  HelloWorld.txt  HelloWorld2.txt
```

checkout newbranch and list contents

```bash
git checkout newbranch
git branch -v
ls
```

Result:

```none
Switched to branch 'newbranch'

  master     a9f956a Add HelloWorld2.txt
* newbranch  a9f956a Add HelloWorld2.txt
  newbranch2 ac33cae Add HelloPlanet.txt

HelloWorld.txt  HelloWorld2.txt
```

switch back to newbranch2 and list

```bash
git checkout newbranch2
git branch -v
ls
```

Result:

```none
Switched to branch 'newbranch2'

  master     a9f956a Add HelloWorld2.txt
  newbranch  a9f956a Add HelloWorld2.txt
* newbranch2 ac33cae Add HelloPlanet.txt

HelloPlanet.txt  HelloWorld.txt  HelloWorld2.txt
```

```bash
git checkout master
git branch -v
ls
```

Result:

```none
Switched to branch 'master'

* master     a9f956a Add HelloWorld2.txt
  newbranch  a9f956a Add HelloWorld2.txt
  newbranch2 ac33cae Add HelloPlanet.txt

HelloWorld.txt  HelloWorld2.txt
```

### Delete a branch

Delete the newbranch branch

```bash
git branch -v
git branch -d newbranch
git branch -v
```

Result:

```none
* master     a9f956a Add HelloWorld2.txt
  newbranch  a9f956a Add HelloWorld2.txt
  newbranch2 ac33cae Add HelloPlanet.txt

Deleted branch newbranch (was e134966).

* master     a9f956a Add HelloWorld2.txt
  newbranch2 ac33cae Add HelloPlanet.txt
```

Try to delete the newbranch2 branch

```bash
git branch -d newbranch2
```

Result:

```none
error: The branch 'newbranch2' is not fully merged.
If you are sure you want to delete it, run 'git branch -D newbranch2'.
```

Force delete the branch

```bash
git branch -D newbranch2
```

Result:

```none
Deleted branch newbranch2 (was ac33cae).
```

## What is a branch

* A way to work on the same things in parallel
* Changes in one branch do not effect changes in another
* In really, is just a logical pointer to a commit

![Branching](./images/branching.png)

## Creating a Remote Repo

```bash
cd ..
mkdir MyRemoteRepo
cd MyRemoteRepo
git init
```

Result:

```none
Initialized empty Git repository in C:/20181213_GitWorkshop/MyRemoteRepo/.git/
```

## Adding and Syncing Remote Repo

```bash
cd ..
cd MyRepo
git remote add origin ../MyRemote
```