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

# What is Git (the local view)
Git is a **Version Control System (VCS)** that holds a history of the changes of the files in a project and can revert changes in files based on that history. It solves the aforementioned issue as you can make changes in your project and if you break something, you can always revert it back. 


Before everything else you need to install git on your local OS and follow the instructions for your system.  
[Download Git for Windows / Linux / MacOS](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

## How git works

{:refdef: style="text-align: center;"}
![My Image]({{ site.baseimg }}/assets/img/example_json.png){:height="40%" width="40%"}
{: refdef}


## File states

## 




```bash
commit 6f9f1935dde016c7086746871d6704d1383bb00e (HEAD, master)
Author: Tbag <Tbag@gmail.com>
Date:   Sat Apr 17 22:37:50 2021 +0300

    Add a second file and a ignored file

 .gitignore         | 1 +
 another_file.txt   | 0
 important_file.txt | 1 +
 3 files changed, 2 insertions(+)

commit ed537265d3ae60f51ecc972ce1799e765b246555
Author: Tbag <Tbag@gmail.com>
Date:   Sat Apr 17 22:18:47 2021 +0300

    First commit

 important_file.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)

```

```bash
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   unwanted_file.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   unwanted_file.txt

```


# What is Git (the distributed view)
Up until now, i haven't told the whole truth about what Git is. Git is a **Distributed Version Control System**. This means that a folder that it monitored by Git can exist in many different computers (the local computers of a team working on some project). Each local computer holds a full backup of that folder (all the files and the changes made on them), so even if one computer dies, you can take the latest backup from the other computers. So now is the right time to break our local shell and confront the world as part of a team. 

## 

# Branching
Branching is what they call the `killer feature` of Git and this section i will explain why. 

# Tips and Tricks


# Exercises
I highly recommend visiting this [page](https://learngitbranching.js.org/) and trying to solve the there. It will further consolidate your knowledge. Another useful link for understanding branching is [this](https://git-school.github.io/visualizing-git/). I used it extensively to produce many of the images shown here.

# References
For this blog post i was (heavily) inspired by the following books / resources
1. Pro Git by Scott Chacon and Ben Straub
2. https://learngitbranching.js.org/
3. https://git-school.github.io/visualizing-git/