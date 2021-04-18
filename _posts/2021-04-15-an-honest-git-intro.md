---
layout: post
title: An honest git intro
date: 2021-04-15 00:00:00 +0300
# description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: git.png # Add image post (optional)
tags: [Mission1, Git] # add tag
---
* This will become a table of contents (this text will be scrapped).  
{:toc}

You  start working on a project named `awesome_project` and after a while you feel ok with the result. You give it back to your client and he wants you to make some changes (maybe fix an icon, add a button etc). Because you are afraid of breaking the code, you copy the files into a folder `awesome_project_v1`. You work on this folder and give it back to the client. Again he finds some work to do, so you repeat the procedure and create a third project named `awesome_project_v2`. Because clients are sadistic beings you may end up (after several iterations) with a project named `awesome_project_v6_ultra_mega_final_this_time_is_final_for_real`. So lets invest some time and do it the right way.


# Objective
Learn the most useful git commands for working in personal or team projects. I intend to
1. Give a high-level introduction about what Git is
2. Introduce the basic git commands that you will use most of the time
3. See how you work with remote repositories
4. Cover one of the most useful features of git -> branching


## Prerequisites
Nothing, but you need to install git and use the command line


# Git from above
Git is a **Version Control System (VCS)** that holds a history of the changes of the files in a project and can revert changes in files based on that history. It solves the aforementioned issue as you can make changes in your project and if you break something, you can always revert it back. 

{:refdef: style="text-align: center;"}
![My Image]({{ site.baseimg }}/assets/img/how_git_saves_changes.png){:height="50%" width="50%"}
{: refdef}

