---
layout: post
title: Do you best with pytest
date: 2021-04-14 00:00:00 +0300
# description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: pytest.png # Add image post (optional)
tags: [Mission1, pytest, TinyDB, cli] # add tag
---
* This will become a table of contents (this text will be scrapped).  
{:toc}


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

# The App
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


# The Database
For the purposes of this post and because we want to focus on the testing side of things , we will use a simple database called TinyDB (which is basically a json file). Json files are a data format that allows passing information between different processes or applications. A json file looks a lot like a python dictionary and python dictionaries can be serialised to json format. A json looks like this

<img src="{{ site.baseurl }}/assets/img/example_json.png" width="200" align="center"> 

The basic functions that are available to us from TinyDB (this is called TinyDB's API) are
```python
from tinydb import TinyDB, Query

db = TinyDB('test.json')    # create a db 

# By default Tinydb creates a table named '_default' where it stores all data
table = db.table('Exams')   # Create a table in that db named Exams

db.drop_table('table_name') # drop the table from database


# Insert a record in the db (in the '_defaults' table)
db.insert({'name': 'Thanos', 'surname': 'Tasakos', 
          'grade': 87, 'exam': 'exam1'}) 

table.insert({'name': 'exam1'}) # or insert in the 'Exam' table

# Search for data (Querying)
q = Query()         # Create a new query object
q.field == 2 	    # Match any document that has a key field with value == 2 
                    # (also possible: !=, >, >=, <, <=)
q.grade > 80        # Find all grades bigger than 80

# Get data
df.all()            # gets all documents in db
db.search(query)    # Get a list of documents matching the query

# Update data
db.update(fields, query) # Update all documents matching the query to contain fields


# Remove data
db.truncate()       # remove all documents in '_defaults' table
table.truncate()    # remove all documents in 'Exams' table
db.remove(query)    # remove all documents 
```

# Dive into the project

## Setting Up

You could clone the final project in a folder and just run the tests, but this is no fun, so i strongly recommend to follow my pace and write it from scratch. 

First things first go to a folder of your choice and create the folders and files that are shown under first image

{% capture url %}{{ site.baseurl }}/assets/img/initial_structure.png{% endcapture %}
{% include image.html url=url description="(a) Initial Project Structure" %}

{% capture url %}{{ site.baseurl }}/assets/img/after_venv.png{% endcapture %}
{% include image.html url=url description="(b) After venv creation" %}



Then create a virtualenv named venv (or whatever name you like) and iclude it in your folder. Open a terminal, navigate to your projects folder and type
```bash
# home/thanos/Documents/github_repos/grades  

# if you do not have virtualenv installed
pip install virtualenv
virtualenv venv
```
Activate the virtual environment
```bash
source venv/bin/activate

pip install tinydb pytest # to install database and testing library 
                          # in your virtual environment
```
The project structure after these steps should look like (b). 

Finally in your setup.py file add the following snippet
```python
# grades/setup.py

from setuptools import setup, find_packages

setup(
    name='grades',
    packages=find_packages(where='src'),
    package_dir={'': 'src'},
)
```

And in a command prompt run 
```
pip install -e .
```
This command will use the setup.py and install your project in editable mode. This will be useful for testing your project while developing.

To test that everything works as expected modify the hello_world.py 
```python
# grades/src/grades/hello_world.py

def hi():
    print('Hi')
```
And then run in command prompt
```bash
python # to start the python interpreter

from grades.hello_world import hi
hi()
# Hi
```

More info about virtual envs and their usefulness can be found [here]({% post_url 2021-04-14-virtualenv %}). What is packaging and how the import works can be found [here]({% post_url 2021-04-14-packaging %}). Οσο μιλάω εσείς παραγγέλνετε

### Write our first test

### Difference between unit tests and functional tests

### Use fixtures 


# References
For this blog post i was (heavily) inspired by the following books
1. Python Testing with pytest Simple, Rapid, Effective, and Scalable by Brian Okken 
2. Test-Driven Development with Python: Obey the Testing Goat: Using Django, Selenium, and JavaScript
