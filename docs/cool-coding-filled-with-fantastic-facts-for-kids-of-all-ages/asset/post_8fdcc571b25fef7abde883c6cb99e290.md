
Some programmers prefer camel case, some prefer snake case; you can use whichever you prefer. Whichever you do use, be consistent within a program, or else things will start looking messy.

HiThereLimbless

![](img/862cb7d96d05319b069165a3aaaaa9d3_54_0.png)

### Comments

You can include comments in code. Comments are messages that you can use to remind yourself or anyone else who reads the code about what a function is doing or what’s happening in a particular place. Their syntax varies, but starting with // is a common way to write them. In this book we've replaced traditional comments with graphics boxes to make them easier to follow, but a typical example (from page 22) would be:

```text
print("Hello, world!") // remember, you need to put quote marks around strings
```

You can end up overusing comments – don't use them when the code is already obvious. A good rule of thumb is to write a comment to explain what each function is meant to do, and also any time you write a particularly complicated piece of code.

## Memory

Your computer can fit lots of things in its storage, but can only read and write to it fairly slowly (compared to how quickly the CPU can do things, that is). To speed things up the computer has another kind of fast storage called the memory or RAM (short for Random Access Memory). The computer's RAM is much faster than its storage, and it's where programs and other files are kept while they're being used. It's more expensive than storage, though, so you'll have less space in memory than in storage. It's also volatile, which means that it needs constant power to remember things - when you switch the computer off it forgets everything in its memory.

![](img/862cb7d96d05319b069165a3aaaaa9d3_56_0.png)

## Input/Output

Along with those core internals, computers also have input devices, like mice, keyboards, and touchscreens, which allow you to communicate with them, and output devices, like displays and speakers, that let the computer communicate with you. Since these are often not built directly into the machine, most computers have ports that let you plug them in. External devices like mice and speakers that connect to the computer are called peripherals.

## User Interfaces

So far we've looked at interacting with a program through lines of text; this is the simplest method to use. Programmers call this a command line interface, or CLI. Most computer users have trouble using a CLI. However, there's another way.

### Getting graphical

That other way is a graphical user interface, or GUI. A GUI lets your program show your users pictures, menus and other elements, and lets them interact with it using a mouse or touchscreen. GUIs take more work to create, so they're not something you should worry about until you've mastered the basics of programming, but they're very user-friendly.

To create a GUI you need a GUI framework. Each programming language has a different set of frameworks with different ways of doing things, all designed to help coders create a GUI for their program. Some languages come with a GUI framework built in, and that's usually the best to start with, but there will be numerous others you can download and use.

### Elements of interaction

All GUI frameworks revolve around a set of key elements you'll recognise from computer programs you've used.

- **Text boxes**: display text to users or allow them to enter text themselves.
- **Buttons**: are things users click to tell the program to do something.
- **Dropdowns**: are a list of options the users can pick from.

![](img/862cb7d96d05319b069165a3aaaaa9d3_57_0.png)

GUI frameworks will let you write code to define elements like buttons, along with their position, size and other properties. They often also include a GUI designer, which will let you draw out your GUI visually, and then generate part of the code for you. While it’s best to start out creating a few buttons in code to understand how they work, designers are much quicker to use.

> **That’s neat!**
>
> The way elements like buttons work is with a special type of function named a callback. A callback is just a function, but its name is passed into another function which will then call it back when a condition is met. So when a button is pressed, that callback function gets run.

- **Check boxes**: are options your users can toggle on or off.
- **Radio buttons**: are like check boxes, but users can only pick one option.
- **Labels**: help describe what all the other elements are for.

![](img/862cb7d96d05319b069165a3aaaaa9d3_58_0.png)

## Feeling Classy

All the programming we’ve seen so far has been examples of procedural programming, using independent variables and functions. However, since the 1970s another style of coding has become increasingly popular: object-oriented programming, which revolves around classes.

### Class is in session

A class is a way to store functions and variables within objects where they naturally belong, rather than having them spread out all over the place. For instance, if you wanted to write a program about dogs you could create a dog() class. Then you would make any variables or functions that related to dogs part of that dog() class.

Like a function, a class needs to be defined before it is used. This definition involves curly brackets like a function - the functions and variables are then put inside this block to show they belong to the class. In some languages functions inside a class are called methods.

Not only is this a nice, logical way to group variables and functions, but it means every time you want to consider a dog in your program, you just need to instantiate the dog() class. Instantiate just means assigning it to a variable, just as you do with a string or an integer. You can then access any of the functions or variables in the class with a dot operator, '.' Functions can also access internal variables by referring to this or self (depending on the language).

![](img/862cb7d96d05319b069165a3aaaaa9d3_59_0.png)

> Right, let's classify this stuff!

defining the dog() class

```text
class dog()
{
    name = "unknown"
    function speak()
    {
        print("Woof! My name is "+this.name)
    }
}
```

- this variable is part of the dog() class
- this function is part of the dog() class
- uses the internal 'name' variable

instantiate a variable of type 'dog()'

```text
my_dog = dog()
my_dog.name = "Rex"
my_dog.speak()
```

- set the 'name' variable for my_dog
- will print "Woof! My name is Rex"

### Under construction

The example above does have one problem – you have to set the name variable before you call speak() or you won't get a sensible result. It's quite often the case that some variables in a class need to be set before it can be used, and object-oriented programming solves this with a constructor. This is a special function in the class that is always called when you instantiate it (e.g. assign it to a variable). In our example above you could change the class definition to include a constructor that sets the name variable. Then you could write code like this:

another_dog's name will be filled in immediately

```text
another_dog = dog("Spot")
another_dog.speak()
```

will print "Woof! My name is Spot"

## Inheritance

### Meet the children

Inheritance, or subtyping, is when you define new child classes (or subclasses) that inherit from a parent class (or superclass). These child classes still retain all of the functions and variables of their parent class, but can also have their own variables and functions specific to them.

For instance, once you have defined a `dog()` class you could define child classes for specific breeds of dog. Anything that is common to all dogs goes into the parent `dog()` class, while anything specific to the breed goes into the individual child classes. Each child class is its own breed of dog with its own characteristics (colour, etc.), but also has all the properties of the parent class, which are common to all dogs (having four feet, etc.).

![](img/862cb7d96d05319b069165a3aaaaa9d3_61_0.png)