Before everything else you need to install git on your local OS and follow the instructions for your system.  
[Download Git for Windows / Linux / MacOS](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

> **CAUTION**: The following 2 sections are very important as they describe the different states the files can be under git versioning and the git workflow

## How git sees data
Everytime you make changes in your files and save the changes (`commit` them in git jargon), git takes a snapshot of every file that is tracking in your folder. You do another change and commit, another snapshot of everything is taken, In order to do that efficiently, the files that are not changed, are not saved again, but a pointer is made to point to that file in a previous snapshot. So git saves data as a series of snapshots as shown in the below figure. 


## File states
There are three different states for a file to be (commited, modified and staged). You can think of that as 3 different places the file can reside into. 
When you commit a file you store it safely to your local .git repository, that means your local database.
When you are working on a file, you modify it and the file resides in your working directory.  
You can't store it (commit it) immediately in your database. You first need to put it in a place called called staging area. Only the lucky files that live there can go to the.git directory with the next commit snapshot. 

### TODO -> add an image about wd, stae, .git


Another important distinction for the files is if they are tracked or untracked. 
Tracked files are the files that git knows about already. It has seen them in previous commits.

Untracked files are newly generated files, that git hasn't seen already 


## Git configuration
Before we start exploring the git commands, we need to do some basic configuration. 
The basic command for this is the `git config` command. 
You can have global configuration for all the projects that you use git to version control them, or you can fine tune your settings for each project. The global settings are usually saved in  a file in a location like `User/.gitconfig`
whereas the local settings are inside each project in the .git folder `.git/config`

The first thing you need to tell git is your name and email. 
```bash
git config --global user.name John Doe              # for global settings
git config --global user.email johndoe@gmail.com
```
or you can have local configuration inside a folder
```bash
git config --local user.name John Wick              # for local settings
git config --local user.email johnwick@yahoo.com
```
Yoy can see all your configured settings by running
```bash
git config --list --show-origin
```
that shows the following results for my case
```bash
file:/home/thanos/.gitconfig    user.name=Thanos Tasakos
file:/home/thanos/.gitconfig    user.email=thanos.tas@gmail.com
file:.git/config        core.repositoryformatversion=0
file:.git/config        core.filemode=true
file:.git/config        core.bare=false
file:.git/config        core.logallrefupdates=true
file:.git/config        user.name=Tbag
file:.git/config        user.email=Tbag@gmail.com
```

# Git basics

## Initialize a git repository
There are 2 ways to start a git repository (fancy words for just saying have git track the file changes inside a project). The first one takes an existing folder and imports it to git, whereas the second clones a git project from somewhere else. We will start by showcasing the first way, so open your command line and go to a folder of your choice. 

> **Note:** Some of the commands that i will show (for creating files etc) are OS specific. This means that they may not work for your OS. I will write in comments what each command do, and you may do it using commands from your OS or by using the GUI. For the git commands i strongly recommend typing them on command line along with me (and not just copy/paste them) in order to develop the necessary muscle memory. 

```bash
cd /path/to/folder      # go to the folder that you'll version control with git 
touch a.txt             # create an empty file
mkdir src               # create a folder
cd src                  # go inside that folder
touch hello_world.py    # create an empty python file in that folder
cd ..                   # go back to the root of your repository
```

The tree structure of your folder should look like this
```bash
.
├── a.txt
└── src
    └── hello_world.py
```
Now let's start tracking the changes in that folder. Let's initialize our git repository
```bash
git init
# Initialized empty Git repository in /home/thanos/Documents/github_repos/git_exploration/.git/
```
The tree structure of your folder now looks like this
```bash
.
├── a.txt
├── .git
│   ├── branches
│   ├── config
│   ├── description
│   ├── HEAD
│   ├── hooks
│   │   ├── applypatch-msg.sample
│   │   ├── commit-msg.sample
│   │   ├── fsmonitor-watchman.sample
│   │   ├── post-update.sample
│   │   ├── pre-applypatch.sample
│   │   ├── pre-commit.sample
│   │   ├── prepare-commit-msg.sample
│   │   ├── pre-push.sample
│   │   ├── pre-rebase.sample
│   │   ├── pre-receive.sample
│   │   └── update.sample
│   ├── info
│   │   └── exclude
│   ├── objects
│   │   ├── info
│   │   └── pack
│   └── refs
│       ├── heads
│       └── tags
└── src
    └── hello_world.py
```
The only thing that changes was that a hidden filder named .git was created and inside that folder is a bunch of files that for now we will ignore.

## A git workflow
One of the most useful info that we want to know about our version controlled files is their status. Git offers a command for that check
```bash
git status              # Show the status of all the files in the git repository
```
outputs
```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	a.txt
	src/

nothing added to commit but untracked files present (use "git add" to track)
```
Git is very helpful and tells us that the files are not yet tracked and proposes us to use add to track them. Lets just use that
```bash
git add .               # Start tracking files. The . option means track all 
                        # the files that you see
git status
```
outputs
```bash
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   a.txt
	new file:   src/hello_world.py

```
Notice now that there are no untracked files anymore, and the previous files are under `Changes to be commited`. Let's commit the changes and check again
```bash
git commit -m 'First commit'    # Every commit commands includes a msg using
                                # -m argument and a string afterwards to quickly
                                # summarize the changes made. 
```
outputs
```bash
[master (root-commit) c1c32eb] First commit
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a.txt
 create mode 100644 src/hello_world.py
 ```
 and if we run `git status` we see that
 ```bash
On branch master
nothing to commit, working tree clean
 ```
That is all, we have made our first commit. Everything looks good.


## Lets do some changes
Open the `hello_world.py` and type
{% highlight python %}
def hi():
    print('Hello world')
{% endhighlight %}  
and type `git status` again
```bash
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   hello_world.py

no changes added to commit (use "git add" and/or "git commit -a")
```
Lets create another file called b.txt and remove the a.txt and see what will happen
```bash
rm a.txt             # remove the file a.txt
touch b.txt          # create a new file 
```
`git status` outputs:
```bash
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    a.txt
	modified:   src/hello_world.py

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	b.txt
```
There is a shortcut to commit the known files in git (the files that are NOT under untracked files).
```bash
git commit -a -m "Second commit"    # Shortcut to do simultaneously the staging and 
                                    # commit for the files that are already known to git
git status
```
outputs
```bash
 2 files changed, 2 insertions(+)
 delete mode 100644 a.txt
thanos:git_exploration$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	b.txt
```
Lets add `b.txt` and see again the output
```bash
git add b.txt
git status
```
outputs
```bash
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   b.txt
```
Notice the different text `Changes to be commited` as opposing to `Changes not staged for commit`. `git add` starts tracking a file and automatically stages it for commit.

## Ignore some files
You can have some files that you do not want to track and save. Good examples of such files, are autogenerated logs or cache files from some libraries. You can do that in git by specifying a `.gitignore` file. 
```bash
touch ignored_file.ign  # Create an empty file named ignored.ign
nano .gitignore         # Create and open a file named .gitignore
```
add to that file the following line
```bash
*.ign                   # This tells git to ignore every file that ends with .ign
```
If you run `git status` you will not see `ignore.ign`, because git is told by the .gitignore file to not track it. Good examples of .gitignore files can be found [here](https://github.com/github/gitignore)

## Learn from history
Git offers a command to see the stream of changes you've made until now
```bash
git log
```
outputs
```bash
commit 44c1a86b1de25cdf70e84dd3d80be8057af63b31 (HEAD -> master)
Author: Thanos Tasakos <thanos.tas@gmail.com>
Date:   Sun Apr 18 19:09:00 2021 +0300

    add gitignore

commit 31be60988dd07e6b75df9410454166be51095422
Author: Thanos Tasakos <thanos.tas@gmail.com>
Date:   Sun Apr 18 18:43:55 2021 +0300

    Second commit

commit c1c32eb4cb0514d9f93d93e561f8109131e9115f
Author: Thanos Tasakos <thanos.tas@gmail.com>
Date:   Sun Apr 18 18:21:29 2021 +0300

    First commit
```
## Undo things

### Unstage a staged file
Lets say you create 1 additional file name `c.ign1`, but you want git to ingore it, and forget to add it to your `.gitignore` file. SO you accidentally add it to the staging area
```bash
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   c.ign1
``` 
You can use the hint *(use "git reset HEAD <file>..." to unstage)*, and add it to gitignore, so that you won't include it to your next commit
```bash
git reset HEAD  c.ign1          # Unstages the file c.ign1
```
### Discard changes made on a file
Let's say you add the following code snippet in your `hello_world.py` 
{% highlight python %}
def bye():
    print('Bye world')
{% endhighlight %}  
If you run `git status` you will see that is tagged as *modified*. If you want to completely discard the changes you made since your last commit to that file you can run `git checkout -- src/hello_world.py`.
> **CAUTION:** Be sure you really don't want these changes. Git can always find and retrieve the files when you commit them. But if a file is deleted before commiting it to git, or its changes are discarded, they **cannot** be retrieved. Git simply does not know about it.


# Git from above (the distributed view)
Up until now, i haven't told the whole truth about what Git is. Git is a **Distributed Version Control System**. This means that a folder that it monitored by Git can exist in many different computers (the local computers of a team working on the same project). Each local computer holds a full backup of that folder (all the files and the changes made on them), so even if one computer dies, you can take the latest backup from the other computers.  

## What is github

## Interact with remote repositories

# Branching
Branching is what they call the `killer feature` of Git and this section i will explain why.  


# Git commands




# Exercises
I highly recommend visiting this [page](https://learngitbranching.js.org/) and trying to solve the there. It will further consolidate your knowledge. Another useful link for understanding branching is [this](https://git-school.github.io/visualizing-git/). I used it extensively to produce many of the images shown here.

# References
For this blog post i was (heavily) inspired by the following books / resources
1. Pro Git by Scott Chacon and Ben Straub
2. https://learngitbranching.js.org/
3. https://git-school.github.io/visualizing-git/