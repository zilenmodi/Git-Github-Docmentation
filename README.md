# Git-Github-Docmentation

## Git Basics

### **What is Version Control System?**

**Version Control System (VCS)** is a software that helps software developers to work together and maintain a complete history of their work.

Following are the types of VCS:

1. Centralized version control system (CVCS):
    - Store all files and enables team collaboration.
    - Drawback of CVCS is its single point of failure.
    - Disk of the central server gets corrupted and proper backup has not been taken, then you will lose the entire history of the project.
2. Distributed/Decentralized version control system (DVCS):
    - Latest snapshot of the directory but they also fully mirror the repository.
    - You can commit changes, create branches, view logs, and perform other operations when you are offline.

### **What is Git & It's Advantages?**

- Free and open source
- Fast and Small
- Implicit Backup
- Security
- Easier branching

## Git Objects

### What is Blob?

- BLOB stands for **Binary Large Object.**
- Each version of a file in Git is represented as a BLOB. A BLOB holds a file’s data but doesn’t contain any metadata about the file or even its name.
- **Example:**
    - Created new directory called practice.
        
        ```
        zilen@sf-cpu-438:~/Desktop$ mkdir practice
        zilen@sf-cpu-438:~/Desktop$ cd practice
        ```
        
    - Initialized practice.
        
        ```
        zilen@sf-cpu-438:~/Desktop/practice$ git init
        Initialized empty Git repository in /home/zilen/Desktop/practice/.git/
        ```
        
    - Remove hooks and see tree.
        
        ```
        zilen@sf-cpu-438:~/Desktop/practice$ rm -rf .git/hooks
        zilen@sf-cpu-438:~/Desktop/practice$ rm -rf .git/hooks
        ```
        
        Output:
        
        ```
        .git
        |-- HEAD
        |-- branches
        |-- config
        |-- description
        |-- info
        |   `-- exclude
        |-- objects
        |   |-- info
        |   `-- pack
        `-- refs
            |-- heads
            `-- tags
        
        8 directories, 4 files
        ```
        
    - Created three files: file1 - Hello, file2 - Hello and file3 - Hello World
    - Add to stage area. Whenever we are adding to stage area then blobs are created for each n every distinct file.
        
        ```
        zilen@sf-cpu-438:~/Desktop/practice$ touch file1
        zilen@sf-cpu-438:~/Desktop/practice$ touch file2
        zilen@sf-cpu-438:~/Desktop/practice$ touch file3
        zilen@sf-cpu-438:~/Desktop/practice$ git add .
        zilen@sf-cpu-438:~/Desktop/practice$ tree .git
        ```
        
        Output:
        
        ```
        zilen@sf-cpu-438:~/Desktop/practice$ cd .git
        zilen@sf-cpu-438:~/Desktop/practice/.git$ cd objects
        zilen@sf-cpu-438:~/Desktop/practice/.git/objects$ ls
        55  e9  info  pack
        ```
        
    - Add two empty file. It will add blobs for empty file also.
        
        ```
        zilen@sf-cpu-438:~/Desktop/practice$ touch file4
        zilen@sf-cpu-438:~/Desktop/practice$ touch file5
        zilen@sf-cpu-438:~/Desktop/practice$ git add .
        zilen@sf-cpu-438:~/Desktop/practice$ tree .git
        ```
        
        Output:
        
        ```
        .git
        |-- HEAD
        |-- branches
        |-- config
        |-- description
        |-- index
        |-- info
        |   `-- exclude
        |-- objects
        |   |-- 55
        |   |   `-- 7db03de997c86a4a028e1ebd3a1ceb225be238
        |   |-- e6
        |   |   `-- 9de29bb2d1d6434b8b29ae775ad8c2e48c5391
        |   |-- e9
        |   |   `-- 65047ad7c57865823c7d992b1d046ea66edf78
        |   |-- info
        |   `-- pack
        `-- refs
            |-- heads
            `-- tags
        
        11 directories, 8 files
        ```
        
    - If we change file3 to Hello World to Hello World! ,It will created new blob for that.
    - Whenever we commit things from staging area. It’s also generate commit object and tree object for current directory.
    - Commit → Tree → Blobs or Sub tree
        
        ```
        zilen@sf-cpu-438:~/Desktop/practice$ git commit -m "Created 5 files"
        [master (root-commit) 42d3b83] Created 5 files
         5 files changed, 3 insertions(+)
         create mode 100644 file1
         create mode 100644 file2
         create mode 100644 file3
         create mode 100644 file4
         create mode 100644 file5
        zilen@sf-cpu-438:~/Desktop/practice$ tree .git
        .git
        |-- COMMIT_EDITMSG
        |-- HEAD
        |-- branches
        |-- config
        |-- description
        |-- index
        |-- info
        |   `-- exclude
        |-- logs
        |   |-- HEAD
        |   `-- refs
        |       `-- heads
        |           `-- master
        |-- objects
        |   |-- 42
        |   |   `-- d3b834a171653024f36d8fa8b23250af063e9d
        |   |-- 55
        |   |   `-- 7db03de997c86a4a028e1ebd3a1ceb225be238
        |   |-- 98
        |   |   `-- 0a0d5f19a64b4b30a87d4206aade58726b60e3
        |   |-- a4
        |   |   `-- e69998746e849150e0dc640ab2f7fef200828d
        |   |-- e6
        |   |   `-- 9de29bb2d1d6434b8b29ae775ad8c2e48c5391
        |   |-- e9
        |   |   `-- 65047ad7c57865823c7d992b1d046ea66edf78
        |   |-- info
        |   `-- pack
        `-- refs
            |-- heads
            |   `-- master
            `-- tags
        
        17 directories, 15 files
        ```
        
    - Make new directory called Names and make file name1 in that with Zilen Modi.
        
        ```
        zilen@sf-cpu-438:~/Desktop/practice$ cd Names
        zilen@sf-cpu-438:~/Desktop/practice/Names$ touch name1
        zilen@sf-cpu-438:~/Desktop/practice/Names$ git add .
        zilen@sf-cpu-438:~/Desktop/practice/Names$ tree .git
        ```
        
    - Let us now verify the type of the files and its contents.
        
        ```
        zilen@sf-cpu-438:~/Desktop/practice$ git cat-file -t be2b
        tree
        zilen@sf-cpu-438:~/Desktop/practice$ git cat-file -p be2b
        040000 tree 79e78e7411892ba615ed7f2fcea1402b520c8c32	Names
        100644 blob e965047ad7c57865823c7d992b1d046ea66edf78	file1
        100644 blob e965047ad7c57865823c7d992b1d046ea66edf78	file2
        100644 blob 980a0d5f19a64b4b30a87d4206aade58726b60e3	file3
        100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391	file4
        100644 blob e69de29bb2d1d6434b8b29ae775ad8c2e48c5391	file5
        
        zilen@sf-cpu-438:~/Desktop/practice$ ls .git/objects/09
        85f4a5299c4ce8171f9a2445297b876021eef2
        zilen@sf-cpu-438:~/Desktop/practice$ git cat-file -t 0985
        blob
        zilen@sf-cpu-438:~/Desktop/practice$ git cat-file -p 0985
        ZIlen Modi
        zilen@sf-cpu-438:~/Desktop/practice$ git cat-file -t 42d3
        commit
        zilen@sf-cpu-438:~/Desktop/practice$ git cat-file -p 42d3
        tree a4e69998746e849150e0dc640ab2f7fef200828d
        author zilenmodi <zilen.m@simformsolutions.com> 1676352430 +0530
        committer zilenmodi <zilen.m@simformsolutions.com> 1676352430 +0530
        
        Created 5 files
        ```
        
    - See Head where pointing and current branch.
        
        ```
        zilen@sf-cpu-438:~/Desktop/practice$ ls .git/logs/refs/heads
        feature  master
        zilen@sf-cpu-438:~/Desktop/practice$ git checkout feature
        Switched to branch 'feature'
        zilen@sf-cpu-438:~/Desktop/practice$ cat .git/HEAD
        ref: refs/heads/feature
        ```
        

### **What is a tree?**

- A tree is like a directory. Each commit in Git points to a tree object, which in turn references the BLOBs. A tree object records the following.
    - BLOB identifiers.
    - Path names.
    - Metadata of all files in that directory.
    
## Git Configuration

### Git Configuration

- **Git config**
    
    Get and set configuration variables that control all facets of how Git looks and operates.
    
- **Set the name**
    
    `$ git config --global user.name "zilenmodi"`
    
- **Set the email**
    
    `$ git config --global user.email "zilen.m@simformsolutions.com"`
    

### **Starting a project**

- **Git initCreate a local repository**
    
    `$ git init`
    
- **Clone repository from url**
    
    `$ git clone url`
    

## Add, Commit and log

### Introduction to Add

- The git add command is used to add file contents to the Staging Area.
- This command updates the current content of the working tree to the staging area. It also prepares the staged content for the next commit.
- Add single file `git add <file-name>`
- Add all file `git add -a` or `git add .`
    
    ```
    zilen@sf-cpu-438:~/Desktop/practice$ touch file6
    zilen@sf-cpu-438:~/Desktop/practice$ git add file6
    zilen@sf-cpu-438:~/Desktop/practice$ git status
    On branch feature
    Changes to be committed:
      (use "git restore --staged <file>..." to unstage)
    	new file:   file6
    ```
    
- Delete file from stage area you have to delete from actual folder then use same command `git add <file-name>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/practice$ git status
    On branch feature
    Changes to be committed:
      (use "git restore --staged <file>..." to unstage)
    	new file:   file6
    
    Changes not staged for commit:
      (use "git add/rm <file>..." to update what will be committed)
      (use "git restore <file>..." to discard changes in working directory)
    	deleted:    file6
    
    zilen@sf-cpu-438:~/Desktop/practice$ git add file6
    zilen@sf-cpu-438:~/Desktop/practice$ git status
    On branch feature
    nothing to commit, working tree clean
    ```
    
- Reset or undo add operation `git reset <file-name>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/practice$ touch file6
    zilen@sf-cpu-438:~/Desktop/practice$ git add file6
    zilen@sf-cpu-438:~/Desktop/practice$ git status
    On branch feature
    Changes to be committed:
      (use "git restore --staged <file>..." to unstage)
    	new file:   file6
    
    zilen@sf-cpu-438:~/Desktop/practice$ git reset file6
    zilen@sf-cpu-438:~/Desktop/practice$ git status
    On branch feature
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    	file6
    
    nothing added to commit but untracked files present (use "git add" to track)
    ```
    

### Introduction to Commit

- It is used to record the changes in the repository. It is the next command after the git add.
- Every commit contains the index data and the commit message. Every commit forms a parent-child relationship.
- Commits are the snapshots of the project.
- `git commit -m “message”`
    
    ```
    zilen@sf-cpu-438:~/Desktop/practice$ git add file6
    zilen@sf-cpu-438:~/Desktop/practice$ git commit -m "added file6"
    [feature 48e2696] added file6
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 file6
    ```
    
- See all the commits `git log`
    
    ```
    zilen@sf-cpu-438:~/Desktop/practice$ git log
    commit 48e2696c7d8cd95c4af8e2a91409fa2e3d6a2dc9 (HEAD -> feature)
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 10:22:34 2023 +0530
    
        added file6
    
    commit fa3b2c25d067127f8eeff224ba6d8b8b084a3b19 (master)
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Tue Feb 14 11:30:53 2023 +0530
    
        Make names folder and file
    
    commit 42d3b834a171653024f36d8fa8b23250af063e9d
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Tue Feb 14 10:57:10 2023 +0530
    
        Created 5 files
    ```
    
- When we create new file and update one file then we have to commit direct then use `git commit -a` or `git commit -am “message”` Command to commit only modified file.
- New file still remain untracked.
    
    ```
    zilen@sf-cpu-438:~/Desktop/practice$ touch file7
    zilen@sf-cpu-438:~/Desktop/practice$ git status
    On branch feature
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git restore <file>..." to discard changes in working directory)
    	modified:   file6
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    	file7
    
    no changes added to commit (use "git add" and/or "git commit -a")
    
    zilen@sf-cpu-438:~/Desktop/practice$ git commit -a "file6 update"
    fatal: paths 'file6 update ...' with -a does not make sense
    
    zilen@sf-cpu-438:~/Desktop/practice$ git commit -am "Updated file6"
    [feature 9edab1a] Updated file6
     1 file changed, 1 insertion(+)
    
    zilen@sf-cpu-438:~/Desktop/practice$ git status
    On branch feature
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    	file7
    
    nothing added to commit but untracked files present (use "git add" to track)
    ```
    
- To update or change last commit message use `git commit -amend`
    
    ```
    zilen@sf-cpu-438:~/Desktop/practice$ git commit --amend  
    [feature 8f6cebb] Updated file6 - Commit message updated
     Date: Wed Feb 15 10:33:24 2023 +0530
     1 file changed, 1 insertion(+)
    
    zilen@sf-cpu-438:~/Desktop/practice$ git log
    commit 8f6cebb1870acfed79ae29b69366e4f17baed951 (HEAD -> feature)
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 10:33:24 2023 +0530
    
        Updated file6 - Commit message updated
    ```
    

### Introduction to Log

- Git log - Display the most recent commits and the status of the head.
    
    `git log`
    
    ```
    zilen@sf-cpu-438:~/Desktop/practice$ git log
    commit 8f6cebb1870acfed79ae29b69366e4f17baed951 (HEAD -> feature)
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 10:33:24 2023 +0530
    
        Updated file6 - Commit message updated
    
    commit 48e2696c7d8cd95c4af8e2a91409fa2e3d6a2dc9
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 10:22:34 2023 +0530
    
        added file6
    
    commit fa3b2c25d067127f8eeff224ba6d8b8b084a3b19 (master)
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Tue Feb 14 11:30:53 2023 +0530
    
        Make names folder and file
    
    commit 42d3b834a171653024f36d8fa8b23250af063e9d
    Author: zilenmodi <zilen.m@simformsolutions.com>
    ```
    
- Display the output as one commit per line - `git log —oneline`
    
    ```
    zilen@sf-cpu-438:~/Desktop/practice$ git log --oneline
    8f6cebb (HEAD -> feature) Updated file6 - Commit message updated
    48e2696 added file6
    fa3b2c2 (master) Make names folder and file
    42d3b83 Created 5 files
    ```
    
- Displays the files that have been modified - `git log --stat`
    
    ```
    zilen@sf-cpu-438:~/Desktop/practice$ git log --stat
    commit 8f6cebb1870acfed79ae29b69366e4f17baed951 (HEAD -> feature)
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 10:33:24 2023 +0530
    
        Updated file6 - Commit message updated
    
     file6 | 1 +
     1 file changed, 1 insertion(+)
    
    commit 48e2696c7d8cd95c4af8e2a91409fa2e3d6a2dc9
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 10:22:34 2023 +0530
    
        added file6
    
     file6 | 0
     1 file changed, 0 insertions(+), 0 deletions(-)
    ```
    
- Display the modified files with location - `git log -p`
    
    ```
    zilen@sf-cpu-438:~/Desktop/practice$ git log -p
    commit 8f6cebb1870acfed79ae29b69366e4f17baed951 (HEAD -> feature)
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 10:33:24 2023 +0530
    
        Updated file6 - Commit message updated
    
    diff --git a/file6 b/file6
    index e69de29..ffc38a8 100644
    --- a/file6
    +++ b/file6
    @@ -0,0 +1 @@
    +Zilen
    
    commit 48e2696c7d8cd95c4af8e2a91409fa2e3d6a2dc9
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 10:22:34 2023 +0530
    
        added file6
    
    diff --git a/file6 b/file6
    new file mode 100644
    index 0000000..e69de29
    
    commit fa3b2c25d067127f8eeff224ba6d8b8b084a3b19 (master)
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Tue Feb 14 11:30:53 2023 +0530
    
        Make names folder and file
    
    diff --git a/Names/name1 b/Names/name1
    new file mode 100644
    index 0000000..0985f4a
    --- /dev/null
    +++ b/Names/name1
    @@ -0,0 +1 @@
    +ZIlen Modi
    ```
    
## Working Area, Stashing

### Basics:

- There are mainly three part where git is divided: Working Area, Staging area and repository.
- Working area means we are working on folder locally.
- Staging area means we have use `git add` Command.
- When we add then modified file tracked and ready for next commit.
- Sometimes you want to switch the branches, but you are working on an incomplete part of your current project. You don't want to make a commit of half-done work.
- Git stashing allows you to do so. The **git stash command** enables you to switch branches without committing the current branch.
- Generally, the stash's meaning is "**store something safely in a hidden place**."
- Create xyz.txt and efg.txt files and then add to staging area.
    
    ```
    zilen@sf-cpu-438:~/Desktop/project$ touch xyz.txt
    zilen@sf-cpu-438:~/Desktop/project$ git add .
    zilen@sf-cpu-438:~/Desktop/project$ git status
    Changes to be committed:
      (use "git restore --staged <file>..." to unstage)
    	new file:   xyz.txt
    ```
    
    ```
    zilen@sf-cpu-438:~/Desktop/project$ touch efg.txt
    zilen@sf-cpu-438:~/Desktop/project$ git status
    Changes to be committed:
      (use "git restore --staged <file>..." to unstage)
    	new file:   xyz.txt
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
    	efg.txt
    ```
    
- Stashing xyz file using `git stash` or `git stash save “Message”`
    
    ```
    zilen@sf-cpu-438:~/Desktop/project$ git stash save "back stash xyz"
    Saved working directory and index state On newb: back stash xyz
    ```
    
- Check stash list using `git stash list`
    
    ```
    zilen@sf-cpu-438:~/Desktop/project$ git stash list
    stash@{0}: On newb: back stash xyz
    ```
    
- Add efg.txt to stage area and then back stage with previous command.
    
    ```
    zilen@sf-cpu-438:~/Desktop/project$ git add .
    zilen@sf-cpu-438:~/Desktop/project$ git stash save "back stash efg"
    Saved working directory and index state On newb: back stash efg
    zilen@sf-cpu-438:~/Desktop/project$ git stash list
    stash@{0}: On newb: back stash efg
    stash@{1}: On newb: back stash xyz
    ```
    
- `git stash apply` Command is used for taking last stash value from stashing area to staging area. It will remain in both area. Where `git stash pop` Command is used to pop last stash from stashing to staging area.
    
    ```
    zilen@sf-cpu-438:~/Desktop/project$ git stash pop
    On branch newb
    
    Changes to be committed:
      (use "git restore --staged <file>..." to unstage)
    	new file:   efg.txt
    
    Dropped refs/stash@{0} (26ca6e18409ac9523dbac5dd8adea4e8125c784b)
    
    zilen@sf-cpu-438:~/Desktop/project$ git stash list
    stash@{0}: On newb: back stash xyz
    ```
    
    ```
    zilen@sf-cpu-438:~/Desktop/project$ git stash apply
    On branch newb
    
    Changes to be committed:
      (use "git restore --staged <file>..." to unstage)
    	new file:   xyz.txt
    
    zilen@sf-cpu-438:~/Desktop/project$ git stash list
    stash@{0}: On newb: back stash xyz
    ```
    
- When there are multiple stash then you can use `git stash apply stash@{index}`
- To see what changes happend so used `git stash show`.
- To see details which things changed in file use partial stash. `git stash show -p`
- Delete most recent stash from queue used `git stash drop`
- Drop with stash index `git stash drop stash@{index}`
- Clear stash `git stash clear`
- Create new branch with all the things in stash. `git stash branch <name>`

## Difference

### Basics

- Track the changes that have not been staged - `git diff`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git diff
    diff --git a/README.md b/README.md
    index 29e1836..4b7719e 100644
    --- a/README.md
    +++ b/README.md
    @@ -235,3 +235,381 @@ Following are the types of VCS:
         - BLOB identifiers.
         - Path names.
         - Metadata of all files in that directory.
    +    ^M
    +## Git Configuration^M
    +^M
    +### Git Configuration^M
    +^M
    diff --git a/README.md b/README.md
    index 29e1836..4b7719e 100644
    --- a/README.md
    +++ b/README.md
    @@ -235,3 +235,381 @@ Following are the types of VCS:
         - BLOB identifiers.
         - Path names.
         - Metadata of all files in that directory.
    +    ^M
    +## Git Configuration^M
    +^M
    +### Git Configuration^M
    +^M
    +- **Git config**^M
    +    ^M
    +    Get and set configuration variables that control all facets of how Git looks and operates.^M
    ```
    
