![](d2d_images/cover.jpg)

While every precaution has been taken in the preparation of this book, the publisher assumes no responsibility for errors or omissions, or for damages resulting from the use of the information contained herein.

PYTHON: BEGINNER'S GUIDE TO PROGRAMMING CODE WITH PYTHON

**First edition. November 17, 2016.**

Copyright © 2016 Charlie Masterson.

ISBN: 978-1386290735

Written by Charlie Masterson.

10 9 8 7 6 5 4 3 2 1

Python:

Beginner’s Guide to

Programming Code

with Python

Charlie Masterson

# Table of Contents

[Introduction](#c003.xhtml_introduction)

[Chapter 1: Hatching Your Python](#c004.xhtml_chapter1)

[Chapter 2: Python Variables, Math, and Comments](#c005.xhtml_chapter2)

[Chapter 3: Conditionals and Booleans](#c006.xhtml_chapter3)

[Chapter 4: Lists and Loops](#c007.xhtml_chapter4)

[Chapter 5: Functions](#c008.xhtml_chapter5)

[Chapter 6: File I/O](#c009.xhtml_chapter6)

[Chapter 7: String Manipulation](#c010.xhtml_chapter7)

[Chapter 8: Basic Object-Oriented Programming: Objects and Classes](#c011.xhtml_chapter8)

[Chapter 9: More on Object-Oriented Programming and Classes](#c012.xhtml_chapter9)

[Chapter 10: Book List Redux](#c013.xhtml_chapter10)

[Conclusion](#c014.xhtml_conclusion)

© Copyright 2017 by Charlie Masterson - All rights reserved.

The following Book is reproduced below with the goal of providing information that is as accurate and reliable as possible. Regardless, purchasing this Book can be seen as consent to the fact that both the publisher and the author of this book are in no way experts on the topics discussed within and that any recommendations or suggestions that are made herein are for entertainment purposes only. Professionals should be consulted as needed prior to undertaking any of the action endorsed herein.

This declaration is deemed fair and valid by both the American Bar Association and the Committee of Publishers Association and is legally binding throughout the United States.

Furthermore, the transmission, duplication or reproduction of any of the following work including specific information will be considered an illegal act irrespective of if it is done electronically or in print. This extends to creating a secondary or tertiary copy of the work or a recorded copy and is only allowed with express written consent from the Publisher. All additional right reserved.

The information in the following pages is broadly considered to be a truthful and accurate account of facts and as such any inattention, use or misuse of the information in question by the reader will render any resulting actions solely under their purview. There are no scenarios in which the publisher or the original author of this work can be in any fashion deemed liable for any hardship or damages that may befall them after undertaking information described herein.

Additionally, the information in the following pages is intended only for informational purposes and should thus be thought of as universal. As befitting its nature, it is presented without assurance regarding its prolonged validity or interim quality. Trademarks that are mentioned are done without written consent and can in no way be considered an endorsement from the trademark holder.

| ![image](d2d_images/chapter_title_corner_decoration_left.png) |  | ![image](d2d_images/chapter_title_corner_decoration_right.png) |

![image](d2d_images/chapter_title_above.png)

# Introduction

![image](d2d_images/chapter_title_below.png)

CONGRATULATIONS ON downloading Python: Beginner’s Guide to Programming Code with Python and thanks for doing so.

The following chapters will discuss the Python programming language, how to get started, and how to program in Python - starting at the most simple concepts and helping you to create real world applications by the end of the book.

I say it a lot near the end, but it’s only because it’s true: programming is the apex of self-expression for a great number of people. There are a great many things you can accomplish using Python, and an even greater number of things if you’re looking at the big picture of the all-encompassing everything of computers and programming.

We’re going to help you get set and get on the path to being the best programmer that you can possibly be. Even if you’re an absolute and total novice, you’ll find this book easy to comprehend and work through, as well as engaging enough to not be an absolute and total bore as some programming books can very much be.

All in all, there are many things to be said about Python, and we may just scratch the surface - but that surface will be enough to prepare you for any and everything you will encounter going forward in the language. 

That is to say, there are plenty of books on this subject on the market, thanks again for choosing this one! Every effort was made to ensure it is full of as much useful information as possible, please enjoy!

| ![image](d2d_images/chapter_title_corner_decoration_left.png) |  | ![image](d2d_images/chapter_title_corner_decoration_right.png) |

![image](d2d_images/chapter_title_above.png)

# Chapter 1:

# Hatching Your Python

![image](d2d_images/chapter_title_below.png)

PYTHON IS ONE OF THE most popular programming languages out there today, full stop. There are few languages as prolific as Python has become. Python is a beautiful and multi-purpose language which can be found everywhere from on web servers to running video games to being the powerhouse behind popular applications.

Learning Python is a huge boon to you as a person in several ways. The largest is, of course, you’re learning a programming language. Learning a programming language in general opens up a huge number of possibilities for the things which you can do with a computer. It can be a career skill and a hobby, too.

Python in particular is a fantastic language to learn because it can be used for a multitude of things. It’s simple enough for beginners to grasp easily and, though simple, it’s incredibly powerful.

In order to use Python, you need to set it up. You can set up Python on Windows, Mac, and Linux. For the purposes of this book, I personally will be using a Linux system, but the instructions should be relatively straightforward and apply to every operating system.

In order to set up Python, you first need to grab a text editor. Many will work and many are out there indeed: I personally will be using Atom, which you can download from the website atom.io. Notepad++ and Sublime Text are also fantastic options.

After you’ve got your text editor, you need to check to be sure you have Python installed. Go to your Terminal (or Powershell in Windows) and try to run the command python. If Python isn’t installed (it says something along the lines of command “python” not recognized), then you need to install it.

In order to install it, you need to go to Python.org and grab Python 2.7.12 for your respective platform.

After it’s installed, make sure it’s working again - it should be.

You’re going to be using your Terminal/PowerShell to navigate and execute files, so you need to know how to navigate using those. If you don’t know, I highly suggest doing a Google search on the topic. There are a ton of very simple tutorials on the subject, but for brevity’s sake, I’d like to avoid going to in-depth on extraneous things as such.

Now we’re going to work on writing and running your first program.

Go into your text editor and create a new file. Save it before you even start writing code, because then you’ll have access to syntax highlighting which will help you out a fair amount. You can save it under whatever name you’d like going forward, but for the purpose of this example, you need to save it as first.py.

In the text file, type the following:

print “hello world”

Then head back to your Terminal or PowerShell and navigate to where you saved the file.

Run it by the following command:

python first.py

What happens? It should run perfectly and print out “hello world” to the console.

Now let’s go back and change that text file a bit more. Let’s add a few lines.

print “hello world”

print “my name is [type your name here]“

print “it’s nice to meet you”

Save the file and execute it again. It should print across multiple lines.

Awesome! We’re done with your very first program. We’re going to be messing with this file a little in the coming chapters in order to teach you important fundamentals of Python.

| ![image](d2d_images/chapter_title_corner_decoration_left.png) |  | ![image](d2d_images/chapter_title_corner_decoration_right.png) |

![image](d2d_images/chapter_title_above.png)

# Chapter 2:

![image](d2d_images/chapter_title_below.png)

Python Variables, Math,

and Comments

WHEN YOU WERE YOUNGER, you probably took a basic algebra class where you’d have to work with equations like y = mx + b. You could actually fill in these letters with other values in order to give you y. These values were called variables.

Variables in programming are somewhat similar. Variables are ways to give a name to a value so that you can use it throughout your program. Variables aren’t restricted to numbers, though.

Go back to your first.py file and a few lines above your print statements, type the following, with your name in the quotations:

name = “John Doe”

Afterwards, go back to the line which says “My name is [your name]” and rewrite it to be the following:

print “my name is ” + name

Then save and run it in console. It should say “my name is “ along with whatever you wrote in the quotations. Go ahead and modify the string some more, add a y, do whatever you want to do to it really, then save and execute it again.

The way that variables work is that they store a value to a name. Python makes working with variables very, very easy compared to other languages. Since it’s a scripting language, it’s rather straightforward with the way that it allows you to type variables. Scripting languages are intended to have you up-and-running as soon as possible and waste as little time as possible, staying out of your way while you create your program.

The variable we just created is called a “string”, which is a set of characters. Every time you print something to the console, you’re printing out a string. If you’re only printing out string values, you can use the + in order to concatenate the strings, which is a fancy word meaning put them together. In order to properly include other kinds of variables in your code, however, you need to use a formatted string.

print “my name is %s” % name

There are a number of formatted types you can use, but for right now, just remember that:

%s-prints a string

%d-prints a base-10 number

%f-prints a float

%r-prints the raw data of the variable (used for debugging)

As I just implied, there are more kinds of variables beyond strings that you can use. Let’s do some work with numbers. Create a new script. I’m going to call mine fruit.py. In Atom, you do this by right-clicking the sidebar where your files are listed and clicking “New file”. When it prompts you for the path, you can simply type the file name.

Firstly, there’s a type of variable called an integer in other languages which is essentially a whole number. Let’s say that you had four apples and your friend had six apples, and you wanted to see how many apples you had altogether. You could type something along the lines of:

myApples = 4

friendApples = 6

totalApples = myApples + friendApples

The variable myApples would have the value of 4, while the variable friendApples would have the value of 6, and totalApples would take the value of the variable myApples added to friendApples.

You can check all of these values by typing some print commands below that.

print “I have %d apples.” % myApples

print “My friend has %d apples.” % friendApples

print “Together, we have %d apples.” % totalApples

Save and run. It should print out something along the lines of the following:

I have 4 apples.

My friend has 6 apples.

Together, we have 10 apples.

Let’s say you gained one more apple, maybe picked it off a tree or something, and now you have 5 apples. Can you think of how you would write this?

Type the following below your print statements.

print “I got one more apple!”

myApples = myApples + 1

print “I now have %d apples.” % myApples

print “Now we have %d apples altogether!” % totalApples

Save and run that file. You’ll notice there’s an error - you should have eleven apples altogether, but it says you’ve only got 10\. This is because you’d set the value of totalApples earlier when myApples was only 4, and you need to set it again.

Below your myApples = myApples + 1 statement, add:

totalApples = myApples + friendApples

That should fix any problems that you’ve got with your totalApples variable.

I should also make the distinction, since we’re formatting strings right now, that if you need to format a number of variables within a string, they need to go within parentheses. For example, if we wanted to combine line one and two into “I have x apples and my friend has y apples”, we would write the following in our code:

“I have %d apples and my friend has %d apples.” % (myApples, friendApples)

Additionally, while we’re dealing with numbers, we should probably talk about Python math. Python handles math expressions by way of something called operators.

The general operators are self-explanatory:

+-addition

—subtraction

*-multiplication

/-division

%-modulus (finds remainder)

**-exponentiation (2**4 is 2 to the power of 4)

//-floor division

Then there are assignment operators. To add 1 to myApples earlier, we typed “myApples = myApples + 1”. You can shorten this, though, to myApples += 1.

Assignment operators are as follows:

=-x = y

+= y-x = x + y

-= y-x = x - y

*= y-x = x * y

/= y-x = x / y

%= y-x = x % y

**= y-x = x ** y

//= y-x = x // y

You can use these to assign values to a given numeric variable and perform assignment operations.

In addition to those operators and variables, there’s also another type of variable called a boolean, which evaluates the truth of a statement.

These are statements are evaluated with comparison operators, which are as such:

x == y-x is equal to y

x != y-x is not equal to y

x > y-x is greater than y

x < y-x is less than y

x >= y-x is greater than or equal to y

x <= y-x is less than or equal to y

Let’s say that you and your friend got in an argument over who has more apples, and you were spitefully complaining to your text editor because you’re certain that you have more apples.

Create a new variable below your current chunk of code called “moreApples”.

Let’s set this to the truth of the expression “myApples is greater than friendApples”, like so:

moreApples = myApples > friendApples

Then below that, type the following:

print “My friend says he has more apples! That’s not even %r!“ % moreApples

Save the file and run from your terminal. The output should look like the following:

$ python fruit.py

I have  4  apples.

My friend has  6  apples.

Together, we have  10  apples.

I gained one more apple!

I now have  5  apples!

Now we have  11  apples altogether!

My friend says he has more apples. That's not even  False !

Ah... well, this is slightly embarrassing. But it’s right, it’s not false when your friend says he has more apples - perhaps you should relearn basic arithmetic before you get into arguments with your friends regarding the amounts of things.

So because the statement myApples > friendApples is false and your amount of apples isn’t actually greater than your friend’s apples, the variable moreApples stored the value False. If it were myApples < friendApples, then it would have stored the value True.

There’s one more type of variable called floating-point, which is essentially decimal numbers. This doesn’t fit terribly well into the idea of apples, but you’d declare a float variable like this:

percentageOfMyFriendThatRolfIsFollowingOurArgumentAboutApples = 0.3

You may be asking why Rolf is still .3 my friend after an argument about apples. Allow me to explain in code:

percentageOfMyFriendThatRolfIsFollowingOurArgumentAboutApples = 0.3

# Rolf is still 30% my friend because he let me borrow his truck to move.

Whoa! What’s this? Well, the technical name is an octothorpe, but it’s also called a “hash” and the “pound sign”. But it’s used to lead off comments in your code. Comments are parts of your code that the compiler ignores when it’s preparing your code to be read for the computer.

You can place these over and over and the compiler will ignore them - fantastic for mid-code poetry breaks.

print “Oh, what a beautiful morning!”

# Howl, by Allen Ginsberg

# I saw the best minds of my generation destroyed by madness,

# starving, hysterical, naked,

print “What a time to be alive!”

The compiler will only see the two print statements and ignore the society-questioning vitriol of 1950s Beat poetry. (Don’t actually take mid-code poetry breaks, it’s frowned upon.)

You can also use these after a line of code, and the compiler will ignore the rest of the line.

print “Rolf is my friend!” # just kidding

Comments, used sparingly, are a tool for absolute good and can help strangers (including yourself in the future when you stumble upon old code) to understand what you’re trying to get at with any given chunk of code.

Avoid, however, using them too often. Overuse of comments makes code nauseating to read, and code should generally be self-explanatory anyway.

One last thing while we’re working with print statements. We aren’t going to use it too much right now, but it will come up later, and it’s worth knowing: escape sequences. These are things you can use in Python in order to modify your text.

The first and foremost example is the newline escape sequence - “\n”. This is used to designate that a string has a line break. Try printing the following:

print “Hello\nworld\nHow are you?”

Save and run this program. It should print across multiple lines.

Another thing you can use is the \t escape sequence, which places a tab between two characters, or at the beginning of a line:

print “I have:\n\t%d boxes of strawberries,\n\t%d apples, \n\t and %d peaches.” % (2, 3, 4)

There are a few other escape characters. For example, if you need to write a single-quote or double-quote within a string, you have two options:

Encase the whole thing in triple quotes, like so:

“””He said “see you tomorrow,” and that’s all.”””

Or escape them, like so:

“He said \”see you tomorrow,\” and that’s all.”

The same goes for backslashes - you have to escape them. These are the primary ones you’ll be using, but a simple Google search will turn up the rest. They’re generally very niche and are only useful for certain situations specific to program debugging or something along those lines. As a novice programmer just trying to find your way around the language, you won’t find much use for them. That said, I won’t stifle you, and if you’re a creative or experimental person, you can probably get some fun results and outputs out of playing around with the other escape characters. By all means, do it.

To recap this chapter, we covered the essentials of variables and math. Those are massive pinnacles of programming, and it’s imperative that you understand them as much as possible if you’re really intending to go forward with programming because they make up the bulk of every major action your program will perform in one way or another. But with all of that done, it’s now time to jump into the wide, wide world of conditionals and loops, where you will start to be exposed to Python’s despotic indentation rules that are actually rather quaint.

| ![image](d2d_images/chapter_title_corner_decoration_left.png) |  | ![image](d2d_images/chapter_title_corner_decoration_right.png) |

![image](d2d_images/chapter_title_above.png)

# Chapter 3:

![image](d2d_images/chapter_title_below.png)

Conditionals and Booleans

EARLIER ON, WE TALKED about comparison operators and how they could be used to determine whether a statement within a language was true or false. This is where we get into one of the biggest concepts underlying any given program. If things were such that you always knew one thing or another, the world would be a very different place. However, this really isn’t the case, and there are times where you have to evaluate a situation, make a determination, and then make a decision regarding that condition.

These kinds of situations are often very serious and demand your utmost response. For example, if your friend Rolf, who doesn’t understand basic apple arithmetic, were trying to log into your computer, you would want it to tell him to go away. So how would we go about this? (We’re going to use our first command to accept user input in this script, so saddle in for that as well.)

Create a new script. Call it what you like - I’ll be calling mine login.py.

We want to create a few variables called username and password. Set username and password to anything that you want.

Ask the user to enter their username, like so:

userInput = raw_input(“What is your username? ”)

Now we’re going to work some magic and have Python decide whether they entered the described username or not.

if userInput == username:

userInput = raw_input(“Password? “)

else:

print “You entered the incorrect username.”

We’re going to get to the else part in a second, but for now, just save this and try to run it. Test it by entering the wrong username first, then run the program again and enter the correct username. If all goes well, you’ll see the proper responses.

Now let’s talk about what’s happening here.

This is called an if/else statement, and is the most basic form of conditional decision making within Python (and most programming languages, for that matter.)

What happens is that you give it a statement that it evaluates the truthfulness of a given statement and then takes action based off of whether or not the statement was true.

What is occurring in that chunk of code up there is that it’s evaluating whether or not userInput—which is the string that we just had the user enter—is the same as “username”. If it is, then it prompts the user for their password. If it isn’t, then it tells them that they entered the wrong username. Simple enough, right?

But we do have that personal vendetta against Mr. Rolf, so we should probably include that within our code. But how? I mean, we’ve already got a completed if statement, right?

Wrong! There’s another thing we can do, called an else if. Check this out:

if userInput == username:

userInput = raw_input(“Password? “)

elif userInput == “rolf” or userInput == “Rolf” or userInput == “ROLF”:

print “There is no room on this computer for Rolf.”

else:

print “You have entered the incorrect username.”

This evaluates the userInput to see if the username is “Rolf” or any variant thereof. String comparison is innately case-sensitive, so “ROlf” would not be equal to “ROLf”. How can we fix this?

Well, we can simultaneously fix the case-sensitivity issue and make the code more elegant by changing our else-if line to the following.

elif userInput.lower() == “rolf”:

This converts whatever the userInput variable is to lower-case. We can now simply compare it to lower-case “rolf” and the issue would be fixed.

You may have noticed the little “or”, and it might have caught you off guard. That’s called a boolean operator.

There are three primary boolean operators in Python: and, or, and not.

“And” is used to check two conditions and see if they both return true. If either returns false, then the whole thing returns false. So to use the apple values from the last script, if we were to write this:

if myApples == 5 and friendApples == 6:

It’d come back as true. However, if even one of those weren’t true, the whole thing would return false.

“Or” is similar, but it checks to see if either condition or expression is true. If even one is true, the whole thing comes back true.

“Not” checks to see if a boolean/condition/expression is not true. For the sake of illustration and exposition, you can actually put a single boolean variable into an if-statement, because an if statement only checks to see if whatever following it is true.

If you had a variable called “IAmCool” which is set to True, and you typed:

if IAmCool:

print “I am cool”

It would actually print “I am cool”, because the if-statement sees that as a true statement. Following?

Now, if IAmCool were set to False because the only thing stronger than your self-deprecating sense of humor is your will to teach yourself various programming languages, and you instead of “if IAmCool” typed this:

if not IAmCool:

print “I am not cool”

It would check to see if IAmCool were false.

So between if, else if, and else statements, you’ve got a pretty solid chunk of conditional decision making under wraps.

Let’s go back to that code we had just a moment ago.

if userInput == username:

userInput = raw_input(“Password? “)

elif userInput.lower() == “rolf”:

print “There is no room on this computer for Rolf.”

else:

print “You have entered the incorrect username.”

We got the username, and it was right. Where do we go from here?

This is where we start to utilize a concept known as nested conditional statements. You can put an if-statement within an if-statement!

This is your time to shine, friend. After prompting for the password, write another if-statement within that if-statement, as well as an else statement. You need to compare userInput to your variable password and see if they’re the same. If they are, you need to welcome the user; if they aren’t, you need to tell them that they’ve entered the wrong password.

By the end, your code should look like this:

if userInput == username:

userInput = raw_input("Password? ")

if userInput == password:

print "Welcome!"

else:

print "That's the wrong password."

elif [...]

If it does, then you succeeded.

| ![image](d2d_images/chapter_title_corner_decoration_left.png) |  | ![image](d2d_images/chapter_title_corner_decoration_right.png) |

![image](d2d_images/chapter_title_above.png)

# Chapter 4:

![image](d2d_images/chapter_title_below.png)

Lists and Loops

IT’S A LITTLE UNCOMMON to put these two concepts in the same chapter, but I’m trying to be brief and they really do go hand in hand.

We’ve talked about variables, sure. But variables can only hold a single value. What if you had multiple values that you wanted to put in something? This is where lists come in handy.

Lists in Python are very straightforward.

Let’s say that we wanted to create a list of our favorite TV shows. We could do this like so:

favoriteShows = [‘Breaking Bad’, ‘Narcos’, ‘House of Cards’]

These are all different elements in a list which starts counting at 0\. You can also access the lists rather simply.

If you were to type the following:

print favoriteShows[0]

Then it would print out the first element of the list, here being Breaking Bad.

You can also enter data into a list rather simply! Lists have a built in function called “append()” which allows you to add data to the list, like so:

listExample.append(raw_input())

This would take the user’s input and add it to the function. (It’s also an example of calling a function as an argument of a function, which makes no sense at all right now but hopefully will in the next chapter!)

You can actually declare empty lists to be used, as well. You’d do so by declaring the variable and setting it with empty brackets, like this:

emptyList = []

From here, you could add elements to the list and start to use it like you would any other list.

To move to the next portion of the lesson and get off the whole list tangent, we should talk about loops. Loops are an integral part of many programs. They serve a great many purposes, but at their most basic level they’re simply a way for a chunk of code within a program to repeat multiple times, most likely changing in one way or another each time.

There are three main kinds of loops in Python: while, for, and do...while. All of these have their own particular uses that they’re tailored for.

While loops are the most simple, they execute over and over for as long as a given condition still comes back as true, and that’s all there really is to it.

Observe the following code:

dogs = 0

while (dogs <= 10):

print “There are %d dogs in the yard!”

dogs += 1

print “Wow! That’s a lot of dogs!”

Can you guess what’s happening here? We declared a variable called dogs and we set it to 0\. We then started the while loop, giving it a condition. While the variable dogs is less than or equal to 10, we want to run this loop. Every iteration of this loop will print “There are x dogs in the yard!”, and the loop increments every single time.

For loops are similar to while loops, but they automatically increment over a set of data, such as the lists we were talking about earlier.

You don’t necessarily have to iterate over lists. Python has a built-in range function that lets you iterate through a certain number of variables. For example, a for loop iterating through range(5) would iterate 5 times, from 0 to 4\. Let’s use this to count to 5.

Here’s an example of that for loop:

for i in range(5):

print “%d” % (i + 1)

Simple enough, right? Not too hard at all. We can also iterate through lists like earlier. If we wanted to print out every TV show on our list from earlier, we could do something like:

print “My favorite shows are: “

for i in favoriteShows:

print “%s” % i

The i is what’s called a loop variable, and in Python, it assumes the type of whatever your list is made of. Since lists can hold mixed values (even at once), this is great and super important.

Let’s actually start working with this and combining a lot of the concepts that we’ve worked on.

Create a new file, call it what you like but I’m going to call mine bookList.py.

The first thing that we’re going to do is create an empty list of books and a boolean called running set to True.

bookList = []

running = True

Now what we’re going to do is create something called a running loop. This is to show you a way that while loops can be used.

We’re going to create a loop that runs for as long as the variable “running” is true.

while running == True:

The first thing we’re going to do within the loop is prompt the user to add a book, list the current books, or exit the program. We’re going to want to compare the response to other things, so we need to set it to a variable.

userInput = raw_input(“Book List v1.\nType \”add\” to add a book, \”list\” to list the books, or \”exit\” to exit the program: ”)

Now we need to parse the input and compare it. First, we’re going to see if the user wanted to add a book, and add a book if they did:

if userInput.lower() == “add”:

userInput = raw_input(“Enter the name of the book: \n”)

bookList.append(userInput)

Perfect. There’s actually a way to simplify that line by just passing the function “raw_input(‘...’)” to bookList.append, but I wanted to show you that you can append any variable to your list.

Now we’re going to determine what happens if the user entered “list”, which should be checking to see if the list is empty and printing out its contents if not:

elif userInput.lower() == “list”:

if not bookList: # this is shorthand for “if the bookList is empty”

print “The list is empty!\n”

else:

for i in bookList:

print “%s\n” % i # prints everything on the list

Now, if the user entered “exit”, we need to set the variable running to false so that we exit the main loop, since it’s only supposed to run while the variable running is true.

elif userInput.lower() == “exit”:

running = False

And lastly, if they entered anything but “add”, “list”, or “exit”, we need to print that their command was invalid.

else:

print “The command was invalid!\n”

This is the first major program we’ve done so far, but this is a very cursory introduction to variables, loops, and input/output.

From here on out, we’re going to be introducing concepts by working on this specific file, so you need to hold this file near and dear. 

| ![image](d2d_images/chapter_title_corner_decoration_left.png) |  | ![image](d2d_images/chapter_title_corner_decoration_right.png) |

![image](d2d_images/chapter_title_above.png)

# Chapter 5:

![image](d2d_images/chapter_title_below.png)

Functions

FUNCTIONS ARE AN INTEGRAL part of any given programming language. They supply a way to define something that’s supposed to happen and may have to happen many times or basic functions of the program in general, and reuse that chunk of code as often as you need to. They also allow you to modify existing values and work with variables that you already have.

The basic breakdown of a function in pseudocode is like this:

function(parameter1, parameter2, etc...) {

do things

}

And it will normally be called within your main portion of code or from other functions like so:

function(variable1, variable2)

Functions can be used to massively simplify abrasively verbose code and make it much easier to understand, while at the same time making it more modular and reusable.

So how do you work with functions in Python? They follow a very simple structure.

In order to declare a function in Python, you simply type:

def functionName(arguments):

code here

That’s really all that there is to it. The parameters that you define for a function can be used within the body of that function’s code. When you call the function later on, you can put any values of the same type in the place. The best way to explain it is that the parameters you use in your function definition are hypothetical, and are intended to be replaced with actual values.

If we wanted to code a function which was to take the length and width of a rectangle, find the area, and return that value, we could do it like this:

def findArea(length, width):

return length * width

You could then call this later in your code. You can use actual values, like so:

area = findArea(4, 6) # “area” would have the value of 24

Or you can use already existent variables in order to call the function.

l = 6

w = 3

area = findArea(l, w) # “area” would have the value of 18

You can even use other functions as arguments, since every function simply returns a value.

def add(number1, number2):

return number1 + number2

def findArea(length, width):

return length * width

area = findArea(4, add(2,2))

This code would first do the add function which would return the value 4, then multiply the return value of the add function by the first argument (4). It would ultimately return the value of 16.

So the question now is, how can we use functions in order to pretty up our existing code and make it more functional? Let’s go back to our bookList code. It’s perfectly functional, right? But looking at it is a mess. Let’s give functions to our addBook and listBook functions, and make them a little bit more, well, functional while we’re at it. 

So let’s look at the if statement for adding a book.

if userInput.lower() == “add”:

userInput = raw_input(“Enter the name of the book.\n”

bookList.append(userInput)

What we want to do is make this so it’s simpler, like so:

if userInput.lower90 == “add”:

addBook(bookList)

Here’s how we’d do this. Functions have to be declared and defined before you call them. You can do it anywhere before. I’m going to do it at the beginning right after our variableList.

def addBook(bList):

userInput = raw_input(“Enter the name of the book you’d like to add.\n”)

bList.append(userInput)

You could have named the variable bList anything, even bookList - the reason I didn’t name it bookList for simplicity’s sake is in order to drive home the point that function parameters are only hypothetical values that you replace with real values when you call them.

Now if we replace our current if-statement with this:

if userInput.lower() == “add”:

addBook(bookList)

It should work perfectly fine.

Now we need to add a function which will allow us to list the books. This is  going to be much the same: we need to send it our list, bookList, and have it read it off. First we need to define it. I’m putting it right after our last function:

def listBooks(listOfBooks):

Now we need to transfer our logic over.

def listBooks(listOfBooks):

if not listOfBooks:

print “The list is empty!\n”

else:

for i in listOfBooks:

print “%s\n” % i

After that, we can go back to our if-statement and replace the ugly code with the far more elegant:

elif userInput.lower() == “list”:

listBooks(bookList)

Save and run your code to ensure that it works. It should go just fine. By the end, it should look a bit like this:

bookList = []

running = True

def addBook(bList):

userInput = raw_input("Enter the name of the book you'd like to add.\n")

bList.append(userInput)

def listBooks(listOfBooks):

if not listOfBooks:

print "The list is empty!\n"

else:

for i in listOfBooks:

print "%s\n" % i

while running == True:

userInput = raw_input("Book List v1.\nType \"add\" to add a book, \"list\" to list the books, or \"exit\" to exit\n")

if userInput.lower() == "add":

addBook(bookList)

elif userInput.lower() == "list":

listBooks(bookList)

elif userInput.lower() == "exit":

running = False

else:

print "The command was invalid!\n"

Notice how much cleaner and easier to read that our primary code is, starting at the run loop and going to the end of the program.

| ![image](d2d_images/chapter_title_corner_decoration_left.png) |  | ![image](d2d_images/chapter_title_corner_decoration_right.png) |

![image](d2d_images/chapter_title_above.png)

# Chapter 6:

![image](d2d_images/chapter_title_below.png)

File I/O

ALRIGHT, LET’S PUT the bookList away for a second, we’ll come back to it momentarily after talking about file input/output and string manipulation, once we finally get to the chapter on object-oriented programming. For now, it’s time to talk about reading and writing files.

There’ll be many times in your programming career (or hobby) that you’ll need to read or write data to a file. There are a crazy amount of applications for this, as well. If you were designing a game, you could save your player’s progress. We could use it in our book list in order to export a list of books (intense foreshadowing.) Even the word processor I’m writing this on needs to export and import data from files constantly.

So how exactly do we do this in Python?

Python, like many other things, makes reading from and writing to a file relatively painless.

First what you’d have to do is open the file and give the value of said file to a variable, like so:

file1 = open(‘example’, mode)

Mode can be many things. w for writing to a file only, a for appending to existing files, r+ for reading and writing, and r to only be read. The mode part may be omitted, and if it is, then it will be assumed you are only reading the file.

Once the file is open, there are a few methods that you can use.

file1.read(size), where size is optional. If size is included, it will read size amount of data and return it as a string, which you could assign to a variable or print or whatever, really. If you exclude size, it will read over the entire file and return the entire thing.

file1.readline() reads only a single line from a file, which can be very useful for certain applications where you need to feed data into a list or something along those lines.

file1.write(string) will write the contents of the given string to the file. If you want to write something that isn’t a string, you’ll need to actually cast it to a string.

liters = 2

str(liters)

file1.write(liters + “\n”)

Or you’d have to do a format string, as such:

file1.write(“There are %d liters” % liters)

Both are perfectly viable ways of achieving the end goal here.

When you’re finished with a file, you always have to close it in order to free up system resources.

file1.close()

We’re going to work with this a bit more in-depth in chapter 10 when we finally finish working with string manipulation and object-oriented concepts and start to synthesize a lot of what we learned, but for now, feel free to experiment with these concepts and try to make something happen using them.

| ![image](d2d_images/chapter_title_corner_decoration_left.png) |  | ![image](d2d_images/chapter_title_corner_decoration_right.png) |

![image](d2d_images/chapter_title_above.png)

# Chapter 7:

![image](d2d_images/chapter_title_below.png)

String Manipulation

THERE WILL ALMOST CERTAINLY be times where you need to manipulate this string or that. Maybe you’ll need to get its length, or you’ll need to split it or make another string from it. Maybe you’ll need to read what character is at x position. Whatever the reason is, the point is that there’s a reason.

The reason that we’re getting into this so late into the book is that it opens us up to a broader discussion on the nature of objects that we’re going to go more in-depth within the next chapter, but in the meantime, we’re also going to be covering extremely useful methods that the Python language provides to be used with strings.

Go ahead and create a new file. As always, you can call it whatever you want. My file is going to be named strings.py. Uncreative name, sure, but we’re going to be getting creative with strings in this chapter, believe me.

So what is a string, really? Well, we obviously know that a string is a line of text, which goes without saying. But what goes into that?

We’ve spoken quite a bit in this list about lists. Lists are actually a form of another variable that’s largely eschewed in Python programming called an array. An array is a pre-allocated set of data that goes together, in the most basic terms of speaking.

Python comes from and is built upon a language called C. In C, there are actually data types. There are data types in Python, too, but Python saves the user time by setting the data type for the programmer instead of having the programmer declare it.

One of the data types in C was called a char, which was a single character. In terms of computer speak; there isn’t a native support for strings. Strings were simply arrays of characters. For example, if one wanted to make a string called “hello”, they would have done the following:

char hello[6] = { ‘h’, ‘e’, ‘l’, ‘l’, ‘o’, ‘\0’ };

Python, in its beautiful habit of maximum abstraction, keeps us from these complexities and lets us just declare:

hello = “hello”

The point is that strings, ultimately, are just sets of data. And like any set of data, they can be manipulated. There will be times, too, where we need to manipulate them.

The most simple form of string manipulation is the concept of concatenation. Concatenated strings are strings that are put together to form a new string. Concatenation is super easy - you simply use the + sign to literally add the strings together.

sentence = “My “ + “grandmother “ + “baked “ + “today.”

print sentence

#  would print “My grandmother baked today.”

The first thing to remember when working with string manipulation is that strings, like any set of data, starts counting at 0\. So the string “backpack” would count like so:

backpack

01234567

There are a few different things that we can do with this knowledge alone. The first is that we can extract a single letter from it.

Let’s say the string “backpack” were stored to a variable called backpack. We could extract the letter “p” from it by typing:

letter = backpack[4]

This would extract whatever the character at index 4 was in the string. Here, of course, it’s p.

If we wanted to extract the characters from “b” to “p”, we could do the following:

substring = backpack[ 0 : 4 ]

This would give the variable substring a string equal to the value of backpack’s 0 index to 4 index:

backpack

01234567

Substring, thus, would have the value of “backp”. Quite the word.

There are a few more things you can do with data sets, and strings specifically, in order to get more specific results.

backpack[start:4] would give you all characters from the start to index four, like just before.

backpack[4:end] would give you all characters from index 4 to the end.

backpack[:2] would give you the first two characters, while backpack[-2:] would give you the last two characters. backpack[2:] would give you everything but the first two characters, while backpack[:-2] would give you everything aside from the last two characters.

However, it goes beyond this simple kind of arithmetic.

String variables also have built-in functions called methods. We’ve already worked with these a bit in the last chapter when we were working with files. Most things in Python - or object-oriented languages in general, really - are forms of things called objects. These are essentially variable types that have entire sets of properties associated with them. Macrovariables which contain a large number of microvariables and microfunctions, if you will.

Every single string is an instance of the string class, thus making it a string object. The string class contains definitions for methods which every string object can access, as an instance of the string class.

For example, let’s create a bit of a heftier string.

tonguetwister = “Peter Piper picked a peck of pickled peppers”

The string class has a variety of built-in methods you can utilize in order to work with its objects.

Let’s take the split method. If you were to type:

splitList = tonguetwister.split(‘ ‘)

It would split the sentence at every space, giving you a list of each word. splitList, thus, would look a bit like this: [‘Peter’, ‘Piper’, ‘picked’, ‘a’, ‘peck’, ‘of’, ‘pickled’, ‘peppers’]. Printing splitList[1] would give you the value ‘Piper’.

There’s also the count method, which would count the number of a certain character. Typing:

tonguetwister.lower().count(‘p’)

You would get the number 9.

There’s the replace method, which will replace a given string with another. For example, if you typed:

tonguetwister = tonguetwister.replace(“peppers”, “potatoes”)

tonguetwister would now have the value of “Peter Piper picked a peck of pickled potatoes”.

There’s the strip, lstrip, and rstrip methods which take either a given character or whitespace off of both sides of the string. This is really useful when you’re trying to parse user input. Unstripped user input can lead to unnecessarily large data sets and even buggy code.

The last major one is the join method, which will put a certain character between every character in the string.

print “-”.join(tonguetwister)

would print “P-e-t-e-r-P-i-p-e-r-p-i-c-k-e-[...]”

There are also various boolean expressions which will return true or false. The startswith(character) and endswith(character) methods are two fantastic examples. If you were to type:

tonguetwister.startswith(“P”)

It would ultimately return true. However, if you were to type instead:

tonguetwister.startswith(“H”)

It would ultimately return false. These are used for internal evaluation of strings as well as for evaluating user input.

A few other examples are string.isalnum() which will see if all characters in the string are alphanumeric or if there are special characters, string.isalpha() which will see if all characters in the string are alphabetic, string.isdigit() which will check to see if the string is a digit or not, and string.isspace() which will check to see if the string is a space or not.

These are all extremely useful for parsing a given string and making determinations on what to do if the string is or isn’t a certain way. 

| ![image](d2d_images/chapter_title_corner_decoration_left.png) |  | ![image](d2d_images/chapter_title_corner_decoration_right.png) |

![image](d2d_images/chapter_title_above.png)

# Chapter 8:

![image](d2d_images/chapter_title_below.png)

Basic Object-Oriented Programming: Objects and Classes

PYTHON IS AN OBJECT-oriented programming language. In fact, most modern languages are. But what exactly does this mean? We’ve spoken in vague terms of objects and classes but we haven’t really established quite what this actually means in in any certain terms one way or another.

An object is an instance of a class. Most things you’ll deal with in Python are objects. Earlier, when we worked with file input and output, we created instances of a file class. In the last chapter, we were working with strings, and we created instances of the string class. Every instance has built in methods that it can access that are derived from the class definition itself. So what exactly is a class?

A class is a way of defining objects. This sounds terribly vague, but let’s look at it this way.

You likely have or have had a pet, right? Let’s say there’s a dog, and his name is Roscoe.

Well, Roscoe is an animal. Animals have broad, generally defined characteristics, but they’re all animals, much like Roscoe is an animal. Get comfy with Roscoe, because we’re going to be talking him a lot while we talk about the relations between classes and the relations between classes and objects.

We’ve established that Roscoe is most certainly an animal. He fits the definition of an animal. In this manner, Roscoe is a specific instance of the animal class. If you were writing a simulation of life, and you had people and animals, you would define Roscoe as an instance of animal, just as you declared variable file1 as an instance of file, or you declared tonguetwister as an instance of string.

Now, we need to talk about how we actually define a class and an object within Python.

Create a new file to work with, I’m calling mine pursuitOfRoscoe.py.

Within this file, we’re going to start right out the bat by defining a class.

To declare a class, you follow the following template:

class name(parent)

We’ll talk about parent classes in the next chapter. For now, let’s just make our animal class. Every class which isn’t deriving from another class has “object” as its parent, so let’s put that.

class Animal(object):

We’re on our way to defining Roscoe, now.  We need a way to define an animal. Let’s think about what most animals have. Most animals have legs, that’s a start. Animals also have Latin names. Let’s work with those two. If your class stores data, you generally need to have an initializer function within your class. It’s not a necessity, but it is very common practice.

class Animal(object):

def __init__(self, legs, name):

self.legs = legs

self.name = name

Perfect. Since Roscoe’s a dog, he’ll have 4 legs, and his species is Canis Lupus Familiaris.

With that in mind, we now have a definition for animal classes that can be used amongst many animals, not just Roscoe. That’s the entire idea behind classes: creating reusable data structures for any given object so that the code is more readable, easy to understand, cleaner, and portable, among other buzzword adjectives that are surprisingly very, very true.

How do we declare an instance of this class now? Like anything else!

roscoe = Animal(4, “Canis Lupus Familiaris”)

We can go in and change these variables too. Canis lupus is so formal, and Roscoe’s our buddy, so let’s change that to Roscoe.

roscoe.name = “Roscoe”

There we go. Much better.

Hopefully, this makes the distinction between classes and objects much clearer.

Roscoe is a dog, and an animal. Thus he takes from the common concept of being an animal. Since he’s an instance of an animal, he automatically receives the traits that all animals have. How cool is that?

Let’s go a bit further, and incorporate some functions. What’s something that every animal does? Sleep. Every single animal sleeps, aside from Ozzy Osborne.

Let’s give animals a function so that they can sleep.

Below our initializer, create a new function called sleep that takes the arguments of self and hours. Then print out a line of text that says the animal’s name and how long it’s sleeping for. My code ended up looking a bit like this, and hopefully yours will as well.

def sleep(self, hours):

print “%s is sleeping for %d hours!” % (self.name, hours)

Then below our declaration of Roscoe, let’s go ahead and run the “sleep” function with the argument of 4 hours.

roscoe = Animal(4, “canis lupus familiaris”)

roscoe.name = “Roscoe”

roscoe.sleep(4)

Save this and run it. If all goes well, it should print out “Roscoe is sleeping for 4 hours!”.

At this point you’ve got a cursory understanding of classes. We’ll go more in-depth with broad object oriented programming concepts and their applicability within Python in the next chapter.

| ![image](d2d_images/chapter_title_corner_decoration_left.png) |  | ![image](d2d_images/chapter_title_corner_decoration_right.png) |

![image](d2d_images/chapter_title_above.png)

# Chapter 9:

![image](d2d_images/chapter_title_below.png)

More on Object-Oriented Programming and Classes

THERE ARE A FEW VERY broad object-oriented concepts we’ve yet to cover, and this is because they require a far more in-depth explanation than I was willing to give in the same exact chapter that we began to talk about any of the concepts.

There are four primary concepts within object-oriented programming that we need to discuss more in-depth. These are inheritance, polymorphism, abstraction, and encapsulation. Python provides for all of these, and very well at that.

Inheritance is the notion of deriving a class and things from within that class into another child class. There’s a very simple way to explain this concept. Classes can break down into other more specific classes. For example, Roscoe is an animal. But he’s also a dog. A dog is a type of animal. Shouldn’t Roscoe be a dog and not an animal? Isn’t he both? How do we handle this?

Think of it this way: every dog is an animal, but not every animal is a dog. So we can break down the animal class even further. The way that we derive one class from another is by inheritance. Here’s how we’d declare a dog class which extends the animal class. All dogs have 4 legs aside (for the most part), so we can declare that ahead of time and manually change it if a dog ever doesn’t have 4 legs.

class Dog(Animal):

def __init__(self, name):

self.name = name

self.legs = 4

The way that this works is that the Dog class is an extension of the Animal class. The Dog class receives all the functions and variables of the dog class, so we don’t have to redefine them.

This also means that if we were to erase our first line and re-declare Roscoe more accurately as a dog, we could still declare sleep. Observe.

roscoe = Dog(“Roscoe”)

roscoe.sleep(4)

It should go without a hitch. However, the cool thing about child classes is that you can also give them their own functions that their parent can’t use. For example, animals don’t bark - dogs do. Let’s create a bark function in our dog class for practice’s sake.

def bark(self):

“%s says: Bark!” % self.name

Now let’s try to declare bark via Roscoe.

roscoe.bark()

It should print out exactly what we entered. To illustrate further, create an instance of parent class Animal, let’s call it “lion”:

lion = Animal(4, “panthera leo”)

Try to call the method bark by way of Lion.

lion.bark()

There should be an error. Why is this? Well, it’s because - as we said - every dog is an animal, but not every animal is a dog. The bark() function was defined in the Dog class but not in the Animal class, so instances of the Animal class can’t access this method at all.

The next concept of object-oriented programming is called “polymorphism”. This means that something has the property of being able to perform the same task as something else, but in a different way. There are two ways of achieving this: function overloading (performing a similar function/method but with different parameters) and function overriding (rewriting a function of a parent class so that it works better for your own class).

To illustrate this, let’s go back to our bark method. Under our bark method, we’re going to create another bark method, declared like this:

def bark(number):

print “%s just barked, %d times! How cute.” % (self.name, number)

Now we have two different forms of the bark function. If you declare

roscoe.bark()

You’re going to see “Roscoe says: Bark!”

But, if you declare

roscoe.bark(3)

You’ll see “Roscoe just barked, 3 times! How cute.”

This is the basic idea of function overloading and polymorphism in essence: giving multiple ways to do a similar thing.

This program is already adorable, but we can make it even more adorable while also learning more about Python coding and string manipulation. Go back to your bark(number) method, and change it so it looks like this:

barkString = “Bark! “ * number

print “%s just barked, %d times. How cute. %s) (self.name, number, barkString)

Now save and run. You can repeat a string multiple times by simply using the multiplication and giving how many times to multiply!

The next major concept of object-oriented programming languages is abstraction. This is the idea of hiding internal details and functionality, to be more forward and more safe for both the programmer and end user. Python shows this by having a very abstract interface compared to other languages and providing a large amount of functionality for you so you never have to get down to the nitty-gritty of what your computer is actually doing behind the scenes.

The last major concept of object-oriented languages is called encapsulation, wherein code and data is wrapped together into a single unit. The primary way that we can display this is by the notion of having a class - not only in Python, but anywhere. Using a class automatically wraps important data and functions together in one easily accessible and usable place. Other datas have something called access control where you can actually dictate what classes can and can’t access the data that you’re putting in your class. Class data in Python is by default public.

All in all, object-oriented programming isn’t very tough to grasp, but it’s full of concepts that stand for much bigger and larger things, and these are the concepts that can be difficult to understand and implement in the end.

Now we’re going to incorporate the concepts we’ve been going over in the past few chapters - string manipulation, file input/output, and classes - in the next one as a final way to work on and put together all of the concepts we’ve built up so far, making a program that will keep a list of books for the end user.

| ![image](d2d_images/chapter_title_corner_decoration_left.png) |  | ![image](d2d_images/chapter_title_corner_decoration_right.png) |

![image](d2d_images/chapter_title_above.png)

# Chapter 10:

![image](d2d_images/chapter_title_below.png)

Book List Redux

CONGRATS ON MAKING it this far. Programming is confusing at first. Now it’s time to combine the concepts we’ve learned and create a newer version of our book list program.

So let’s think about what we want this program to do.

I want this program to have five options:

1)  Add books to a temporary list

2)  List the temporary book list

3)  Read books from a file

4)  Write the temporary list to a new book file

5)  Write it to an existing file

6)  Clear the temporary list.

So let’s get started with this.

Let’s create a new file, I’m calling it bookkeeper.py, because I’m a programmer in 2016 and the modus operandi is using trendy catchy names.

In this file, the first thing we want to do is create a class called book.

class book(object):

def __init__(self, title, author):

self.title = title

self.author = author

Now we need to start making our functions. The first function, addBook, is going to create a new instance of the book class and add it to our list of books.

def addBook(bookList):

title = raw_input(“What is the name of the book?”)

author = raw_input(“What is the author’s name?”)

bookList.append(book(title.upper(), author.title()))

The reason that we put author.title() is because the string.title() method manipulates a string such that every first word is capitalized, much like a title.

Afterwards, we need a function in order to list the books. We’ll pass to it a list of books.

def listBook(bookList):

for i in bookList:

print “\”%s\”, by %s\n” % (i.title, i.author)

This will loop through every book in book list and print out their title and author, accessing their respective properties.

This is where things get pretty fun. We need to create a function in order to read books from a file. Additionally, we’re going to give people the option to add it to their temporary book list. We’ll start by declaring the function and then passing the list of books.

def readBooks(bookList):

Then we’re going to declare a second temporary list within the function that we’re going to save every book in the file to.

bList = []

After this, we open the file for reading. We need to prompt the user for the filename. We’ll do that like so:

f = open(raw_input(“ Enter the filename.”))

Now, we’re going to iterate through every line in this file. There’s a handy built-in functionality for this in Python using for loops. We’re going to then use our string method string.find() in order to locate the comma in the line and divide the line of text there into a title and an author, by creating two substrings. Each of these substrings will need to be stripped - the first of the comma, and the second of whitespace. After this, we’re going to append the book to the function’s book list, printing out each line as we go. A bit of a complicated set of code, but it’ll explain itself.

for line in f:

comma = line.find(“,”)

title = line[0:comma].rstrip(‘,’) #substring 1

author = line[comma+1:].strip() #substring 2

bList.append(book(title.upper(), author.title()))

print “%s, %s” % (title.upper(), author.title())

Next, we prompt the user, asking if they want to add the results to their temporary list. If they say yes, we iterate through bList, appending each book to bookList. Otherwise, we just tell them it wasn’t saved and close the file.

if userInput == “yes”:

for i in bList:

bookList.append(i)

print “Saved.”

else:

print “Not saved.”

f.close()

That brings an end to our readBooks method.

Now it’s time to get to our writeToNew method.

First we define it, then ask the user to name the file. We then open the file, iterate through a book list while writing the contents to that file, then close it.

def writeToNew(bookList):

userInput = raw_input(“ Enter the filename you’d like to export to.”)

f = open(userInput, ‘w’) # the w indicates that we’d like to write

for i in bookList:

f.write(“%s, %s\n” % (i.title.upper(), i.author.title()))

f.close()

Now we need to create the “write to existing file” method. It’s simple enough. Ultimately, it’s very similar to the last function, but we change an essential argument.

def writeToExisting(bookList):

userInput = raw_input(“ Enter the file you’d like to add to.”)

f = open(userInput, ‘a’) # using a instead of w tells it we’ll be appending a file, rather than writing a new one

for i in bookList:

f.write(“%s, %s\n” % (i.title.upper(), i.author.title()))

Those are the primary functions that needed to be written. Now it’s time to move on to the actual bulk of our code.

First we define our bookList and our running boolean.

bookList = []

running = True

Now we start our while loop. The last program was very messy. Let’s clean it up a bit.

First, we’re going to create a much prettier menu:

while running == True:

print “Welcome to BOOKKEEPER. Type:”

print “\t\”ADD\” to add a book to your temp list.”

print”\t\”LIST\” to read out your temp list.”

print “\t\”READ\” to read an existing file.”

print “\t\”SAVE NEW\” to save to a new file.”

print “\t\”SAVE EXISTING\” to save to an existing file.”

print “\t\”CLEAR\” to clear your temporary list.”

print “\t\”EXIT\” to exit.”

Already, our menu is looking much prettier and more organized than it was. A tab space before each option really spruces it up.  Now it’s time to actually accept the user input and make decisions. You simply call every function, sending them bookList, until you get to the “clear” option. When you get to the “clear” variation, you’ve simply got to reset bookList to be empty by re-declaring it as empty. This is really pretty straightforward.

userInput = raw_input()

if userInput.lower() == “add”:

addBook(bookList)

elif userInput.lower() == “list”:

listBook(bookList)

elif userInput.lower() == “read”:

readBooks(bookList)

elif userInput.lower() == “save new”:

writeToNew(bookList)

elif userInput.lower() == “save existing”:

writeToExisting(bookList)

elif userInput.lower() == “clear”:

bookList = []

elif userInput.lower() == “exit”:

running = False

else:

print “The command was invalid!\n\n”

That brings an end to our program. It’s far easier to understand and grasp than the former, and is far more fleshed out. Python is pretty forgiving structurally, but just to be sure, here’s how the program looks for me. Feel free to compare yours:

class book(object):

def __init__(self, title, author):

self.title = title

self.author = author

def addBook(bookList):

title = raw_input("What is the name of the book?")

author = raw_input("What is the author's name?")

bookList.append(book(title.upper(), author.title()))

def listBook(bookList):

for i in bookList:

print "\"%s\", by %s\n" % (i.title.upper(), i.author)

def readBooks(bookList):

bList = []

f = open(raw_input(" Enter the filename."))

for line in f:

comma = line.find(",")

title = line[0:comma].rstrip(',')

author = line[comma+1:].strip()

bList.append(book(title.upper(), author.title()))

print "%s, %s" % (title.upper(), author.title())

userInput = raw_input("Would you like to record this to your temporary list?")

if userInput == "yes":

for i in bList:

bookList.append(i)

print "Saved."

else:

print "Not saved."

f.close()

def writeToNew(bookList):

userInput = raw_input("Enter the filename you'd like to export to.")

f = open(userInput, 'w')

for i in bookList:

f.write("%s, %s\n" % (i.title.upper(), i.author.title()))

f.close()

def writeToExisting(bookList):

userInput = raw_input("Enter the filename you'd like to add to.")

f = open(userInput, 'a')

for i in bookList:

f.write("%s, %s\n" % (i.title.upper(), i.author.title()))

f.close()

bookList = []

running = True

while running == True:

print "Welcome to BOOKKEEPER. Type:"

print "\t\"ADD\" to add a book to your temp list."

print "\t\"LIST\" to read out your temp list."

print "\t\"READ\" to read an existing file."

print "\t\"SAVE NEW\" to save to a new file."

print "\t\"SAVE EXISTING\" to save to an existing file."

print "\t\"CLEAR\" to clear your temporary list."

print "\t\"EXIT\" to exit."

userInput = raw_input()

if userInput.lower() == "add":

addBook(bookList)

elif userInput.lower() == "list":

listBook(bookList)

elif userInput.lower() == "read":

readBooks(bookList)

elif userInput.lower() == "save new":

writeToNew(bookList)

elif userInput.lower() == "save existing":

writeToExisting(bookList)

elif userInput.lower() == "clear":

bookList = []

elif userInput.lower() == "exit":

running = False

else:

print "The command was invalid!\n\n"

This program has hopefully helped you to understand how we can synthesize a lot of the concepts that we’ve covered so far. I also hope that it helped you to understand a bit more the relation between classes and objects. There are certainly far more confusing things in the language, but object-oriented concepts as such can be a little difficult to comprehend anyway.

Having gone through the major concepts and facets of the language, we’ve covered the bulk of the important things that there are to cover. At this point, I’d like to drive home how important of a resource the internet can be. Programming can be something that will make you want to tear your hair out at times. Admittedly, Python is an easier language, and even better, the compiler can be very informational, especially compared to other languages such as C++ or C where the compiler can be very confusing.

There will always be something you don’t know in the world of programming, and when you’re starting out, the list is endless. For practical purposes, there’s only so much that I can cover in the relatively limited scope of a beginner book. However, there are also more answers than you can ever imagine. The beautiful thing about programming is that everything has a solution somewhere. Often, it’ll already be developed in an API or module somewhere. When it’s not, it’s ultimately possible. The beauty of programming is that it’s an incredible way to express yourself, and if something can be done, it can be done on a computer. Computers break down in a very, very simple way to sequences of 1s and 0s and computations that are performed constantly, but in that simplicity is an endless amount of extrapolated complexity.

We may have written a relatively simple program. But the concepts contained therein will underlie a lot of the concepts that you may work with going forward while working with any other program or programming language.

And at the end of the day, if nothing else, you can say that you’ve written a really cool program to help you keep track of any and all books that you own, including this one. Isn’t that really a victory in and of itself?

| ![image](d2d_images/chapter_title_corner_decoration_left.png) |  | ![image](d2d_images/chapter_title_corner_decoration_right.png) |

![image](d2d_images/chapter_title_above.png)

# Conclusion

![image](d2d_images/chapter_title_below.png)

THANK YOU FOR MAKING it through to the end of the book, let’s hope it was informative and able to provide you with all of the tools you need to achieve your goals whatever they may be.

The next step is to use this knowledge to your advantage. Do something with it. You can absolutely use this book as a reference, but it wasn’t written to necessarily be one - this book was written in order to teach you the essence of programming and everything that you need to do to start programming in Python, as well as the essential tools of the language that you’ll have to know how to use as a beginner.

Python has a ton of support and is immensely popular, so you can find a way to use it for whatever you may need to do. For example, for game programming, there is the PyGame library.

Ultimately this book was written with the goal in mind of teaching you not necessarily about Python, but programming at large. Programming is a science, yet it is also an art - it’s a form of self-expression, of manipulating computer bytecode in order to get the end result you desire out of your brain and onto the computer screen. Python is just one means by which you can accomplish this goal.

Python is ultimately derived from a language called C, and the C programming language would go onto inspire a huge number of languages - not only Python, but also C++, Java, Lua, Go, D, R, Ruby, and so many more. This book was intended to teach you the underlying concepts so that you’re not restricted by any given programming language, because programming languages are much the same across one or another. The important thing is that you understand the underlying concepts - control flow, objects, input and output, manipulating variables - so that you can produce the end result that you want.

I hope you found this book to be a useful and fantastic starting place as a Python learner and hopeful programmer, whether you’re programming for your career or programming simply as a hobby.

![Charlie Masterson](d2d_images/ata_image.jpg)

# About the Author

Charlie Masterson is a computer programmer and instructor who has developed several applications and computer programs.

As a computer science student, he got interested in programming early but got frustrated learning the highly complex subject matter.

Charlie wanted a teaching method that he could easily learn from and develop his programming skills. He soon discovered a teaching series that made him learn faster and better.

Applying the same approach, Charlie successfully learned different programming languages and is now teaching the subject matter through writing books.

With the books that he writes on computer programming, he hopes to provide great value and help readers interested to learn computer-related topics.