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
