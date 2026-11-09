
## Taking things further

When you have finished this book your adventure really begins! You might want to develop your own projects now in Python. Should you be interested, you are now in a good position to start a new language. You will find that all you need to do is look up the syntax used in the new language to indicate loops or classes etc. You will find there are a lot of similarities in, for example, PHP, Java and the C family of languages. Alternatively, you might want to delve into some other tools and libraries that add functionality to Python. Here are some starting points:

### The Python stuff

**Coding Club books**

This is the first Level 3 book in the series but you may still find things to interest you in any of the other project books at lower levels.

http://www.codingclub.co.uk

**PyGame**

This popular library currently works best using Python 2 rather than 3 but there is not too much difference. The library makes extensive use of classes in its game implementation.

http://www.pygame.org/

**PiFace**

If you have a Raspberry Pi you may want to try your hand at physical computing. One way of doing this is to purchase a PiFace from Manchester University which can be programmed directly in Python. It will enable you to use your computer to control all sorts of things by interfacing with a selection of sensors or a talking chicken, for instance.

http://pi.cs.man.ac.uk/

### Non-Python stuff

**Arduino**

This is an alternative to the PiFace for physical computing. It works with any type of computer rather than just a Raspberry Pi. The language used is C but you will find that the code to sense and control uses far less complicated code than we have been using in this book, so it will not take you very long to get used to it.

http://www.arduino.cc

**GameMaker**

This has been popular in some schools for a number of years. It uses a drag-and-drop system for building games. After a while though, this becomes limiting. At this point you can add your own code or download others. Now you will be in a position to understand the code and design your own.

http://www.yoyogames.com/

**Greenfoot**

If you really love the idea of building code in an OOP way, there is no better way of exploring this in Java than by trying out Greenfoot. There are lots of free resources on this site including many great video tutorials.

http://www.greenfoot.org/

## Appendix

### Some key bits of information

**Companion website**

Go to www.codingclub.co.uk for the complete source code to all the apps in this book plus example answers for many of the puzzles, challenges and ideas found at the end of each chapter. Also find out about the characters that feature in the books and other exciting information about the Coding Club series. While on the website, take the time to submit your email address to ‘keep informed’ about the latest developments as and when they happen.

**Useful code examples**

**while loops:**

```python
while my_test == True:
    # code that does things goes here
```

**for loops:**

```python
for i in my_list:
    print(i)
```

**quick comparison function:**

```python
def is_same(guess, password):
    return guess == password
    # returns True if the same and False if different
```

**Instantiation example:**

```python
import cat
romeo = cat.Cat("Romeo")
```

### Class planning template

| Class Name |
|---|
| Attributes |
| Methods |

(A printable version is available on the companion website.)

## Glossary and index

- **argument** — a piece of information that is required by a function, a method or a class so that it can perform its task; this is usually a `string` or `number`, for example, `my_function(arguments go here)`. — 11
- **attributes** — the properties of an object such as width, height, colour, etc. — 27
- **boolean variable** — a variable that holds only two values – `True` or `False` — 11
- **bug** — a piece of code that is causing a program to fail to run properly or at all — 48
- **casting** — the process of converting one data-type into another; for example, sometimes a number may be stored as text but need to be converted into an integer; this can be done like this: `int ("3")` — 99
- **classes** — in object-oriented programming, classes are sections of code that objects are built from; in this book they are compared to factories although it is more common to describe them as templates or blueprints — 19
- **comments** — some text in a computer program that is for the human reader and is ignored by the computer when running the program; in Python all comments begin with a hash symbol `#` — 9
- **comparative operators** — sometimes called logic operators; they allow us to compare data in a program; they include `==` and `>`
- **concatenating** — the joining of two strings into one string
- **constant** — a number that does not change; it is good practice to name constants in capitals e.g. `SPEED_OF_LIGHT`
- **constructor** — a special kind of method that is called when an instance of a class is created; it is constructed with the Python keyword `__init__`; one of its purposes is to initialise an object’s attributes
- **data-types** — different types of information stored by the computer, for example floats, integers, strings, tuples, lists and dictionaries
- **debugging** — the process of finding bugs in a program
- **default value** — a value given to an argument or variable as a starting point
- **dot operator** — a dot is used in coding to link a method or function with its class or module e.g. in `math.random(1, 6)` the dot tells the computer that the random function is found in the math module
- **equals operator** — the equals sign is used to assign a value to a variable in coding, for example `n=2` assigns the value 2 to the variable `n`

| Term | Definition | Page |
|---|---|---:|
| **factory** | in this book, factory is used to describe a class (in advanced object-oriented programming the word has a different meaning) | 19 |
| **function** | a reusable piece of code | 10 |
| **global variable** | a variable that is usable anywhere in a program | 63 |
| **hacking** | taking some previously written code and re-writing bits to make it do something different | 49 |
| **hard coded** | when an actual value is put into code instead of a variable that can subsequently change e.g. `width = 45` is hard coded whereas `width = my_width_variable` is not | 50 |
| **IDE** | stands for Integrated Development Environment; IDLE is an example of one; they are special text editors with useful tools built in for programmers | 8 |
| **IDLE** | stands for Integrated Development Environment; this is the IDE that comes with a normal Python 3 install | 8 |
| **index** | the number that references a value in a string, tuple or list; each item in the container data type is indexed from 0 for the first item, 1 for the next etc. | 85 |
| **infinite loop** | a piece of code that keeps running forever; this is usually a bad thing | 63 |
| **initialise** | to assign a start value to a variable | 27 |
| instance | in object-oriented programming, an instance is an object created from a class | 22 |
| instantiate[d] | in object-oriented programming the process of bringing into existence an object created from a class | 22 |
| interactive mode | this is when we use IDLE to try out snippets of code without saving them | 8 |
| lists | ordered container data types that can hold values of any type and can have elements added or removed; like tuples each element is indexed from 0 | 106 |
| local variable | a variable that is defined inside a function and is only usable inside that function | 63 |
| loop | a piece of code that keeps repeating until a certain condition is met | 47 |
| method | the name given to a function in a class | 20 |
| module | a saved Python file whose functions can be used by another program | 10 |
| objects | in object-oriented programming, objects are instances of classes – entities created from factories e.g. lion is an object instantiated from the Cat class | 18 |
| object-oriented programming (OOP) | a system of programming where the emphasis is on building objects from classes rather than focusing on actions and logic | 17 |
| parameters | another name for attributes | 27 |