- Track the changes that have staged but not committed - `git diff --staged`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git add .
    zilen@sf-cpu-438:~/Desktop/notes$ git diff --staged
    diff --git a/README.md b/README.md
    index 29e1836..4b7719e 100644
    --- a/README.md
    +++ b/README.md
    @@ -235,3 +235,381 @@ Following are the types of VCS:
         - BLOB identifiers.
         - Path names.
         - Metadata of all files in that directory.
    +    ^M
    +## Git Configuration^M
    +^M
    +### Git Configuration^M
    +^M
    +- **Git config**^M
    +    ^M
    +    Get and set configuration variables that control all facets of how Git looks and operates.^M
    +    ^M
    +- **Set the name**^M
    +    ^M
    ```
    
- Git Diff Branches - `git diff <branch 2>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git diff master feature
    ```
- Track the changes between two commits - `git diff c1 c2`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git diff 974553a6c20e7416e34e4cf34b984727bf4e0eb9 3e39ef51fc1f84de8b605f3c78cc1935b34dab1e
    diff --git a/README.md b/README.md
    index 29e1836..c1657e1 100644
    --- a/README.md
    +++ b/README.md
    
    +    ^M
    +## Git Configuration^M
    +^M
    +### Git Configuration^M
    +^M
    +- **Git config**^M
    +    ^M
    +    Get and set configuration variables that control all facets of how Git looks and operates.^M
    +    ^M
    +- **Set the name**^M
    +    ^M
    +    `$ git config --global user.name "zilenmodi"`^M
    +    ^M
    +- **Set the email**^M
    +    ^M
    +    `$ git config --global user.email "zilen.m@simformsolutions.com"`^M
    +    ^M
    +^M
    +### **Starting a project**^M
    +^M
    +- **Git initCreate a local repository**^M
    +    ^M
    +    `$ git init`^M
    +    ^M
    +- **Clone repository from url**^M
    +    ^M
    +    `$ git clone url`^M
    ```
    
