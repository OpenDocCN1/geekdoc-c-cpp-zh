![](cover.jpeg)

Programming:

Python Programming - Windows 10, Software & Databases

© Copyright 2015 - All rights reserved.

In no way is it legal to reproduce, duplicate, or transmit any part of this document in either electronic means or in printed format. Recording of this publication is strictly prohibited and any storage of this document is not allowed unless with written permission from the publisher. All rights reserved.

The information provided herein is stated to be truthful and consistent, in that any liability, in terms of inattention or otherwise, by any usage or abuse of any policies, processes, or directions contained within is the solitary and utter responsibility of the recipient reader. Under no circumstances will any legal responsibility or blame be held against the publisher for any reparation, damages, or monetary loss due to the information herein, either directly or indirectly.

Respective authors own all copyrights not held by the publisher.

Legal Notice:

This book is copyright protected. This is only for personal use. You cannot amend, distribute, sell, use, quote or paraphrase any part or the content within this book without the consent of the author or copyright owner. Legal action will be pursued if this is breached.

Disclaimer Notice:

Please note the information contained within this document is for educational and entertainment purposes only. Every attempt has been made to provide accurate, up to date and reliable complete information. No warranties of any kind are expressed or implied. Readers acknowledge that the author is not engaging in the rendering of legal, financial, medical or professional advice.

By reading this document, the reader agrees that under no circumstances are we responsible for any losses, direct or indirect, which are incurred as a result of the use of information contained within this document, including, but not limited to, —errors, omissions, or inaccuracies.

TABLE OF CONTENTS

Introduction

Configuring Your Windows 10 Environment For Python

What You Need:

Installing Python on Windows

Download and Install Python

Using the Windows Python Installation

Installing a Package Manager

Installing Cygwin

Installing Sublime Text

Check it All Works

Getting To Grips With Python

Creating and Running Programs

Comments

Variables

Reserved Keywords

Basic Variable Types

Numbers

Integers

Floating Point Numbers

Strings

Other Useful Values

More Complex Data Types

The List

Tuples

Dictionaries

Sets

Conditions

Boolean operators

The "in" operator

The 'is' Operator

The "not" Operator

Loops

"break" and "continue" Statements

Functions

How to Call a Function in Python

Classes and Objects

Accessing Object Variables

Accessing Object Functions

Modules and Packages

Exploring built-in modules

Writing Modules

Writing Packages

MySQL Python Tutorial

Before We Begin

The –MySQL Module

Mysqldb Module

Creating and Populating a Table

Retrieving Data

The Dictionary Cursor

Column Headers

Prepared Statements

Inserting Images

Reading Images

Transaction Support

Conclusion

Introduction

Knowing where to begin with computer programming can be a real challenge. Most people have little to no knowledge of how to write computer code or where to even begin when it comes to writing a computer program. Python is an easy language to learn, and is capable of so much more than just simple programming.

It is a general purpose language that first appeared in the 1980’s and was, believe it or not, named after Monty Python. It’s used for a wide range of purposes, from testing microchips, to powering some of the biggest websites in the world and to building video games. Python is a small language, is close to the English language and contains hundreds of third party libraries.

Because Python is similar to the English language, it is easy to read. It also follows very strict rules on punctuation, which means that, unlike some computer languages, your code is not littered with annoying curly braces ({ }), that get in the way and make it difficult to read. Python also contains PEP 8, a set of rules that tells each Python developer how their code should be formatted, meaning you always know what to do, where a new line should be and helps you to read other Python scripts, no matter who wrote them. 

Python has been in existence for more than 20 years and there is an awful lot of Python code about. It is also an open source language, which means that anyone can take it, read it and modify it for their own uses.  There are plenty of Python community groups where users can go to get help or just join in general Python chitchat.

In this book, I want to talk about what Python can do and how to get it up and running on your Windows 10 PC, as well as how to use it. This is suitable for complete beginners or for more advanced users and I hope that everyone will gain something from this book.

Configuring Your Windows 10 Environment For Python

So, you want to learn how to use Python on your Windows 10 computer. The first thing you need to do is configure your Windows environment, i.e. your computer, and prepare it for use with the programming language.

What You Need:

●  

● A Windows 10 PC or laptop

● Python

● Cygwin

● A text editor

Let’s look at this one step at a time:

Installing Python on Windows

There are a couple of things you need to do to get the Python environment running on your Windows computer:

● Download and install Python

● Use the Windows Python Installation

● Install a Package Manager

Download and Install Python

