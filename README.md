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
