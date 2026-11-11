
## CHAPTER 3: PROGRAMMING IN LUA

Lua is a new language that is gaining a lot of popularity for its flexibility and ease of use. It is the language chosen by the developers of ComputerCraft to allow you to write programs that can control Minecraft from within the ComputerCraft mod.

Lua is an easy language to learn and if you have used Python, you will find it particularly easy as the syntax is quite similar.

As we look at Lua, you will find it useful to have the Lua command line open (Figure 3-1) so that you can type in commands and try things out.

If you are not sure about how to start the Lua command line and what it is for, then please look back over Chapter 2.

The Lua programming language is not unique to ComputerCraft. It is available for most types of computer. There is also an online Lua interpreter, that works like the ComputerCraft Lua Command Line, except that it does not have any of the commands that are specific to ComputerCraft for doing things like controlling Redstone.

You can find the online Lua interpreter here:

http://www.lua.org/demo.html

Figure 3-2 shows how it is used. Just type the Lua commands in the box at the top and then press Run to run the code. The results of any print commands or errors will be shown in the box underneath.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_25_0.png)

Figure 3-1. The Lua Command Line

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_25_1.png)

Figure 3-2. Lua Online

### Simple Sums

Programming languages all allow you to do calculations and display results. Try entering the following on the Lua command line:

```lua
print(2 + 2)
```

This will display the answer (4). No surprise there!

The print command tells Lua to display on the command line whatever is inside the (). So, we could just do:

```lua
print(4)
```

Try it. But by putting a sum inside the (), the sum is performed first and the result of the sum is displayed rather than the sum itself.

### Variables

Variables are a way of giving a value a name. Try typing the following into the Lua command line:

```lua
a = 23
print(a)
```

The first line gives the variable called a the value 23 and the second line prints the value of a. You can use almost any name you like for a variable, but it cannot contain any spaces and by convention, it should start with a lowercase letter. You can use underscore characters (_) to separate words.

So for example you could write:

```lua
number_of_blocks = 100
print(number_of_blocks)
```

You can use variables in sums too. Try typing in the following commands:

```lua
number_of_blocks = 100
print(number_of_blocks)
number_of_blocks = number_of_blocks + 1
print(number_of_blocks)
```

Lua will first display the answer 100 and then 101.

The line `number_of_blocks = number_of_blocks + 1` has added one to `number_of_blocks`.

In the examples so far, the variable we have used has contained a number. Variables can hold different types of values, not just numbers. Perhaps the most common type of variable is called a string.

The word string amongst programmers means just some text. This could be a single word or a sentence or even the entire contents of a web page.

Try the program out a few times with both the correct password and an incorrect password.

Note how the end of the series of commands to run if the condition is true are marked with the end keyword. It is also important to indent the things that should be done, so that you can immediately see what is going to run if the condition is true, as opposed to commands outside the if statement that will always be run. Indent the lines of code inside the “if” statement by pressing tab once.

We could expand this example, so that if the wrong password was entered then you get a different message back. To do this we use an if else command as shown below.

```lua
password = io.read()
if password == "computercraft" then
    print("Opening Door")
else
    print("Wrong Password")
end
```

### Loops

If you want to do something more than once then you need to put the commands that you want to repeat inside a while loop. For example, if you wanted to allow people to keep trying to guess the password, you could put the code above inside a loop like this:

```lua
while true do
    password = io.read()
    if password == "computercraft" then
        print("Opening Door")
    else
        print("Wrong Password")
    end
end
```

The first line (while true do) will ensure that all the commands right up to the end on the last line will be repeated forever. Forever, because the condition after the word while is, in this case, true.

The value true is called a Boolean value. These kinds of value can only be either true or false. We will see them later in the context of controlling Redstone, where true means on and false means off.

If you wanted to only allow someone five incorrect guesses, then you could change the code like this:

```lua
fails = 0
while fails < 5 do
    password = io.read()
    if password == "computercraft" then
        print("Opening Door")
    else
        print("Wrong Password")
        fails = fails + 1
    end
end
print("You are only allowed 5 attempts. Exiting")
```

Now, we are using a variable called fails that counts the number of times an incorrect password was entered. When this exceeds 5, the condition for staying in the while loop (that fails is less than 5) is no longer true and Lua exits the while loop and prints the message that the number of attempts has been exceeded.

This kind of "while" loop is handy if you just want to keep doing something until a condition stops being true. The other common situation where you might want to loop a certain number of times is called the "for" loop.

The following example prints out the numbers 1 to 10. Try typing it into a program (call it "fortest") and run it.

```lua
for i = 1, 10 do
    print(i)
end
```

Try changing 10 to 100 and run it again.

### Functions

When you write programs in any language, if you are not careful, there comes a point where everything gets too complicated to work out what is going on. A great way to keep things simple and easy to modify is to break up your programs into manageable chunks called functions.

By putting sections of code in a function, you get the added advantage that you do not have to repeat yourself in your program, you can just call the same function from different places in your program.

There are really two things that you need to be able to do to a function. The first is to define it, which specifies the commands that are going to be contained in the function and the second is to make the function run. Making the function run is referred to as "calling" the function.

To define a function you use the "function" command. Let's start by defining a really simple function that just prints out three lines of text every time it is called.

To try this out, change directory to the "mystuff" directory that you created earlier and type the following command:

```
edit functiontest
```

Then type the following into the editor before saving the file.

```lua
function printWelcome()
  print("This program is written")
  print("in the programming language Lua")
  print("Lua comes from Brazil")
end

printWelcome()
printWelcome()
printWelcome()
```

Save the program and exit the editor, then try running it by typing:

```
functiontest
```

You should see the whole message printed out three times.

We can use a "for" loop rather than call the function three times, one after the other. Change the code to agree with the listing below and then run it again. The message will be printed out 10 times.

```lua
function printWelcome()
  print("This program is written")
  print("in the programming language Lua")
  print("Lua comes from Brazil")
end

for i = 1, 10 do
  printWelcome()
end
```

Functions can also be supplied with something called parameters. So, if for example, we wanted to write a function that would count up to a number of our choosing, we could write something like this:

```lua
function count(numberOfTimes)
  for i = 1, numberOfTimes do
    printWelcome()
  end
end
```

You could then instruct it to count up to 10 using:

```lua
count(10)
```

To make it count to 1000, you would just do:

```lua
count(1000)
```

If you want a function to have more than one parameter, you just separate them with commas both where you define the function and where you call it.

Modify the count example to take two parameters, fromNumber and toNumber.

```lua
function count(fromNumber, toNumber)
  for i = fromNumber, toNumber do
    printWelcome()
  end
end
```

```lua
count(5, 20)
```

Another thing that functions can do is to return a value. When a function returns a value, it means that you can assign the returned value to a variable.

Let's write a function that converts temperatures in degrees C to degrees F:

```lua
function c2f(c)
  f = c * 9 / 5 + 32
  return f
end
```

```lua
temp = c2f(20)
print(temp)
```