● First of all, you need to download the correct installation package, so go to [http://www.python.org/download/windows/http://www.python.org/download/windows/](http:///h)

● Click on Individual Releases

● You will now be taken to a list of releases, choose the latest one

● Make sure that you download the version that corresponds with the version of Windows that you are running and whether it is 32 or 64-bit.

● If you are running the Mozilla Firefox browser, click on Save File. If you are using Internet Explorer, click on Run

● The Python installer will open so select who is going to be able to access Python on your system – ether just you, or anyone on the system. Click on Next

● Now you need to pick a directory to install Python to – leave it as the default selected and click on Next

● Click the box to accept the installation options and click on Next

● Python will now start to install on your system. Leave it until it has finished and then click on Finish

Using the Windows Python Installation

● Click the Start menu and look for Python v*.*.* - whichever version you installed

● You will see that several things have been installed.

o IDLE – Python GUI – similar to the command line Python prompt but it has an interface which is graphical

o Module Docs – a help file that tells you about the installed modules

o Python (Command line) – looks like the server prompt

o Python Manuals – there for hl if and when you need it

o Uninstall Python – which you will hopefully never have to use.

Before you can access Python just by typing it at the command prompt, we need to set the Windows PATH variable, which we will do next.

Installing a Package Manager

You will very quickly determine that you need to install a module that is not included in the standard distribution of Python. To do this, we need to install a Package Manager that will let us install the new packages. For this bit, we are using EasyInstall but, later on, I will tell you how to install and use Cygwin as well, so you have the choice.

● Go to [http://peak.telecommunity.com/DevCenterEasyInstall](http:///h) 

● Click on Installing “Easy Install”

● Right click on the ez setup.py linked and select Save Link as or Save Target as

● When it has finished, find the .py file on your PC and double click on it so it runs. It will open and run within Python and will be installed

To set up the PATH variable, so that Windows 10 knows where to look for Python:

● Right click My Computer

● Select Properties

● On the next screen, click on  Advanced

● On the next screen, click on Environment Variables

● I am going to assume that, when you installed Python, you chose to install it just for you and not for everyone else on the system – click on Path – located in the box under User Variables

● Click on Edit

● On the next screen, look of the variable value box and place your cursor after the (;) which denotes the last entry

● Enter the following as the final entry in the box and do NOT forget to include the (;) semicolon at the end – C:\Python25\Scripts;

● Click on OK another three times to get out of System Properties

● Now open up a command prompt by clicking on Start, Run and typing in cmd. Click on OK

● In the next box type in easy_install BeautifulSoup – this will install the module BeautifulSoup – repeat this for any other module that you want to use and they will be installed

● When you get back to the command prompt, type in Python and then press Enter

● Type in import BeautifulSoup (or the name of any other module)

● Another prompt will appear without showing any error messages. We now know that we have set the PATH variable properly and that EasyInstall was installed correctly.

● You also now know how to install new packages!

That is all there is to installing Python and EasyInstall on your computer. Next, Cygwin

Installing Cygwin

This isn’t quite so easy

● Go to [http://cygwin.com/http://cygwin.com/](http:///h)

● Click on Install Cygwin from the menu on the left

● Click on setup-x86.exe and then run it

Cygwin is a useful program as it will download other programs from the internet and install them for you. You will need to provide information about your internet connection, although, as you go through the set up process, you will mostly be able to accept the default settings

Once that has completed, you will be presented with a list of download sites. They are all identical so just pick any one from the list and click on Next

Now you will get an Upgrade warning –this will only be applicable to those who are upgrading from an older version of Cygwin. If this is the first time you have installed it, ignore this message

Now you will be presented with a list of software to download. You want three packages – openssh, git and curl. Type the name of each one into the search on the site and, when the package comes up, click on Skip. This will ensure that the latest version is installed – do this for each package.

Once those three are ready for installation, Cygwin will inform you that you need to install other packages as dependencies. What this means is that, if you wat to use a specific package, called A for example, and A needs another package called B to run properly, Cygwin will know this and will ask if it can install package B as well as A.

When this message appear, just click on Next, Cygwin will begin to download and install the three packages you asked for as well as all of their dependencies. This can take a while, although that will depend on how fast your internet connection is. On your screen, you will see three separate progress bars – when the middle one, called TOTAL, is full, Cygwin has finished.

If you have requested that Cygwin put an icon on your desktop, it will proceed to do so and you will see a shortcut called Cygwin Terminal. This is the icon you will use when you run your Python code as well as for accessing the packages you downloaded through Cygwin.

Click on it and a terminal window will appear and we can begin to use it. First of all, we need to find out which packages have actually been installed so, at the command prompt, type the word which

A list of packages will appear and will most likely show you all the Cygwin packages you installed but it may not show Python itself. That’s OK, because you did not install Python using Cygwin. Now you need to tell Cygwin to find Python and you do that by typing the following command:

● $ echo "PATH=\$PATH:/cygdrive/c/Python32" >> .bash_profile

Make sure that you type in the version of Python that you are using – if you installed a different version replace Python32 with the correct one. You will only need to do this step once; after this, the terminal will find Python all the time.

That’s Cygwin installed and set up, the final step is to set up your text editor. I am giving you the instructions for Sublime Text – if you use a different one make sure you follow the installation instructions that come with it. Be aware that Microsoft Word is NOT a text editor; it is a word processing program and, as such, cannot be used for this.

Installing Sublime Text

Sublime text is a very powerful text editor, it is very useful and it also has a free trial that does not expire.

● Go to [http://www.sublimetext.com/](http:///h) and download the installer

● Run it

●  

While Sublime Text is not free, you can use it on a trial for as long as you like. I would suggest though, if you get on with it and use it to write a lot of programs, that you purchase a license for the full software – do this with any that you use.

Check it All Works

Now that everything is installed, it’s time to see if it all works OK. The very first program that any programmer writes is the now famous “Hello World!” program. All this does is turn out text on the terminal and is a good way of checking that everything works as it should.

Type the following at the command line in your terminal:

● $ python -c 'print("Hello, World!")'

● Hello, World!

If that works, open up Sublime Text and we will write a program to file. Type the following into the text editor:

● #!/usr/bin/env python

● print("Hello, World!")

Save it to your Home Directory, making sure it goes in C:\Cygwin\home as hello.py.

Open your terminal and type cd c:\cygwin\home, press enter

Type the following at the command prompt:

●  

● $ chmod a+x hello.py

● $ ./hello.py

● Hello, World!

You should see “Hello, World!” show up on your screen. If it does, you are ready to start learning how to use Python on your Windows 10 computer.

Getting To Grips With Python

On your windows desktop, you should see a Python icon. Double click on it and this will open up the Interactive Interpreter. This is where you are going to type in individual commands and see what the results are instantly. It’s a really good way of experimenting to see what commands do and it is also a highly useful tool. Type in:

● X = 3

Press Enter and then type in

●  

● Print X

●  

Press enter again – you should see something like the following appear on your

● >>> x = 3

● >>> print x

● 3

● >>>

## [Creating and Running Programs](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

In order for Python to be truly useful to you, you need to know how to create a program and run it. On Windows 10, when you install Python, this will associate all files with the .py extension with the interactive interpreter. To run any program, open the terminal and change the directory to the one that you installed Python in – something like cd c:\Python** - make sure you replace ** with the version number. Then when you are ready to run your program, you type in the following:

● **./program.py - ** denotes the name of your program

These programs are simply text files that contain a set of instructions for the interpreter and they are compiled in your text editor. Python will install something called an IDE – Integrated Development Environment, which will have some very useful tools in it, such as a syntax checker, code browser and debugger. All of these tools are designed to help you get your coding correct from the word go.

Comments

Any line of code that begins with # is a comment. Comments are for your information and will not be read by the interpreter. Every line that contains a comment must begin with the hash symbol.

Variables

Remember that very simple program we created at the beginning of this chapter? The x is a variable and we associated that with a number, in this case 3, before we printed it to the screen. Variables are the most basic concept of any programming language and are what we use to store values in while we work with them.

The code we wrote – x = 3 – is a statement – statements on a particular job and in this case, the job is to assign the value (3) to the variable (x). In Python, this is known as binding and it is an important concept.

The name of a variable in Python can be pretty much anything, provided you follow simple rules:

● It must only contain asci characters, underscores and digits – you cannot use any other symbol or a space

● It must not begin with a digit

● It cannot be any of the words that are on a reserved keyword list.

Reserved Keywords

● and

● as

● assert

● break

● class

● continue

● def

● del

● elif

● else

● except

● exec

● finally

● for

● from

● global

● if

● import

● in

● is

● lambda

● not

● or

● pass

● print

● raise

● return

● try

● while

● with

● yield

None of these keywords can be used in any file or program name as they are reserved by Python. As Python is a dynamic language, these keywords can change in the future so, to stay up to date, you can periodically check the current list of keywords by typing in the following in the terminal:

● #!/usr/bin/python

●  

● # keywords.py

●  

● import sys

● import keyword

●  

●  

● print "Python version: ", sys.version_info

● print "Python keywords: ", keyword.kwlist

[Basic Variable Types](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

We now know that variables are a basic Python concept and so are all the different value types that variables can have. These are called data-types, denoting all the ways of storing the data. The word “type” has a particular meaning in computer programming, in that it means a specific way of categorizing different types of objects. Each object has a type and the most basic data types are:

[Numbers](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

Integers

Integers are whole numbers and, in theory, they are any whole number in between a range of plus infinity down to minus infinity. The range is limited by the computer but in Python, the absolute maximum size is limited by just one thing – how much memory your computer has got.

Python uses two integer types – integers and long integers, which are integers that are longer than a specific amount.

Floating Point Numbers

Computers are very good when it comes to dealing with integers, or whole numbers. A floating point number is one that has a number after a decimal point, e.g. 5.2, or -8.1.

Whole numbers can be stored as floating point numbers – all you do is add a decimal point in when you write it down, for example, 1.0, or 9.0\. Floating point numbers are quite a bit slower to work with because computers find them somewhat more complicated.

In the newer versions of Python, if you try to divide an integer by an integer, you will get a result you don’t expect, for example:

●  

● >>> 7/2

● 3

In order to get the right result, one of the integers must be converted to a floating point number:

● >>> 7.0/2

● 3.5

[Strings](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

A string is simply a piece of text and Python will not make any distinction between a string that contains one character or an entire block of characters or text. Python contains two different string types – basic and Unicode.

Basic string types are used to store text in a sequence of numbers, or bytes, with just one byte for each character. You should only use these if you know for certain that your text has ASCII values in it. They are also used for storing binary data and are often called byte-strings.

Unicode strings use the Unicode standard to store text internally. These are a little more complicated to use because you have to know the encoding that you have stored the code in, whenever you read it or save it out. An overview of how to use each one is below:

Basic String – you add a string to your program by surrounding the relevant text with single or double quote marks, for example:

● x = 'This is a string'

● y = "And so is this."

You can also include a string that has a break in it, or runs over several lines, using triple quotes, like this:

● x = """This string

● goes over multiple lines.

● So it includes line breaks."""

●  

● y = '''This string uses single quotes.

● But it is still multi-line.

● As you might have guessed.'''

You can also include special characters, like a quote character or line breaks, by using escaped characters. Python uses the UNIX convention of making use of the backslash key as an escape character. For example:

● # The variable x is a string which contains

● # a single line break

● x = '\n'

● # The variable y has an escaped quote character

● # To include the quote in the string (instead of

● # it terminating the string)

● y = 'Don\'t worry about quotes'

● # z is a single character - a backslash which has to be escaped

● # with another backslash

● z = '\\'

If you don’t want to use the escape key to enter a backslash in your test sting, you can use what is known as a raw string. To denote this, you would precede the string with r.

Because raw strings are meant to be used for useful expressions and not, for example, Windows paths, they cannot have a backslash at the end. The backslash is interpreted by Python as an escape from the quote that comes after.

Python strings are stored using numbers and are not encoded in any way. The interpreter will take what you give it and store it as a byte sequence. Because they hold bytes, these strings must only have ASCII characters in them, unless you add an encoding at the start – then you can include characters that are not ASCII. However, you should only do this if you really know what you are doing. 

Unicode Strings – These contain an internal representation that allows text to be stored as text. In effect, your computer knows which characters are being compared by the text. However, you will still need to select an encoding for when you write or read that data.

Unicode literals can be included in your program by putting a u at the front of the string. If you do not specify the encoding at the beginning, you will only be able to use ASCI characters but Python will store your data as Unicode and not a byte string.

Quoting and escae rules are the same for Unicode strings as they are for byte strings:

● x = u'A unicode string'

●  

● y = u'''A multi-line unicode

● string.'''

●  

● y = ru"""This is a

● raw, multi-line

● unicode string !!!

● """

You can force the interpreter to convert Unicode to byte strings and vice versa with specifying explicit encoding but you are likely to get one of the following errors:

● UnicodeEncodeError

● UnicodeDecodeError

One of those will just bring your program crashing to a halt. When this happens, it is usually because one of the strings that you are trying to “implicitly” convert contains characters that cannot be represented in the default encoding (usually ASCII).

[Other Useful Values](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

There are some other values that are extremely useful:

● None - Sometimes seen as Null in other programming languages, this represents “nothing”.

● True - The 'Boolean' value of true.

● False - The Boolean value of false.

You will see these values quite a lot throughout your programming life and they can be included in any program you write simply by writing:

● x = None

● y = True

● z = False

[More Complex Data Types](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

When you work with more complicated information, you might want to group certain data together. Python has a lot of concepts that allow you to do this, including things like list comprehensions, generators and iterators. The fundamental way of grouping this data is to use something called data-structures. These objects will store all of the values together and, in Python, you can create custom data-structures. However, it does have four built in ones. Object that are used to store data are known as containers.

The following data types can have many different operations performed on them and many are built in to the data type already (called Methods).

[The List](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

This is used to store groups of items in order. You can add to them or remove them at any time, sort them or search through the list for specific values. You can even start with a list that is empty, adding to it as you go along, or you can use one that is already pre-populated. Items that are included in your list can be any other object, and that includes other lists as well. This means that you can have many different lists, and lists of lists, using them to create a complex structure – these are useful as building blocks.

When you write a list, it should have square brackets, with each item separated by a comma:

● # w is an empty list

● w = []

●  

● # x has only one member

● x = [3.0]

●  

● # y is a list of numbers

● y = [1, 2, 3, 4, 5]

●  

● # z is a list of strings

● # and other lists

● z = ['first', [], 'second', [1, 2, 3, 4], 'third']

You can access anything on a list by “indexing”. That index has to be an integer that represents the position of the item in the list. The first position is zero. Variables can be indexed by placing square brackets, containing the index, after the variable.

If you attempt to get access to a position that has not yet been created, you will receive an IndexError on screen. If you want to access from the end of the list, you use negative indexes. -1 is the last position on your list, followed by -2, -3, etc.:

● >>> x = [1, 2, 3, 4, 5]

● >>> print x[0]

● 1

● >>> print x[4]

● 5

● >>> print x[-1]

● 5

● >>> print x[-5]

● 1

● >>> print x[10]

● Traceback (most recent call last):

●   File "<stdin>", line 1, in ?

● IndexError: list index out of range

[Tuples](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

Tuples are similar to lists in that they store sequential information. However, they cannot be changed after they have been created, unlike a list, which can be. The interpreter knows exactly the types and the lengths of the members of a tuple and, as such, they are more efficient to work with than a list is. Tuples can be sliced or indexed but not changed and you will come across them “implicitly” throughout Python. An example of that would functions that return multiple values would return those values as a tuple.

To create a tuple, you use parentheses, not square brackets:

● >>> x = (1, 2, 3,4)

● >>> x

● (1, 2, 3, 4)

● >>> x[0]

● 1

● >>> x = (1,)

● >>> x

● (1,)

● >>> x[0]

● 1

● >>> x = ()

● >>> x

● ()

● >>> x[0]

● Traceback (most recent call last):

●   File "<stdin>", line 1, in ?

● IndexError: tuple index out of range

Even if you only have one member in the tuple, you still need to add the comma. If you just put a 1, for example, t would not be classed as a tuple, whereas 1, would be. If you need to create an empty tuple, you would use one of the following

:

● ()

● tuple ()

[Dictionaries](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

Dictionaries are one of the most useful and flexible types of data and Python is built on them. Dictionaries will store data but they use keys. This means you can look up particular pieces of data using that key. As with the other data types, there is a syntax built in to Python to allow you to create a dictionary:

● >>> x = {'key1': 'value1', 'key2': 'value2'}

● >>> print x

● {'key2': 'value2', 'key1': 'value1'}

●  

The values can be retrieved though indexing, in the same way as you do with lists and using the same syntax. However, instead of the position you would use the key:

● >>> x = {'key1': 'value1', 'key2': 'value2'}

● >>> print x['key1']

● value1

Strings don’t have to be used as keys, instead any object can be used, provided it is immutable, i.e. it doesn’t change. This is another good example of where tuples come in handy:

● >>> attemptedKey = {}

● >>> x = {attemptedKey: 'some value to store'}

● Traceback (most recent call last):

●   File "<stdin>", line 1, in ?

● TypeError: dict objects are unhashable

● >>> anotherTry = (None, 2)

● >>> x = {anotherTry: 'some value to store'}

● >>> print x

● {(None, 2): 'some value to store'}

[Sets](http://www.voidspace.org.uk/python/articles/python_datatypes.shtml#/h)

The set is, without a doubt, one of the most useful of all the data types; so useful that it is now a built in feature of Python. Sets have unique members and are extremely efficient for testing if a value is contained in the set. It is a good deal faster than using the list data type but, unlike all the other data types, there isn’t any syntax. In order to create a set you need to use the set constructor:

● >>> x = set()

● >>> x

● set([])

● >>> x.add(1)

● >>> x

● set([1])

● >>> x.add(1)

● >>> x

● set([1])

● >>> x.add(2)

● >>> 1 in x

● True

● >>> 2 in x

● True

● >>> 3 in x

● False

● >>>

Conditions

In order to evaluate conditions, Python uses Boolean variables. You already know that True and False are the Boolean variables that are returned when an expression is evaluated or compared, for example:

●  

● x = 2

● print x == 2 # prints out True

● print x == 3 # prints out False

● print x < 3  # prints out True

If you notice, the variable assignment uses on Equals operator whereas a double Equals operator is used when a comparison between two variables is done. Not Equals is shown as “I=”

Boolean operators

You can build up complex Boolean expressions by using two Boolean operators – “and” and “or”. For example:

● name = "John"

● age = 23

● if name == "John" and age == 23:

● print "Your name is John, and you are also 23 years old."

●  

● if name == "John" or name == "Rick":

● print "Your name is either John or Rick."

The "in" operator

This can be used as a way of checking if a specific object actually exists inside an object container, like a list:

● if name in ["John", "Rick"]:

● print "Your name is either John or Rick."

Python does not use brackets to define code blocks instead it uses indentation. Standard indentation is 4 spaces although you can use any other space amount or the tab button if you wish. Code blocks do not require any termination. The following example is the use of the “if” statement with code blocks:

● if <statement is true>:

●     <do something>

●     ....

●     ....

● elif <another statement is true>: # else if

●     <do something else>

●     ....

●     ....

● else:

●     <do another thing>

●     ....

●     ....

For example:

● x = 2

● if x == 2:

●     print "x equals two!"

● else:

●     print "x does not equal to two."

A statement can only be evaluated as True if any one of the following is right:

● The True Boolean variable is used or is calculated by using an expression, or

● An object that is not considered as “empty” is passed.

Examples of objects that are considered as empty include:

1.  An empty string – denoted by “”
2.  An empty list – denoted by []
3.  The number zero is used – 0
4.  Use of the false Boolean value – False

The 'is' Operator

The “is” operator does not match variable values; instead, it matches instances themselves. An example:

● x = [1,2,3]

● y = [1,2,3]

● print x == y # Prints out True

● print x is y # Prints out False

●  

The "not" Operator

If you use “not” in front of a Boolean operator, it will invert it:

● print not False # Prints out True

● print (not False) == (False) # Prints out False

Loops

Python has two different types of loop – For and While. The “for” loop will iterate over a specific sequence, for example:

● primes = [2, 3, 5, 7]

● for prime in primes:

● print prime

They are able to iterate over number sequences that use the “range” and the “xrange” functions. The difference between these two is that the first will return a new list containing numbers of a specific range while the second will return an iterator, which is far more efficient.

● # Prints out the numbers 0,1,2,3,4

● for x in xrange(5): # or range(5)

● print x

●  

● # Prints out 3,4,5

● for x in xrange(3, 6): # or range(3, 6)

● print x

●  

● # Prints out 3,5,7

● for x in xrange(3, 8, 2): # or range(3, 8, 2)

● print x

“while” loops will repeat for as long as a specific Boolean condition is met, for example:

● # Prints out 0,1,2,3,4

●  

● count = 0

● while count < 5:

● print count

● count += 1  # This is the same as count = count + 1

"break" and "continue" Statements

The difference between these two is that “break” is used as a way of exiting a “for” loop while “continue” will skip over the current text block and will go back to the “for” or “while” statement. A couple of examples:

● # Prints out 0,1,2,3,4

●  

● count = 0

● while True:

●     print count

●     count += 1

●     if count >= 5:

●         break

●  

● # Prints out only odd numbers - 1,3,5,7,9

● for x in xrange(10):

●     # Check if x is even

●     if x % 2 == 0:

●         continue

●     print x

●  

Functions

Functions are an incredibly useful way of dividing code into blocks that are useful. This allows you to order your code, to make it a bit more readable, to reuse it and, in the process save yourself some time. Functions are also a way of defining interfaces so that programmers are able to share their code.

We know that Python will make use of blocks, which is a piece of code written something like:

● block_head:

●     1st block line

●     2nd block line

●     ...

In instances where the block line is some more Python code or another block, and the block head is written in the following format – block_keyword block_name(argument1, argument2…). You already know some of the block keywords – if, for, while, etc. We use the keyword def to define a function n Python, followed up by the name of the function:

● def my_function():

●     print "Hello From My Function!"

Functions can also receive arguments – these are variables that have been passed from the caller to the function. An example:

● def my_function_with_args(username, greeting):

● print "Hello, %s , From My Function!, I wish you %s"%(username, greeting)

● Execute Code

Functions can also return a value by using the keyword return, for example

● def sum_two_numbers(a, b):

● return a + b

How to Call a Function in Python

All you need to do is write the name of the function, followed by (). Put ay arguments that are required inside the brackets. An example:

● # print a simple greeting

● my_function()

● #prints - "Hello, John Doe, From My Function!, I wish you a great year!"

● my_function_with_args("John Doe", "a great year!")

● # after this line x will hold the value 3!

● x = sum_two_numbers(1,2)

Classes and Objects

Objects are simply variables and functions encapsulated into one single entity. Each object gets it functions and its variables from a class, and these are simply a template with which to create an object. A basic class would look something like:

● class MyClass:

● variable = "blah"

●  

● def function(self):

● print "This is a message inside the class."

In order to assign this class to a specific object, you would do this:

● myobjectx = MyClass()

The variable named “MyObjectx” now holds a class object that came from “MyClass”. This contains a variable and function that ae defined inside the “MyClass” class.

Accessing Object Variables

In order to access the variable that is inside the new object named “MyObject”, you would need to do this:

● myobjectx.variable

So, the following would prduce the string “blah”:

● print myobjectx.variable

It is possible to create many objects that are the same class, i.e., they have the same functions and variables defined. However, each one would contain an independent copy of the variables that are defined in the class. For example, if you were to define a different object using the “MyClass” class, and then change the string in the variable we used in the example above:

● myobjecty = MyClass()

● myobjecty.variable = "yackity"

And then print both of the values:

● print myobjectx.variable   # This would print "blah".

● print myobjecty.variable   # This would print "yackity".

Accessing Object Functions

If you want to access an object function, you would use notation that is similar to that used in accessing a variable:

● myobjectx.function()

●  

Printing that message would give you “This is a message inside the class”.

Modules and Packages

All a Python module is is a Python file that has the .py extension that implements a set of functions. A module is imported from another module by using the import command. 

The first time you load a module into a running script, it will initialized by the execution of the code inside the module. This is done just once. If another module that is in your code imports that same module, it will only be loaded once, not twice. The local variables that are inside the module act as “singletons” and are only initialized the first time.

If you wanted to import the module called urllib, a module that allows you to create read data from a URL, you would do this:

● # import the library

● import urllib

● # use it

● urllib.urlopen(...)

Exploring built-in modules

There are two important functions that are incredibly handy when it comes to exploring modules that are built in to Python – the dir and help functions. You can use the dir function to look for functions that are implemented in each module:

● >>> import urllib

● >>> dir(urllib)

● ['ContentTooShortError', 'FancyURLopener', 'MAXFTPCACHE', 'URLopener', '__all__', '__builtins__', '__doc__', '__file__', '__name__', '__package__', '__version__', '_ftperrors', '_get_proxies', '_get_proxy_settings', '_have_ssl', '_hexdig', '_hextochr', '_hostprog', '_is_unicode', '_localhost', '_noheaders', '_nportprog', '_passwdprog', '_portprog', '_queryprog', '_safe_map', '_safe_quoters', '_tagprog', '_thishost', '_typeprog', '_urlopener', '_userprog', '_valueprog', 'addbase', 'addclosehook', 'addinfo', 'addinfourl', 'always_safe', 'basejoin', 'c', 'ftpcache', 'ftperrors', 'ftpwrapper', 'getproxies', 'getproxies_environment', 'getproxies_macosx_sysconf', 'i', 'localhost', 'main', 'noheaders', 'os', 'pathname2url', 'proxy_bypass', 'proxy_bypass_environment', 'proxy_bypass_macosx_sysconf', 'quote', 'quote_plus', 'reporthook', 'socket', 'splitattr', 'splithost', 'splitnport', 'splitpasswd', 'splitport', 'splitquery', 'splittag', 'splittype', 'splituser', 'splitvalue', 'ssl', 'string', 'sys', 'test', 'test1', 'thishost', 'time', 'toBytes', 'unquote', 'unquote_plus', 'unwrap', 'url2pathname', 'urlcleanup', 'urlencode', 'urlopen', 'urlretrieve']

When you locate the function in the module that you want to use, you can read more about it by using the help function, in the interpreter:

● help(urllib.urlopen)

Writing Modules

It is a very simple task to write a Python module. All you do is create a .py file that is named after the module name and then use the Python name to import it (without using the .py extension) by using the import command.

Writing Packages

A package is a namespace, which includes a number of modules and packages. They are directories with a twist. Each Python package is a directory that has to contain a special file, named _ini_.py. The file itself can be empty merely indicating that the directory in it is a Python package – that way it can be imported in the way you would import a module.

If you were to create a directory that is named foo, which would mark the name of the package, you can create a module within that package that you could call bar. Don’t forget that you need to add the _init_.py file to the foo directory as well. In order to use the module called bar, you can import it on one of two ways:

● import foo.bar, OR

● from foo import bar

If you use the first way, you have to use the prefix foo whenever you access bar. But, in the second method, you don’t need to do this because you are importing the module itself to the namespace.

You can also use the _init_.py file to determine which modules the package is going to export as the API, while you keep the other modules internal by overriding the variable all – an example:

● __init__.py:

● __all__ = ["bar"]

MySQL Python Tutorial

For the final chapter, I want to talk to you about how to program, using Python, for the MySQL database. I will cover the basics of Python programming, using the MySQL dB module.

About the MySQL Database

MySQL is one of the best database management systems around. A multi-user system, it is very popular on the internet and is available for use on most of the biggest operating system platforms. As well as Windows, it will run on Linux, BSD UNIX ad on the Mac OS. Large well-known websites, like YouTube ad Wikipedia use MySQL, and these are sites that can manage millions of queries per day.

Before We Begin

You will need to install a number of packages in order to run these examples on your computer, starting with MySQL, if you haven’t already installed it.

From your command prompt, type in this:

● $ sudo apt-get install mysql-server

This will install the MySQL server and a number of other packages. While you are installing it, you will be prompted to put in a password for the MySQL root account:

● $ apt-cache search MySQLdb

● python-mysqldb - A Python interface to MySQL

● python-mysqldb-dbg - A Python interface to MySQL (debug extension)

● bibus - bibliographic database

● eikazo - graphical frontend for SANE designed for mass-scanning

At this stage, we do not know what the MySQLdb module package name is so we can use the following command to find out what it is:

● $ sudo apt-get install python-mysqldb

Now it’s time to create a brand new database user along with the new database:

● $ mysql -u root -p

● Enter password:

● Welcome to the MySQL monitor.  Commands end with ; or \g.

● Your MySQL connection id is 30

● Server version: 5.0.67-0ubuntu6 (Ubuntu)

Type 'help;' or '\h' for help.

Type '\c' to clear the buffer.

● mysql> SHOW DATABASES;

● Database          

● information_schema 

● mysql              

● 2 rows in set (0.00 sec)

Using the root account, we can connect to the database. To show all of the available databases, simply type Show Databases at the command prompt.

● mysql> CREATE DATABASE testdb;

● Query OK, 1 row affected (0.02 sec)

We can now create a testdb database and this what you are going to use throughout this chapter

● mysql> CREATE USER 'testuser'@'localhost' IDENTIFIED BY 'test623';

● Query OK, 0 rows affected (0.00 sec)

● mysql> USE testdb;

● Database changed

● mysql> GRANT ALL ON testdb.* TO 'testuser'@'localhost';

● Query OK, 0 rows affected (0.00 sec)

● mysql> quit;

● Bye

Next, you need to create a new user and you are going to give that user all privileges for all tables that are within the testdb database

We create a new database user. We grant all privileges to this user for all tables of the testdbdatabase.

The –MySQL Module

This is what will implement the C API for MySQL and it is not compatible at all with the DB API interface in Python. Most programmers prefer to use the MySQL module because it is object oriented so that is one we are going to use here. The following is an example using the –mysql Module:

● #!/usr/bin/python

● # -*- coding: utf-8 -*-

●  

● import _mysql

● import sys

●  

● try:

●     con = _mysql.connect('localhost', 'testuser', 'test623', 'testdb')

●     con.query("SELECT VERSION()")

●     result = con.use_result()

●     print "MySQL version: %s" % \

●         result.fetch_row()[0]

● except _mysql.Error, e:

●     print "Error %d: %s" % (e.args[0], e.args[1])

●     sys.exit(1)

●  

● finally:

●     if con:

●         con.close()

As you can see, this example will do two things – get and print the MySQL database version. To do this, you use the statement SELECT VERSION ().

Mysqldb Module

MySQLdb is a wraparound for Python and it is compatible with the DB API, thus making the code far more portable. This is the best and most preferred method of working with MySQL

Examples.

In the first example, we are going to retrieve the MySQL database version:

● #!/usr/bin/python

● # -*- coding: utf-8 -*-

● import MySQLdb as mdb

● import sys

● try:

●     con = mdb.connect('localhost', 'testuser', 'test623', 'testdb');

●     cur = con.cursor()

●     cur.execute("SELECT VERSION()")

●     ver = cur.fetchone()

●     print "Database version : %s " % ver

● except mdb.Error, e:

●     print "Error %d: %s" % (e.args[0],e.args[1])

●     sys.exit(1)

● finally:   

●     if con:   

●         con.close()

As you can see from the script, we are connecting to the testdb database and are then executing the statement SELECT VERSION(). This will give us the current version of the database and then we print it so it shows up on your window.

● import MySQLdb as mdb

The next command is importing the module

● con = mdb.connect('localhost', 'testuser',

●     'test623', 'testdb');

Now we can connect to the database using the connect() method, which has four different parameters:

● The host – this is where the MySQL database is located

● Databse User Name

● Users Acount Password

● Database name

The following example shows this:

● cur = con.cursor()

● cur.execute("SELECT VERSION()")

The connection gives us the cursor object, which is then used to travel around the records we got from the results set. We then call the execute() method and execute the SQL statement

● ver = cur.fetchone()

The data is fetched and, as we have only retrieved a single record, we use the fetchone() method

● print "Database version : %s " % ver

We can then print the retrieved data to the window

● except mdb.Error, e:

●     print "Error %d: %s" % (e.args[0],e.args[1])

●     sys.exit(1)

The next step is to check for any errors, an important step because working with databases is very prone to errors.

● finally:   

●     if con:   

●         con.close()

In the last step, we can release the resources, resulting in something that might look something like:

● $ ./version.py

● Database version : 5.5.9

Creating and Populating a Table

We will now create a table and put some data into it, or populate it, as it is known:

● #!/usr/bin/python

● # -*- coding: utf-8 -*-

● import MySQLdb as mdb

● con = mdb.connect('localhost', 'testuser', 'test623', 'testdb');

● with con:

●     cur = con.cursor()

●     cur.execute("DROP TABLE IF EXISTS Writers")

●     cur.execute("CREATE TABLE Writers(Id INT PRIMARY KEY AUTO_INCREMENT, \

●                  Name VARCHAR(25))")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Jack London')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Honore de Balzac')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Lion Feuchtwanger')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Emile Zola')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Truman Capote')")

We have created a table of authors and added in the names of 5 writers

● with con:

Using the with keyword, the interpreter will automatically release those resources as well as carrying out error handling

● cur.execute("CREATE TABLE Writers(Id INT PRIMARY KEY AUTO_INCREMENT, \

● Name VARCHAR(25))")

The above SQL statement will create a brand new database table that is called writers. There are two columns in the table – ID and Name

● cur.execute("INSERT INTO Writers(Name) VALUES('Jack London')")

● cur.execute("INSERT INTO Writers(Name) VALUES('Honore de Balzac')")

● ...

To insert new authors into the table, we use the INSERT statement and add two more rows:

● mysql> SELECT * FROM Writers;

● +----+-------------------+

● | Id | Name              |

● +----+-------------------+

● |  1 | Jack London       |

● |  2 | Honore de Balzac  |

● |  3 | Lion Feuchtwanger |

● |  4 | Emile Zola        |

● |  5 | Truman Capote     |

● +----+-------------------+

● 5 rows in set (0.00 sec)

After the script has been executed, we can use the mysql client tool and select all the data from that table.

Retrieving Data

Now that we have put some data in the database, it’s time to retrieve it:

● #!/usr/bin/python

● # -*- coding: utf-8 -*-

● import MySQLdb as mdb

● con = mdb.connect('localhost', 'testuser', 'test623', 'testdb');

● with con:

●     cur = con.cursor()

●     cur.execute("SELECT * FROM Writers")

●     rows = cur.fetchall()

●     for row in rows:

●         print row

The above example shows you how to retrieve all of the data from the table called Writers.

● cur.execute("SELECT * FROM Writers")

This statement selects all of the data from that table.

● rows = cur.fetchall()

We use the fetchall() method to retrieve all records, which are returned in a result set.

● for row in rows:

●     print row

We can now print, row by row, all of the data to the window.

● $ ./retrieve.py

● (1L, 'Jack London')

● (2L, 'Honore de Balzac')

● (3L, 'Lion Feuchtwanger')

● (4L, 'Emile Zola')

● (5L, 'Truman Capote')

It isn’t always going to be possible to retrieve all of the data at the same time so, instead, we would fetch each row, one at a time.

● #!/usr/bin/python

● # -*- coding: utf-8 -*-

● import MySQLdb as mdb

● con = mdb.connect('localhost', 'testuser', 'test623', 'testdb');

● with con:

●     cur = con.cursor()

●     cur.execute("SELECT * FROM Writers")

●     for i in range(cur.rowcount):

●         row = cur.fetchone()

●         print row[0], row[1]

Again, we can print the data from the table and fetch each row one at a time.

● for i in range(cur.rowcount):

●     row = cur.fetchone()

●     print row[0], row[1]

We use the fetchone() method to get each row and the rowcount property will show the total number of rows that the SQL statement returns.

● $ ./retrieve2.py

● 1 Jack London

● 2 Honore de Balzac

● 3 Lion Feuchtwanger

● 4 Emile Zola

● 5 Truman Capote

The above shows the output from the example

The Dictionary Cursor

In the MySQLdb module, there are a number of cursor types. The default one returns data in a tuple of tuples. The dictionary cursor sends the data in the format of a dictionary, allowing us to refer to the data by the name of the columns:

● #!/usr/bin/python

● # -*- coding: utf-8 -*-

● import MySQLdb as mdb

● con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')

● with con:

●     cur = con.cursor(mdb.cursors.DictCursor)

●     cur.execute("SELECT * FROM Writers LIMIT 4")

●     rows = cur.fetchall()

●     for row in rows:

●         print row["Id"], row["Name"]

In the above example, you can see that we use the dictionary cursor to retrieve the first four rows from the table called Writers. Broken down, the example looks like:

● cur = con.cursor(mdb.cursors.DictCursor)

The DictCursor is used

● cur.execute("SELECT * FROM Writers LIMIT 4")

We use it to bring in four rows from the table.

● for row in rows:

● print row["Id"], row["Name"]

The data is referred to by the names of the columns in the table.

● $ ./dictcur.py

● 1 Jack London

● 2 Honore de Balzac

● 3 Lion Feuchtwanger

● 4 Emile Zola

The above is an example of the output.

Column Headers

Next, we will look at how to print the column headers, with the data, from the table in the database

● #!/usr/bin/python

● # -*- coding: utf-8 -*-

● import MySQLdb as mdb

● con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')

● with con:

●     cur = con.cursor()

●     cur.execute("SELECT * FROM Writers LIMIT 5")

●  

●     rows = cur.fetchall()

●  

●     desc = cur.description

●  

●     print "%s %3s" % (desc[0][0], desc[1][0])

●  

●     for row in rows:   

●         print "%2s %3s" % row

Once again, we can print the contents of the table to the window and, this time, we are including the column names as well. These are called “meta data” and are obtained from the cursor object

● desc = cur.description

We use a description attribute to return the information from each column

● print "%s %3s" % (desc[0][0], desc[1][0])

●  

And then we print and format the names of the columns

● for row in rows:   

●     print "%2s %3s" % row

The data is traversed and printed

● $ ./columnheaders.py

● Id Name

● 1 Jack London

● 2 Honore de Balzac

● 3 Lion Feuchtwanger

● 4 Emile Zola

● 5 Truman Capote

The above is the output from the script.

Prepared Statements

Now let’s look at prepared statements. When we write one of these, we use a placeholder instead of writing in the values. Prepared statements increase both performance and security and the Python DB gives you five different ways to build a prepared statement. One of those ways, the ANSI print format code, is supported by the MySQLdb module.

● #!/usr/bin/python

● # -*- coding: utf-8 -*-

●  

● import MySQLdb as mdb

●  

● con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')

● with con:   

●  

●     cur = con.cursor()

●     cur.execute("UPDATE Writers SET Name = %s WHERE Id = %s",

●         ("Guy de Maupasant", "4"))       

●     print "Number of rows updated:",  cur.rowcount

Let’s change an author name, the one on row 4:

● cur.execute("UPDATE Writers SET Name = %s WHERE Id = %s",

●     ("Guy de Maupasant", "4"))  

In this, we have used to placeholders, both identified by the %s markers. The values are bound to the placeholder before the SQL statement is executed.

● $ ./prepared.py

● Number of rows updated: 1

One row has been updated

● mysql> SELECT Name FROM Writers WHERE Id=4;

● +------------------+

● | Name             |

● +------------------+

● | Guy de Maupasant |

● +------------------+

● 1 row in set (0.00 sec)

We have change the name of the author on row 4.

Inserting Images

Sometimes you might want to put an image into your database. Not everyone recommends that you do this because images are known as binary data, However, MySQL database has a specific datatype that we use to store binary, called BLOB (Binary Large Object). Other variants are TINYBLOB, LONGBLOB and MEDIUMBLOB.

● mysql> CREATE TABLE Images(Id INT PRIMARY KEY, Data MEDIUMBLOB);

● Query OK, 0 rows affected (0.08 sec)

We have created a new table that we have called Images.

● #!/usr/bin/python

● # -*- coding: utf-8 -*-

● import MySQLdb as mdb

● def read_image():

●     fin = open("woman.jpg")   

●     img = fin.read()

●     return img

● con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')

● with con:

●     cur = con.cursor()

●     data = read_image()

●     cur.execute("INSERT INTO Images VALUES(1, %s)", (data, ))

In the script above, we have read a .JPG file from a disk and put it into the table called Images.

● def read_image():

●     fin = open("woman.jpg")   

●     img = fin.read()

●     return img

The read_image() method is used to read binary data from the .JPG file, which is located in the directory that we are currently working in

● cur.execute("INSERT INTO Images VALUES(1, %s)", (data, ))

The image has been successfully inserted into the table.

Reading Images

We now know how to insert an image into a table but how do we read that image back?

● #!/usr/bin/python

● # -*- coding: utf-8 -*-

● import MySQLdb as mdb

● def writeImage(data):

●     fout = open('woman2.jpg', 'wb')

●     with fout:

●         fout.write(data)

● con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')

●  

● with con:

●     cur = con.cursor()

●     cur.execute("SELECT Data FROM Images WHERE Id=1")

●     data = cur.fetchone()[0]

●     writeImage(data)   

The above script shows that we read a file from the images table

● cur.execute("SELECT Data FROM Images WHERE Id=1")

We have selected one record from the table.

● fout = open('woman2.jpg', 'wb')

Now we open a writable binary file.

● fout.write(data)

And we write that data to the disk.

You should now have an image titled woman2.jpg in the current directory and we can look to see if it is the right one, the one you inserted in the last example.

Transaction Support

Transactions are atomic units of database operations against the data in either one or several different databases. The effect of the SQL statements in each transaction and these can be rolled back or committed to that database.

If a database supports a transaction, Python will automatically – and silently – start a transaction as soon as the cursor is created. We use the commit () method for committing the updates that are made with that cursor and we use the rollback () method to roll them back, or discard them. Each of these methods will start a new transaction.

MySQL database includes several different storage engine types, the most common of which are MyISAM and InnoDB. InnoDB is now the default engine although there is some tradeoff between speed and security. The MyISAM tables process much faster and offer no support for transactions. The rollback () and commit () methods are not implemented and do not do anything. However, the InnoDB table are infinitely more secure against the loss of data, and they support transactions, although they are slower to process.

● #!/usr/bin/python

● # -*- coding: utf-8 -*-

● import MySQLdb as mdb

● import sys

● try:

●     con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')

●     cur = con.cursor()

●     cur.execute("DROP TABLE IF EXISTS Writers")

●     cur.execute("CREATE TABLE Writers(Id INT PRIMARY KEY AUTO_INCREMENT, \

●                  Name VARCHAR(25)) ENGINE=INNODB")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Jack London')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Honore de Balzac')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Lion Feuchtwanger')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Emile Zola')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Truman Capote')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Terry Pratchett')")

●     con.commit()

● except mdb.Error, e:

●     if con:

●         con.rollback()

●     print "Error %d: %s" % (e.args[0],e.args[1])

●     sys.exit(1)

● finally:   

●     if con:   

●         con.close()

The writers table has been recreated and we are now going to work explicitly with transactions.

● cur = con.cursor()

The BEGIN statement is not called to start a transaction in the Python DB API. Instead, the transaction is started as soon as the cursor is created.

● cur.execute("CREATE TABLE Writers(Id INT PRIMARY KEY AUTO_INCREMENT, \

●                 Name VARCHAR(25)) ENGINE=INNODB")

In this one, we are looking at an InnoDB table type – if you are using an older version of MySQL, you will need to specify the engine type.

● con.commit ()

The transaction must be ended with one of two things – a commit () or a rollback () method. If you place a comment on this line, dented by the hash (#) symbol, the table will still be created but the data will not be written to it.

So far, we have been working with transactions but have not explicitly stated it. Instead we used context managers, which handle both the entry and exit from the runtime context, when the code block is executed. The context manager is usually invoked with the use of the with statement.

You can use connection objects as context managers in MySqldb. These will automatically rollback or commit the transactions and will also clean the code by eliminating the try, finally and except statements.

● #!/usr/bin/python

● # -*- coding: utf-8 -*-

● import MySQLdb as mdb

● con = mdb.connect('localhost', 'testuser', 'test623', 'testdb')

● with con:

●     cur = con.cursor()

●     cur.execute("DROP TABLE IF EXISTS Writers")

●     cur.execute("CREATE TABLE Writers(Id INT PRIMARY KEY AUTO_INCREMENT, \

●                  Name VARCHAR(25))")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Jack London')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Honore de Balzac')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Lion Feuchtwanger')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Emile Zola')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Truman Capote')")

●     cur.execute("INSERT INTO Writers(Name) VALUES('Terry Pratchett')")

In the above example, the context manager has dealt with all of the world that is needed for error handling and has automatically committed or rolled back a transaction.

Conclusion

Python is a nice language to use, very easy to read and to understand, While it may look complicated, it isn’t and, once you get the hang of it, you can spend hours creating simple programs, before you move on to the more complex ones.

When you are ready to move on to more advanced programming with Python, you will find plenty of information on the internet to help you. In the meantime, take some time to get to grips with using Python on Windows 10 and, above all, enjoy it!

Thanks you for downloading my book. If you found it helpful, please consider leaving me a review at Amazon.com

[→](http://www.amazon.com/gp/product-reviews/B013L09EC0) [Click here to leave a review on Amazon](http://www.amazon.com/gp/product-reviews/B013L09EC0)