---
title: "E03: Host MySQL"
published: true
morea_id: experience-mysql-hostserver
morea_type: experience
morea_summary: "Get started with hosting a MySQL server"
morea_sort_order: 3
morea_start_date: "2023-01-21"
morea_labels:
---

# E03: Host MySQL

## Task

Be sure to use the [grading assistant](https://sp23.ics321.org/) to make sure your assignment is correct.

To begin this assignment you must first become familiar with your cPanel server and how to run Python programs from the command line.

Your server host name is http://<your UH username>.ics321.org. Your cPanel control panel is at http://<your UH username>.ics321.org/cpanel.

**Your username is the first 5 characters of your UH username followed by '321'** and your password is Xy12345678%#! where X is the first letter of your last name capitalized. y is the first letter of your first name not capitalized. 12345678 is your 8-digit UH ID.

For example, my UH email address is **richardh@hawaii.edu**. My server URL is **http://richardh.ics321.org**, my cPanel login username is **richa321** and my password would be **Hr12345678%#!** (if **12345678** were my 8-digit UH ID).

Once you log into cPanel, you see there are a large number of apps available to you. Open the File Manager and familiarize yourself with the directories and files that come with a server.

## 1.1 Executing Python Instructions

Locate the hidden file named .htaccess in your public_html directory. To make sure hidden files are visible, in the File Manager, click the Settings button in the upper right hand corner and check the checkbox to Show Hidden Files.

Add the following two lines to your .htaccess file at the very top.

Options +ExecCGI
AddHandler cgi-script .py

This will tell the web server that any file ending in .py is a cgi-script, or program.

To test to make sure your server can execute Python programs, create a new file in your public_html directory named test.py containing the following program:

```
#!/usr/bin/python3

print("Content-type: text/plain\n")
print("hello world!")

import sys
ver = sys.version
print("Python version",ver)

import cgi
form = cgi.FieldStorage()

if "name" in form:
name = form['name'].value
else:
name = "there"

print("Hello",name)
```

Save the file. Change the file permissions to 755. To do so, right-click on the file in the file manager and select Change Permissions. A window like the following will appear.
![permission picture](/Users/benjaminkim/Desktop/GitHub/SampleMoreaWebsite/morea/Relational-Databases-Create/permission.jpeg)

Next, you need to make sure that your test.py file doesn't contain carriage returns at the end of each line. To do so, click on the Terminal application in cPanel. Then type cd public_html. Then type sed -i 's/\r$//g' test.py.

![path picture](/Users/benjaminkim/Desktop/GitHub/SampleMoreaWebsite/morea/Relational-Databases-Create/path.png)

To test your program, enter your domain name in the browser. You should see test.py in the list of files. Click on it. Your program should respond with the Python version number and "Hello there."

In the browser address bar, if you type "?name=Joe" after the URL (e.g., http://<your UH username>.ics321.org/test.py?name=Joe) then the your program should respond with the Python version number and "Hello Joe."

## 1.2 Executing PHP Programs

To execute PHP programs, create a new file in your public_html directory named test.php containing the following program:
```
<?php

header('Content-Type: text/plain');
print("hello world!\n");

$ver = phpversion();
print("PHP version $ver\n");

if(isset($_REQUEST['name'])) {
    $name = $_REQUEST['name'];
}else{
    $name = "there";
}

print("Hello $name\n");
?>
```
To test your program, enter your domain name in the browser. You should see test.php in the list of files. Click on it. Your program should respond with the PHP version number and "Hello there."

In the browser address bar, if you type "?name=Joe" after the URL (e.g., http://<your UH username>.ics321.org/test.php?name=Joe) then the your program should respond with the PHP version number and "Hello Joe."

## Submission instructions
When you are done you don't need to do anything. Be sure to use the grading assistant (link at the top) to verify you got all the points and your scores will be automatically recorded.



