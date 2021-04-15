---
layout: post
title: Do you best with pytest 
date: 2021-04-14 00:00:00 +0300
# description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: insert_image.jpg # Add image post (optional)
tags: [pytest, TinyDB, cli] # add tag
---

When i started programming i thought that the only thing there was when writing code was to handle the task at hand. Later i would organize that code into functions and classes, write some documentation about it and hopefully whenever i needed to change something i could catch up really quickly.

The problem with that approach is when i did changes that broke the code that i have writen already. Maybe some new function did not do what i wanted. In these hard times i would place my hopes to simple print statements like  
```
# some code
print('Yo')
# another chunk of code with a variable a
print(a)
print(type(a))
print('Bye')
```
I would then fix the problem and delete the print statements (until the next bug).   

Testing comes to liberates us from this perpetual headache by formalising the way our program should work. Ideally, you should first write a test about a chunk of your program, make it fail and then implement the least effort to get that test to pass. By going through these circles of testing, programming and then testing again, you would realize Test Driven Development mindset and be more at ease about the functionality of your code. So let's start!

# Objective
Create a simple Command Line Interface App and thoroughly test it using the pytest module. 
I intend to 
1. Cover the most useful features of pytest library
2. Introduce basic concepts of Test Driven Development

## The App
We will create an command line interface app that  a teacher would use to grade the students taking his lecture. Of course you can create the same functionality in other ways, but we wanted a relatively simple app as a test bed for the creation of our tests.

We want to create the following basic functionality with this app
1. Insert a student record (Name, Surname, Grade, Exercise identifier)
2. Update a student record 
3. Delete a student record
4. Aggregation functionality
    * Delete every record for a student
    * Find the final grade of student based on some formula for the weight of each exercise
    * Return top K or bottom K performing students

The finished Grades app can be found [here](https://github.com/thanos91/grades)


see [Name of Link]({% post_url 2017-09-12-the-best-organizer-software %})

## The Database


## Let's Dive
You could clone the final project in a folder and just run the tests, but this is no fun, so i strongly recommend to follow my pace and write ti from scratch. 

First things first go to a folder of your choice and create the folders and files that are shown below



![I and My friends]({{site.baseurl}}/assets/img/we-in-rest.jpg)



# References
For this blog post i was inspired by the following books
1. Python Testing with pytest Simple, Rapid, Effective, and Scalable by Brian Okken 
2. Test-Driven Development with Python: Obey the Testing Goat: Using Django, Selenium, and JavaScript