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

```none
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

```bash
echo "Hello World!" > HelloWorld.txt
git status
```

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

```none
[master 0fc8620] Add HelloWorld.txt
 1 file changed, 1 insertion(+)
 create mode 100644 HelloWorld.txt
```

```bash
git status
```

```none
On branch master
nothing to commit, working tree clean
```

```bash
echo "Hello World!" > HelloWorld.txt
git add HelloWorld.txt
git commit -m "Add HelloWorld.txt"
```

## What is a Commit


## Empty first commit

* Personal preference
* Allows for rolling back to a completely empty folder

```bash
cd ..
mkdir EmptyStart
cd EmptyStart
```

```bash
git init
git commit --allow-empty -m "In the beginning there was nothing"
```