## Branching & Checkout

### Basics

- Create branch - `git branch <branch-name>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git branch f1
    zilen@sf-cpu-438:~/Desktop/notes$ git branch
      f1
      feature
    * master
    ```
    
- List all the branch - `git branch` or `git branch list`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git branch
      feature
    * master
    zilen@sf-cpu-438:~/Desktop/notes$ git branch --list
      feature
    * master
    ```
    
- List all branch along with remote - `git branch -a`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git branch -a
      feature
    * master
      remotes/origin/master
    ```
    
- Checkout branch - `git checkout <branch-name>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git checkout f1
    M	README.md
    Switched to branch 'f1'
    zilen@sf-cpu-438:~/Desktop/notes$ git branch
    * f1
      feature
      master
    ```
    
- Delete branch - `git branch -d <branch-name>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git branch -d f1
    Deleted branch f1 (was cdb408c).
    ```
    
- Create and switch to another branch - `git checkout -b <branch-name>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git checkout -b f2
    Switched to a new branch 'f2'
    zilen@sf-cpu-438:~/Desktop/notes$ git branch
    * f2
      feature
      master
    zilen@sf-cpu-438:~/Desktop/notes$ git add .
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m "first"
    [f2 208ceb8] first
     1 file changed, 1 insertion(+), 1 deletion(-)
    zilen@sf-cpu-438:~/Desktop/notes$ git push origin f2
    Username for 'https://github.com': zilenmodi
    Password for 'https://zilenmodi@github.com': 
    Enumerating objects: 5, done.
    Counting objects: 100% (5/5), done.
    Delta compression using up to 8 threads
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 278 bytes | 278.00 KiB/s, done.
    Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
    remote: Resolving deltas: 100% (1/1), completed with 1 local object.
    remote: 
    remote: Create a pull request for 'f2' on GitHub by visiting:
    remote:      https://github.com/zilenmodi/Git-Github-Docmentation/pull/new/f2
    remote: 
    To https://github.com/zilenmodi/Git-Github-Docmentation.git
     * [new branch]      f2 -> f2
    ```
    
