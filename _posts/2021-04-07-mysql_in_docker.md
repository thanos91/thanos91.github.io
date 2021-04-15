---
layout: post
title: Create 
date: 2021-04-07 00:00:00 +0300
# description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: insert_image.jpg # Add image post (optional)
tags: [Docker, MySQL] # add tag
---

Nowadays, everyone and their mothers are expected to know SQL. Although you as an esteemed Data Scientist think that this is not what you are paid for, you fail to recognize the data part in DS. The language to speak with data is (for the last 50 years) SQL, so reluctantly you should consider adding this to your programming arsenal. Btw you need to have a database in your sytem and some data in it. So, because you also want to join the cool guys and girls and don't pollute your OS, it is a good idea to create the database inside a Docker Container. [go there](#Prerequisites)

# Objective
The objective of this post is to create and run a Docker Container with a MySQL Database configured,
We will use that container for the subsequent tasks, in order to familiarize with the basic (and advanced) SQL syntax.

Inspitation about the following post is drawn from  
1. SQL in 10 Minutes, Sams Teach Yourself
2. SQL Practice Problems 57 Beginning, Intermediate, and Advanced Challenges for You to Solve Using a Learn-By-Doing Approach
3. SQL Cookbook Query Solutions and Techniques for All SQL Users 
4. Learning SQL Generate, Manipulate, and Retrieve Data 
5. The Docker book

# Prerequisites
* Basic knowledge of Docker
* basic knowledge of running commands in command line

## Lets dockerize it

Create a file named "Dockerfile" with the following
commands in it


```
# my_project_folder/DockerFile

FROM mysql:

ADD create.sql 
```
The following code snippet does 2 things:
1. goes to Docker Hub(the place that docker images are stored) and downloads the specific image to your pc

2. runs the create.sql script that creates and populates the tables in our database

So the resulting image from this Dockerfile has a MySQL database created and populated, ready for use

### Spin up a container
