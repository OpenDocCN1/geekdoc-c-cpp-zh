
## STEP 5

However, you can't combine both strings and integer type variables in the same command, as you would a set of similar variables. You need to either turn one into the other or vice versa. When you do try to combine both, you get an error message:

```
print (name + age)
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_34_0.png)

## STEP 6

This is a process known as TypeCasting. The Python code is:

```
print (character + " is " + str(age) + " years old.")
```

or you can use:

```
print (character, "is", age, "years old.")
```

Notice again that in the last example, you don't need the spaces between the words in quotes as the commas treat each argument to print separately.

```
>>> print (name + age)
Traceback (most recent call last):
  File "<pyshell#18>", line 1, in <module>
    print (name + age)
TypeError: Can't convert 'int' object to str implicitly
>>> print (character + " is " + str(age) + " years old.")
David Hayward: Descended from Vikings is 44 years old.
>>> print (character, "is", age, "years old.")
David Hayward: Descended from Vikings is 44 years old.
```

## STEP 7

Another example of TypeCasting is when you ask for input from the user, such as a name. for example, enter:

```
age= input ("How old are you? ")
```

All data stored from the Input command is stored as a string variable.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_34_1.png)

## STEP 8

This presents a bit of a problem when you want to work with a number that's been inputted by the user, as age + 10 won't work due to being a string variable and an integer. Instead, you need to enter:

```
int(age) + 10
```

This will TypeCast the age string into an integer that can be worked with.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_34_2.png)

## STEP 9

The use of TypeCasting is also important when dealing with floating point arithmetic; remember: numbers that have a decimal point in them. For example, enter:

```
shirt=19.99
```

Now enter type(shirt) and you'll see that Python has allocated the number as a 'float', because the value contains a decimal point.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_34_3.png)

## STEP 10

When combining integers and floats Python usually converts the integer to a float, but should the reverse ever be applied it's worth remembering that Python doesn't return the exact value. When converting a float to an integer, Python will always round down to the nearest integer, called truncating; in our case instead of 19.99 it becomes 19.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_34_4.png)

## User Input

We’ve seen some basic user interaction with the code from a few of the examples earlier, so now would be a good time to focus solely on how you would get information from the user then store and present it.

### USER FRIENDLY

The type of input you want from the user will depend greatly on the type of program you’re coding. For example, a game may ask for a character’s name, whereas a database can ask for personal details.

## STEP 1

If it’s not already, open the Python 3 IDLE Shell, and start a New File in the Editor. Let’s begin with something really simple, enter:

```
print("Hello")
firstname=input("What is your first name? ")
print("Thanks.")
surname=input("And what is your surname? ")
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_35_0.png)

## STEP 3

Now that we have the user’s name stored in a couple of variables we can call them up whenever we want:

```
print("Welcome", firstname, surname, ". I hope you’re well today.")
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_35_1.png)

## STEP 2

Save and execute the code, and as you already no doubt suspected, in the IDLE Shell the program will ask for your first name, storing it as the variable firstname, followed by your surname; also stored in its own variable (surname).

![](img/2f9c26fcf758b5bc56897d9c75b6347f_35_2.png)

## STEP 4

Run the code and you can see a slight issue, the full stop after the surname follows a blank space. To eliminate that we can add a plus sign instead of the comma in the code:

```
print("Welcome", firstname, surname+". I hope you’re well today.")
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_35_3.png)

## STEP 5

You don’t always have to include quoted text within the input command. For example, you can ask the user their name, and have the input in the line below:

```
print("Hello. What’s your name?")
name=input()
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_36_0.png)

## STEP 6

The code from the previous step is often regarded as being a little neater than having a lengthy amount of text in the input command, but it’s not a rule that’s set in stone, so do as you like in these situations. Expanding on the code, try this:

```
print("Halt! Who goes there?")
name=input()
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_36_1.png)

## STEP 7

It’s a good start to a text adventure game, perhaps? Now you can expand on it and use the raw input from the user to flesh out the game a little:

```
if name=="David":
    print("Welcome, good sir. You may pass.")
else:
    print("I know you not. Prepare for battle!")
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_36_2.png)

## STEP 8

What you’ve created here is a condition, which we will cover soon. In short, we’re using the input from the user and measuring it against a condition. So, if the user enters David as their name, the guard will allow them to pass unhindered. Else, if they enter a name other than David, the guard challenges them to a fight.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_36_3.png)

## STEP 9

Just as you learned previously, any input from a user is automatically a string, so you need to apply a TypeCast in order to turn it into something else. This creates some interesting additions to the input command. For example:

```
# Code to calculate rate and distance
print("Input a rate and a distance")
rate = float(input("Rate: "))
```

![](img/2f9c26fcf758b5bc56897d9c75b6347f_36_4.png)

## STEP 10

To finalise the rate and distance code, we can add:

```
distance = float(input("Distance: "))
print("Time:", (distance / rate))
```

Save and execute the code and enter some numbers. Using the float(input element, we’ve told Python that anything entered is a floating point number rather than a string.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_36_5.png)

## Creating Functions

Now that you’ve mastered the use of variables and user input, the next step is to tackle functions. You’ve already used a few functions, such as the print command but Python enables you to define your own functions.

### FUNKY FUNCTIONS

A function is a command that you enter into Python to do something. It’s a little piece of self-contained code that takes data, works on it and then returns the result.

## STEP 1

It’s not just data that a function works on. They can do all manner of useful things in Python, such as sort data, change items from one format to another and check the length or type of items. Basically, a function is a short word that’s followed by brackets. For example, len(), list() or type().

![](img/2f9c26fcf758b5bc56897d9c75b6347f_37_0.png)

## STEP 3

You can pass variables through functions in much the same manner. Let’s assume you want the number of letters in a person’s surname, you could use the following code (enter the text editor for this example):

```
name=input ("Enter your surname: ")
count=len(name)
print ("Your surname has", count, "letters in it.")
```

Press F5 and save the code to execute it.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_37_1.png)

## STEP 2

A function takes data, usually a variable, works on it depending on what the function is programmed to do and returns the end value. The data being worked on goes inside the brackets, so if you wanted to know how many letters are in the word antidisestablishmentarianism, then you’d enter: len("antidisestablishmentarianism") and the number 28 would return.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_37_2.png)

## STEP 4

Python has tens of functions built into it, far too many to get into in the limited space available here. However, to view the list of built-in functions available to Python 3, navigate to www.docs.python.org/3/library/functions.html. These are the predefined functions, but since users have created many more, they’re not the only ones available.

![](img/2f9c26fcf758b5bc56897d9c75b6347f_37_3.png)