- Delete remote branch - `git push origin -d <branch-name>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git push origin -d f2
    Username for 'https://github.com': zilenmodi
    Password for 'https://zilenmodi@github.com': 
    To https://github.com/zilenmodi/Git-Github-Docmentation.git
     - [deleted]         f2
    ```
    
## Merge

### Basics of merge

- There are two branches **master** and **feature.**
- We can see that we made some commits in both functionality and master branch, and merge them. It works as a pointer.
- It will find a common base commit between branches. Once Git finds a shared base commit, it will create a new "merge commit." It combines the changes of each queued merge commit sequence.
- To merge the specified commit to currently active branch - `git merge <commit-id>`
- To merge the specified branch to currently active branch - `git merge <branch-name>`
- **Fast Forward merge:** When f1 and f2 branch have same base point, then create 4 new file in f1 and do 4 commit for individual file created. then checkout f2 branch. f1,f2 → c1←c2←c3←c4  (head→f1).
- Apply `git merge f1` , So it will not created new commit and do fast forward merge so now f1 and f2 points at same base point of c4 commit.
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git merge f1
    Updating 208ceb8..e972ef1
    Fast-forward
     file1 | 0
     file2 | 0
     file3 | 0
     file4 | 0
     4 files changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 file1
     create mode 100644 file2
     create mode 100644 file3
     create mode 100644 file4
    zilen@sf-cpu-438:~/Desktop/notes$ git diff f1 f2
    ```
    
- To prevent fast forward merge then use `—no-ff`
- It’s prevent ff and create new commit like “merge f1 and f2”
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ touch file5
    zilen@sf-cpu-438:~/Desktop/notes$ git add .
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m "created file5"
    [f2 78c2398] created file5
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 file5
    
    zilen@sf-cpu-438:~/Desktop/notes$ touch file6
    zilen@sf-cpu-438:~/Desktop/notes$ git add .
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m "created file6"
    [f2 d730cb7] created file6
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 file6
    
    zilen@sf-cpu-438:~/Desktop/notes$ git checkout f1
    Switched to branch 'f1'
    
    zilen@sf-cpu-438:~/Desktop/notes$ git merge f2 --no-ff
    Merge made by the 'ort' strategy.
     file5 | 0
     file6 | 0
     2 files changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 file5
     create mode 100644 file6
    
    zilen@sf-cpu-438:~/Desktop/notes$ git show
    commit 45f8b39ce377db25590a0811e233e22224ace001 (HEAD -> f1)
    Merge: e972ef1 d730cb7
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 18:45:40 2023 +0530
    
        Merge branch 'f2' into f1
    ```
    
- Merge all commits then merge branch use `—squash`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git merge --squash f2
    Squash commit -- not updating HEAD
    ```
    
## Show, Head and Detached Head

### Basics

- The **HEAD** points out the last commit in the current checkout branch. It is like a pointer to any reference. The HEAD can be understood as the "**current branch**" When you switch branches with 'checkout,' the HEAD is transferred to the new branch.
- It stores the status of Head in **.git\refs\heads** directory.
- To see status of Head use - `git show` or `git show HEAD`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git show
    commit be406475f71e269d897cf8bfa4db7f1af8e8cbc9 (HEAD -> f1)
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 16:22:16 2023 +0530
    
        Added file1
    
    diff --git a/file1 b/file1
    new file mode 100644
    index 0000000..e69de29
    
    zilen@sf-cpu-438:~/Desktop/notes$ git show HEAD
    commit be406475f71e269d897cf8bfa4db7f1af8e8cbc9 (HEAD -> f1)
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 16:22:16 2023 +0530
    
        Added file1
    
    diff --git a/file1 b/file1
    new file mode 100644
    index 0000000..e69de29
    ```
    
- We can also checkout particular commit along with it’s id whuch known as **detached head status**.
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git checkout 9a13624e1d3ca9ad93a97d49726e735f2d919fe1
    Note: switching to '9a13624e1d3ca9ad93a97d49726e735f2d919fe1'.
    
    **You are in 'detached HEAD' state.** You can look around, make experimental
    changes and commit them, and you can discard any commits you make in this
    state without impacting any branches by switching back to a branch.
    
    HEAD is now at 9a13624 deleted file1
    ```
    
- When we do new commits with this head point and without pointing any branch and then move back to main branch, Then all commits became **dangling commits**.
- To overcome we can create new branch at that commit called temporary and then rebase with main branch.
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ touch file4
    zilen@sf-cpu-438:~/Desktop/notes$ git add .
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m "created file4"
    [detached HEAD e407fd1] created file4
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 file4
    ```
    
    **Before Detached head: checkout 9a13**
    
    ```
    **F1 pointing to be40**
    
    commit be406475f71e269d897cf8bfa4db7f1af8e8cbc9 (HEAD -> f1)
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 16:22:16 2023 +0530
    
        Added file1
    
    commit 9a13624e1d3ca9ad93a97d49726e735f2d919fe1
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 16:17:09 2023 +0530
    
        deleted file1
    ```
    
    **After Detached head:** Created new file4 and commit
    
    ```
    **Done commit on 9a13**
    
    commit e407fd14cc3a2c9704e5b252a6a681c7dff25050 (HEAD)
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 16:47:22 2023 +0530
    
        created file4
    
    commit 9a13624e1d3ca9ad93a97d49726e735f2d919fe1
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 16:17:09 2023 +0530
    
        deleted file1
    ```
    
    ****************************After rebase -**************************** `git rebase f1`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git rebase f1
    Successfully rebased and updated detached HEAD.
    
    zilen@sf-cpu-438:~/Desktop/notes$ git log
    commit e972ef10df0e36e805e0e59534c7cce15477c0f5 **(HEAD)**
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 16:47:22 2023 +0530
    
        created file4
    
    commit be406475f71e269d897cf8bfa4db7f1af8e8cbc9 **(f1)**
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 16:22:16 2023 +0530
    
        Added file1
    
    commit 9a13624e1d3ca9ad93a97d49726e735f2d919fe1
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 16:17:09 2023 +0530
    
        deleted file1
    ```
    
- Even now, Head and f1 not pointing to same, So for that we have to merge using temp branch.
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git status
    HEAD detached from 9a13624
    nothing to commit, working tree clean
    
    zilen@sf-cpu-438:~/Desktop/notes$ git branch tmp
    
    zilen@sf-cpu-438:~/Desktop/notes$ git checkout f1
    Previous HEAD position was e972ef1 created file4
    Switched to branch 'f1'
    
    zilen@sf-cpu-438:~/Desktop/notes$ **git rebase tmp**
    Successfully rebased and updated refs/heads/f1.
    
    zilen@sf-cpu-438:~/Desktop/notes$ git log
    commit e972ef10df0e36e805e0e59534c7cce15477c0f5 **(HEAD -> f1, tmp)**
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Wed Feb 15 16:47:22 2023 +0530
    
        created file4
    
    zilen@sf-cpu-438:~/Desktop/notes$ git branch -d tmp
    Deleted branch tmp (was e972ef1).
    ```
    
## Rebase

### Basics

- **Rebasing** is a process to reapply commits on top of another base trip. It is used to apply a sequence of commits from distinct branches into a final commit.
- It is an alternative of git merge command. It is a linear process of merging.
- Like, Do c1 and c2 commit on f3 then, Created new branch f4 and checkout same. then commit f1 and f2 on that bracnh.
- Move to f3 branch and do c3 and c4 commit.
- Then move to f4 branch and do rebase - `git rebase <branch-name>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git checkout f3
    Switched to branch 'f3'
    
    zilen@sf-cpu-438:~/Desktop/notes$ touch file.txt
    zilen@sf-cpu-438:~/Desktop/notes$ git add file.txt
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m **"c1"**
    [f3 3062c0b] c1
     1 file changed, 1 insertion(+)
     create mode 100644 file.txt
    
    zilen@sf-cpu-438:~/Desktop/notes$ git add file.txt
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m **"c2"**
    [f3 e49fe30] c2
     1 file changed, 1 insertion(+)
    
    zilen@sf-cpu-438:~/Desktop/notes$ git checkout -b f4
    Switched to a new branch 'f4'
    zilen@sf-cpu-438:~/Desktop/notes$ git diff f3 f4
    
    zilen@sf-cpu-438:~/Desktop/notes$ git add file.txt
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m **"f1"**
    [f4 5580812] f1
     1 file changed, 1 insertion(+)
    
    zilen@sf-cpu-438:~/Desktop/notes$ git add file.txt
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m **"f2"**
    [f4 40c86aa] f2
     1 file changed, 1 insertion(+)
    
    zilen@sf-cpu-438:~/Desktop/notes$ git checkout f3
    Switched to branch 'f3'
    
    zilen@sf-cpu-438:~/Desktop/notes$ git add file.txt
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m **"c3"**
    [f3 de1bd0d] c3
     1 file changed, 1 insertion(+)
    
    zilen@sf-cpu-438:~/Desktop/notes$ git add file.txt
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m **"c4"**
    [f3 33ea32e] c4
     1 file changed, 1 insertion(+)
    
    **zilen@sf-cpu-438:~/Desktop/notes$ git diff f3 f4
    diff --git a/file.txt b/file.txt
    index e649d90..3b73725 100644
    --- a/file.txt
    +++ b/file.txt
    @@ -1,4 +1,4 @@
     c1
     c2
    -c3
    -c4
    +f1
    +f2**
    
    zilen@sf-cpu-438:~/Desktop/notes$ git checkout f4
    Switched to branch 'f4'
    
    **zilen@sf-cpu-438:~/Desktop/notes$ git rebase f3
    Auto-merging file.txt
    CONFLICT (content): Merge conflict in file.txt**
    ```
    
- If there are some conflicts in the branch, resolve them, and perform below commands to continue changes -
    
    `git status`
    
    `git rebase —continue`
    
- The above command is used to continue with the changes you made. If you want to skip the change, you can skip as follows -
    
    `git rebase —skip`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git add file.txt
    zilen@sf-cpu-438:~/Desktop/notes$ git rebase --continue
    [detached HEAD 95b3209] f1
     1 file changed, 1 insertion(+)
    Successfully rebased and updated refs/heads/f4.
    
    zilen@sf-cpu-438:~/Desktop/notes$ git log --oneline
    2838537 (HEAD -> f4) f2
    95b3209 f1
    33ea32e (f3) c4
    de1bd0d c3
    e49fe30 c2
    3062c0b c1
    ```
    

![https://wac-cdn.atlassian.com/dam/jcr:c34c17d8-22fd-4df8-9ac6-474ae80bf0e0/02%20Usage.svg?cdnVersion=789](https://wac-cdn.atlassian.com/dam/jcr:c34c17d8-22fd-4df8-9ac6-474ae80bf0e0/02%20Usage.svg?cdnVersion=789)

![https://wac-cdn.atlassian.com/dam/jcr:4e576671-1b7f-43db-afb5-cf8db8df8e4a/01%20What%20is%20git%20rebase.svg?cdnVersion=789](https://wac-cdn.atlassian.com/dam/jcr:4e576671-1b7f-43db-afb5-cf8db8df8e4a/01%20What%20is%20git%20rebase.svg?cdnVersion=789)

- Merge commits, So use `git rebase -i <commit-id>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/notes$ git add file.txt
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m "c1"
    [f4 73a6d63] c1
     1 file changed, 1 insertion(+), 6 deletions(-)
    zilen@sf-cpu-438:~/Desktop/notes$ git add file.txt
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m "c2"
    [f4 7556dfb] c2
     1 file changed, 1 insertion(+)
    zilen@sf-cpu-438:~/Desktop/notes$ git add file.txt
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m "c3"
    [f4 1e37cb3] c3
     1 file changed, 1 insertion(+)
    zilen@sf-cpu-438:~/Desktop/notes$ git add file.txt
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m "c4"
    [f4 625ac3d] c4
     1 file changed, 1 insertion(+)
    zilen@sf-cpu-438:~/Desktop/notes$ git add file.txt
    zilen@sf-cpu-438:~/Desktop/notes$ git commit -m "c5"
    [f4 e1a7942] c5
     1 file changed, 1 insertion(+)
    
    zilen@sf-cpu-438:~/Desktop/notes$ git log --oneline
    e1a7942 (HEAD -> f4) c5
    625ac3d c4
    1e37cb3 c3
    7556dfb c2
    73a6d63 c1
    
    **zilen@sf-cpu-438:~/Desktop/notes$ git rebase -i 2838
    [detached HEAD 7f279b3] Merged c2,c3,c4
     Date: Thu Feb 16 11:24:15 2023 +0530
     1 file changed, 3 insertions(+)
    Successfully rebased and updated refs/heads/f4.**
    
    zilen@sf-cpu-438:~/Desktop/notes$ git log --oneline
    0748f68 (HEAD -> f4) c5
    7f279b3 Merged c2,c3,c4
    73a6d63 c1
    ```
    
## Push, Pull, Fetch and Remote

### Basics of fetch

- The "**git fetch**" **command** is used to pull the updates from remote-tracking branches. Additionally, we can get the updates that have been pushed to our remote branches to our local machines.
- We can fetch a specific branch from a repository - `git fetch url b-name`
    
    ```
    zilen@sf-cpu-438:~/Desktop/project$ git fetch origin master
    remote: Enumerating objects: 4, done.
    remote: Counting objects: 100% (4/4), done.
    remote: Compressing objects: 100% (2/2), done.
    remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (3/3), 720 bytes | 720.00 KiB/s, done.
    From https://github.com/zilenmodi/project1
     * branch            master     -> FETCH_HEAD
       6a294eb..e192d41  master     -> origin/master
    ```
    
- Then merge, `git merge`
    
    ```
    zilen@sf-cpu-438:~/Desktop/project$ git merge origin/master
    Merge made by the 'ort' strategy.
     hotel.txt | 1 +
     1 file changed, 1 insertion(+)
     create mode 100644 hotel.txt
    ```
    
- Fetch all the branches and objects - `git fetch`
    
    ```
    zilen@sf-cpu-438:~/Desktop/project$ git fetch
    remote: Enumerating objects: 12, done.
    remote: Counting objects: 100% (12/12), done.
    remote: Compressing objects: 100% (6/6), done.
    remote: Total 8 (delta 2), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (8/8), 1.93 KiB | 657.00 KiB/s, done.
    From https://github.com/zilenmodi/project1
       e192d41..b6e8075  master     -> origin/master
       36b1ee2..d4bdccc  feature1   -> origin/feature1
       45c1c65..86aac13  newb       -> origin/newb
    zilen@sf-cpu-438:~/Desktop/project$ git merge
    Merge made by the 'ort' strategy.
     hotel.txt | 2 +-
     1 file changed, 1 insertion(+), 1 deletion(-)
    zilen@sf-cpu-438:~/Desktop/project$ ls
    def.txt  git-practice  hotel.txt  name.txt  text.txt
    zilen@sf-cpu-438:~/Desktop/project$ cat hotel.txt
    Real Preparika
    ```
    

### Basics of Pull

- Pull request is a process for a developer to notify team members that they have completed a feature. Once their feature branch is ready, the developer files a pull request via their remote server account.
- Pull request announces all the team members that they need to review the code and merge it into the master branch.
    
    ![https://static.javatpoint.com/tutorial/git/images/git-pull.png](https://static.javatpoint.com/tutorial/git/images/git-pull.png)
    
- We can pull a remote repository by just using the git pull command - `git pull`
    
    ```
    zilen@sf-cpu-438:~/Desktop/project$ git pull
    remote: Enumerating objects: 10, done.
    remote: Counting objects: 100% (10/10), done.
    remote: Compressing objects: 100% (4/4), done.
    remote: Total 6 (delta 2), reused 0 (delta 0), pack-reused 0
    Unpacking objects: 100% (6/6), 1.24 KiB | 422.00 KiB/s, done.
    From https://github.com/zilenmodi/project1
       d4bdccc..46c6a02  feature1   -> origin/feature1
       86aac13..52785fc  newb       -> origin/newb
    There is no tracking information for the current branch.
    ```
    
- For specified branch - `git pull url <b-name>`

### Basics of push

- Push local repo to remote - `git push origin <b-name>`
- Upstream remote - `git push -u origin <b-name>`

<aside>
💡 git pull = git fetch + git merge

</aside>

| git fetch | git pull |
| --- | --- |
| Fetch downloads only new data from a remote repository. | Pull is used to update your current HEAD branch with the latest changes from the remote server. |
| Fetch is used to get a new view of all the things that happened in a remote repository. | Pull downloads new data and directly integrates it into your current working copy files. |
| Fetch never manipulates or spoils data. | Pull downloads the data and integrates it with the current working file. |
| It protects your code from merge conflict. | In git pull, there are more chances to create the merge conflict. |
| It is better to use git fetch command with git merge command on a pulled repository. | It is not an excellent choice to use git pull if you already pulled any repository. |

### Some extra:

- Check the configuration of the remote server - `git remote -v`
- Add a remote for the repository - `git remote add <url>`
- Remove a remote connection from the repository - `git remote rm`
- Change remote url - `git remote set-url <url>`


## Reset, Revert and Restore

### Basics of reset

- A mixed option is a default option of the git reset command. If we would not pass any argument, then the git reset command considered as **--mixed** as default option.
- A mixed option updates the ref pointers. The staging area also reset to the state of a specified commit. The undone changes transferred to the working directory. - `git reset —mixed <c-id>`
- The soft option does not touch the index file or working tree at all, but it resets the Head as all options do.
- When the soft mode runs, the refs pointers updated, and the resets stop there. It will act as git amend command. `git reset —soft <c-id>`
- Reset from all stage - `git reset —hard <c-id>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/project$ cd files
    zilen@sf-cpu-438:~/Desktop/project/files$ touch file1
    zilen@sf-cpu-438:~/Desktop/project/files$ touch file2
    zilen@sf-cpu-438:~/Desktop/project/files$ touch file3
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git add file1
    zilen@sf-cpu-438:~/Desktop/project/files$ git commit -m "added file1"
    [fmain 31ab1df] added file1
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 files/file1
    zilen@sf-cpu-438:~/Desktop/project/files$ git add file2
    zilen@sf-cpu-438:~/Desktop/project/files$ git commit -m "added file2"
    [fmain db2efaf] added file2
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 files/file2
    zilen@sf-cpu-438:~/Desktop/project/files$ git add file3
    zilen@sf-cpu-438:~/Desktop/project/files$ git commit -m "added file3"
    [fmain fc0191a] added file3
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 files/file3
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git log --oneline
    fc0191a (HEAD -> fmain) added file3
    db2efaf added file2
    31ab1df added file1
    ca067ab (feature1) Merge remote-tracking branch 'refs/remotes/origin/feature1' into feature1
    d4bdccc Create tech.txt
    8559da4 xyz
    36b1ee2 clang file again modified
    4d14a8a git-practice added
    9501ea1 modified clang
    9520234 Created clang.txt file
    4b879cf Stash Pop and create new file
    49e5034 Restore from last commit  text.txt file
    3918b6b Modified text.txt file
    9b6c33d Created text.txt file
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git log HEAD~3 --oneline
    ca067ab (feature1) Merge remote-tracking branch 'refs/remotes/origin/feature1' into feature1
    d4bdccc Create tech.txt
    8559da4 xyz
    36b1ee2 clang file again modified
    4d14a8a git-practice added
    9501ea1 modified clang
    9520234 Created clang.txt file
    4b879cf Stash Pop and create new file
    49e5034 Restore from last commit  text.txt file
    3918b6b Modified text.txt file
    9b6c33d Created text.txt file
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git reset --hard db2efaf
    HEAD is now at db2efaf added file2
    zilen@sf-cpu-438:~/Desktop/project/files$ git reset --mixed 31ab1df
    zilen@sf-cpu-438:~/Desktop/project/files$ git reset --soft ca067ab
    
    zilen@sf-cpu-438:~/Desktop/project/files$ ls
    file1  file2
    zilen@sf-cpu-438:~/Desktop/project/files$ git ls-files
    file1
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git log
    commit ca067abdb0fa348013b90576efe0e29939598f21 (HEAD -> fmain, feature1)
    Merge: 8559da4 d4bdccc
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Thu Feb 16 16:20:40 2023 +0530
    
        Merge remote-tracking branch 'refs/remotes/origin/feature1' into feature1
    ```
    

### Basics of Revert

- In Git, the term revert is used to revert some changes. The git revert command is used to apply revert operation. It is an undo type command. However, it is not a traditional undo alternative.
- git revert is a commit.
- Created 5 files and and make two modification in f1 and f2.
- Add Zilen to f1 and Modi to f2.
- Do 7 commits with suitable name.
    
    ```
    zilen@sf-cpu-438:~/Desktop/project/files$ git add file1
    zilen@sf-cpu-438:~/Desktop/project/files$ git commit -m "Modified f1"
    [dev d3f5320] Modified f1
     1 file changed, 1 insertion(+)
    zilen@sf-cpu-438:~/Desktop/project/files$ git add file2
    zilen@sf-cpu-438:~/Desktop/project/files$ git commit -m "Modified f2"
    [dev 6b4da92] Modified f2
     1 file changed, 1 insertion(+)
    zilen@sf-cpu-438:~/Desktop/project/files$ git log --oneline
    6b4da92 (HEAD -> dev) Modified f2
    d3f5320 Modified f1
    cad1235 Created f5
    995b7a8 Created f4
    fccedf5 Created f3
    dfe51f6 Created f2
    dfa9074 Created f1
    ```
    
- Then delete f1 and make commit for that.
    
    ```
    zilen@sf-cpu-438:~/Desktop/project/files$ rm -rf file1
    zilen@sf-cpu-438:~/Desktop/project/files$ git add .
    zilen@sf-cpu-438:~/Desktop/project/files$ git commit -m "deleted file1"
    [dev 1cb9686] deleted file1
     1 file changed, 1 deletion(-)
     delete mode 100644 files/file1
    ```
    
- Add new file f6 and commit.
    
    ```
    zilen@sf-cpu-438:~/Desktop/project/files$ touch file6
    zilen@sf-cpu-438:~/Desktop/project/files$ git add .
    zilen@sf-cpu-438:~/Desktop/project/files$ git commit -m "Created f6"
    [dev 142bab8] Created f6
     1 file changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 files/file6
    ```
    
- Current scenario
    
    ```
    zilen@sf-cpu-438:~/Desktop/project/files$ git log --oneline
    142bab8 (HEAD -> dev) Created f6
    1cb9686 deleted file1
    6b4da92 Modified f2
    d3f5320 Modified f1
    cad1235 Created f5
    995b7a8 Created f4
    fccedf5 Created f3
    dfe51f6 Created f2
    dfa9074 Created f1
    ```
    
- Now we thought that **1cb9686 deleted file1** have to undo, We want to undo commit so we can use revert and old commit remain in list.
    
    `git revert <c-id>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/project/files$ git revert -e 1cb9686
    [dev 8eaf1b2] Revert "deleted file1"
    1 file changed, 1 insertion(+)
    create mode 100644 files/file1
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git log --oneline
    8eaf1b2 (HEAD -> dev) Revert "deleted file1"
    142bab8 Created f6
    1cb9686 deleted file1
    6b4da92 Modified f2
    d3f5320 Modified f1
    ```
    
- Revert is also used to revert merge of two branchs.
    
    ```
    zilen@sf-cpu-438:~/Desktop/project/files$ git log --oneline --graph
    *   0f11fbb (HEAD -> dev) Merge branch 'fea' into dev
    |\  
    | * 2385564 (fea) edited f6
    |/  
    * 8eaf1b2 Revert "deleted file1"
    * 142bab8 Created f6
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git revert -e 0f11fbb -m 1
    [dev 9d05fd0] Revert "Merge branch 'fea' into dev"
     1 file changed, 10 deletions(-)
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git log --oneline --graph
    * 9d05fd0 (HEAD -> dev) Revert "Merge branch 'fea' into dev"
    *   0f11fbb Merge branch 'fea' into dev
    |\  
    | * 2385564 (fea) edited f6
    |/  
    * 8eaf1b2 Revert "deleted file1"
    * 142bab8 Created f6
    * 1cb9686 deleted file1
    ```
    
- Remove file from stage area - `git rm <file-name>`
- Remove from stage but not from local - `git rm —cached <file-name>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/project/files$ git rm --cached file5
    rm 'files/file5'
    zilen@sf-cpu-438:~/Desktop/project/files$ git ls-files
    file1
    file2
    file3
    file4
    zilen@sf-cpu-438:~/Desktop/project/files$ ls
    file1  file2  file3  file4  file5
    ```
    

### Basics of Restore

- Likewise, We have modified file 5 and add line → “Hiiii!!!”
- Then add into stage area using `git add file5`
- Now, We know that we have to write Heyyaaaaa!! instead of that.
- Then we again modified. So, now one is untracked and one is tracked. So, We have to restore from staged and then add new modified.
- Used to unstage - `git restore —staged <file-name>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/project/files$ git status
    On branch fea
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git restore <file>..." to discard changes in working directory)
    	modified:   file5
    
    no changes added to commit (use "git add" and/or "git commit -a")
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git add file5
    zilen@sf-cpu-438:~/Desktop/project/files$ git log -p
    commit e4177105ecb847cf6cbc5495bd9fe6690289000c (HEAD -> fea)
    Author: zilenmodi <zilen.m@simformsolutions.com>
    Date:   Fri Feb 17 13:28:14 2023 +0530
    
        changes f
    
    diff --git a/files/file5 b/files/file5
    index e69de29..fa3728e 100644
    --- a/files/file5
    +++ b/files/file5
    @@ -0,0 +1 @@
    +Hellooooo!!!
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git diff
    diff --git a/files/file5 b/files/file5
    index 2f0d940..d6ea221 100644
    --- a/files/file5
    +++ b/files/file5
    @@ -1,3 +1,3 @@
     Hellooooo!!!
     
    -Hiii!!
    +Heyyaaaaa!!
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git diff --staged
    diff --git a/files/file5 b/files/file5
    index fa3728e..2f0d940 100644
    --- a/files/file5
    +++ b/files/file5
    @@ -1 +1,3 @@
     Hellooooo!!!
    +
    +Hiii!!
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git status
    On branch fea
    
    Changes to be committed:
      (use "git restore --staged <file>..." to unstage)
    	modified:   file5
    
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git restore <file>..." to discard changes in working directory)
    	modified:   file5
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git restore --staged file5
    zilen@sf-cpu-438:~/Desktop/project/files$ git add file5
    zilen@sf-cpu-438:~/Desktop/project/files$ git diff --staged
    diff --git a/files/file5 b/files/file5
    index fa3728e..d6ea221 100644
    --- a/files/file5
    +++ b/files/file5
    @@ -1 +1,3 @@
     Hellooooo!!!
    +
    +Heyyaaaaa!!
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git commit -m "Restored and Modified"
    [fea dc32b0c] Restored and Modified
     1 file changed, 2 insertions(+)
    ```
    

### Basics of Cherry-pick

- Cherry-picking in Git stands for applying some commit from one branch into another branch.
- In case you made a mistake and committed a change into the wrong branch, but do not want to merge the whole branch.
- **You can revert the commit and apply it on another branch.**
- Cherry-pick is a useful tool, but always it is not a good option. It can cause duplicate commits and some other scenarios where other merges are preferred instead of cherry-picking.
- It is a useful tool for a few situations. It is in contrast with different ways such as **merge** and **rebase** command.
- **Use**
    - Scenerio1: Accidently make a commit in a wrong branch.
    - Scenario2: Made the changes proposes by another team member.
- Like we are in branch dev and make some changes and then commit. But If we want this commit in fea branch, So used `git cherry-pick <commit-id>`
    
    ```
    zilen@sf-cpu-438:~/Desktop/project/files$ git checkout dev
    Switched to branch 'dev'
    zilen@sf-cpu-438:~/Desktop/project/files$ git log --oneline
    27b9a5b (HEAD -> dev) okayyy f6
    408155c added restore .
    ac6afc2 added restore
    ```
    
- Pick 27b9a5b (HEAD -> dev) okayyy f6, So…
    
    ```
    zilen@sf-cpu-438:~/Desktop/project/files$ git checkout fea
    Switched to branch 'fea'
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git cherry-pick 27b9a5b
    Auto-merging files/file6
    CONFLICT (content): Merge conflict in files/file6
    error: could not apply 27b9a5b... okayyy f6
    
    zilen@sf-cpu-438:~/Desktop/project/files$ git add .
    zilen@sf-cpu-438:~/Desktop/project/files$ git commit -m "picked f6"
    [fea b214155] picked f6
     Date: Fri Feb 17 12:08:13 2023 +0530
     1 file changed, 1 insertion(+), 10 deletions(-)
    ```
