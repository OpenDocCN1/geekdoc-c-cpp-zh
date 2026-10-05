
# Local "Var1"

Now let's look at the puzzle pieces for show:

# Show "Var1"

Show is also using Var1 for an input. Remember that the quote mark " before a word tells MicroWorlds that the word we are using is the name of something, a noun, rather than the name of a procedure, which is more like an action word, or verb.

Here is the procedure we are talking about, again:

- to TestVar
- local "Var1" ;reserves and names a storage place
- show "Var1" ;we want to print the value in the storage place
- end

So, now we have created our variable using name local. But we haven't stored any value in it. We need another procedure for that. Here it is, a bit of punctuation! ":" allows us to grab the value that is in a variable for us to use. We read this colon as "what"s in.

I want to know what the value is inside the memory spot named Var1. But the line, show "Var1. is an instruction to put the word Var on the Command Center. This is not really what I meant!

We will say show Var1, meaning show what's in Var1. There is no space between the colon and the name after it.

Change your TestVar procedure as follows:

- to TestVar
- local "Var1" ; reserves and names a storage place
- show "Var1" ; show what's in Var1
- end

and run your program. Here is the result I get:
Var1 has no value in TestVar

We're getting there. We get an error message, telling us that we haven't put a value into the storage space. When we look at our procedure we can see this is true, we made a storage space (a variable) but we didn't tell MicroWorlds what to put in it. We goofed. It is a programming error to try to use a value from a variable if no name has ever been stored.

So how do we put a value in the variable? We have one more procedure to learn. There is a built-in procedure make that does the job of storing values in named variables. It takes two inputs and no outputs. The first input is the name of the variable, and the second is the value to be stored. It looks like this:

![](img/242aaa06c3a3208f16d97cdd92303648_46_0.png)

Change your procedure to the following:

```
to TestVar
local :Var1 ;creates and names a variable
make :Var1 20 ;puts the value 20 in the variable
show :Var1 ;prints the value in the variable
end
```

![](img/242aaa06c3a3208f16d97cdd92303648_46_1.png)

Or, using our mailbox diagram,

![](img/242aaa06c3a3208f16d97cdd92303648_46_2.png)

Lets take a look at what we have written in our TestVar procedure so far.

- We use local to make a variable named Var1
- We use make to put the value 20 in the variable.
- We use show to show :Var1, the value stored in Var1.

I think it should all work this time! Before you run your program, so that your Command Center shows only the newest messages, add the cc instruction in Main, like this:

```
to Main
cc
TestVar
end
```

This course just clears out the Command Center as you start your program each time. Now run your program.
Bingo! The value stored is 20! Let's put it in 20 and then replace it with 50, and see what happens.

```
to TestVar
local :Var1
make :Var1 20
show :Var1 ; this means show the value stored in Var1
make :Var1 50
show :Var1
end
```

Here's what shows in my Command Center:

- 20
50

Again, using our mailbox diagram,

![](img/242aaa06c3a3208f16d97cdd92303648_47_0.png)

We replaced the value stored, and the first one is gone forever.
What about storing a word instead of a number? Be sure to put a quote mark before the word. Try this:

```
to TestVar
local :Var1
make :Var1 20
show :Var1
make :Var1 "Me"
show :Var1
end
```

Pretty neat, eh!

Let's make another variable to play with.

```
to TestVar
local "Var1"
make :Var1 20
local "Var2"
make :Var2 50
show :Var1
show :Var2
end
```

What does your command center look like? It should show 20, then 50. But in this case, there are two mailboxes!

![](img/242aaa06c3a3208f16d97cdd92303648_48_0.png)

There is a built-in procedure that is easy to use, sum. It takes 2 inputs, both numbers, and has one output (the answer). If you wanted to add 2 and 3, you would write sum 2 3, since outputs come after the procedure name. The answer you can show, or store in a variable, or whatever.

![](img/242aaa06c3a3208f16d97cdd92303648_48_1.png)

Try this:

```
to TestVar
local "Var1"
make :Var1 20
local "Var2"
make :Var2 50
show :Var1
show :Var2
show sum 20 15
show :Var1 15
end
```

What is that last line? We are adding two numbers. One is the value stored in Var1, and the other is 15. Then we are printing the result. Your Command Center should say 20 50 35.

It is an excellent exercise to draw the puzzle of instruction, especially before you run it. It can really help you learn what is going on. It is neat to see how procedures fit together with their inputs and outputs. Try adding these lines to TestVar. Remember, sum has two inputs. Can you tell what they are doing?

```
show :Var1 :Var2
show sum :Var1 15
```

And of course, make up your lines to experiment with.

# Talk like Logo

Another way to be sure you are understanding how Logo works is to "talk" your way through an instruction. I will do this:

```
show sum 20 15
```

I am MicroWorlds Logo. The procedure show tells me to take one input and put it on the Command Center. I need one input.

- The procedure sum has an output that I can use to satisfy my need for an input.
- I need two inputs for sum before I can calculate the output.
- The inputs for sum are the two numbers 20 and 15.
- Now I have the output of sum, it is 35.
- So now I can satisfy the input to show. I will put 35 on the Command Center.

Exercise: Write a procedure testSize (instead of testVar) that will do the following:
- Reserve and name a memory spot called size.
- Rewrite testVar. Instead of Var1, create a variable size.
- Store the value of 5 in the spot.
- Instead of Var2, reserve and name a variable called height.
- Take your height in inches, and store it in the variable.
- Print the current value of size.
- Print the current value of height.
- Add 3 to the value of size and store the result in the same place, size.
- Print the current value of size.

# #10 Animation Using Variables

Now we will make use of our new knowledge of variables. First, type in the following. Save under a new name. It should look like this:

```
to Main
end
to square
  repeat 4 [forward 50 90 1]
end
to Start
  Main
end
```

Now it's time to add an action. I want you to add some lines to Main so it looks like this:

```
to Main
  cc
  talk "turtle"
  set [horse1 horse2 horse3]
  repeat 20 [square]
```

Put the horse1, horse2, and horse3 shapes into your Shape Center.

# Adding an input to our procedure

A while back, I suggested that it would be nice if we could decide how big a square our turtle should make. Then we would have a nice, general procedure that could be used anytime we want a square any size. You won't believe how easy it is to make this improvement, now that we understand variables.

We want to turn our procedure square, which currently has no inputs and outputs, into a procedure that receives one input. We do that simply by thinking of a good name for the input—how about length?—and putting it on the line that declares the procedure. Since we are passing the value in length, we will use :length. Make the following change to square:

```
to square :length
repeat 4 [forward 50 90 1]
end
```

We just used a shortcut! Instead of using the instruction local, we created the variable another way. We put the variable name in the first line of the procedure. This also takes a spot in memory and names it length so we can store a value in it.

Again, using our mailbox diagram,

![](img/242aaa06c3a3208f16d97cdd92303648_51_0.png)

The neat thing is that we don't have to use make to put the value in. We pass the value to the square procedure when we call it. In other words, when we use the square procedure in Main, we need to place an input next to it that will go into the mailbox. The code in Main needs to say, for example,

square 5
instead of

square

The 5 would go into the mailbox which is part of the procedure square. That mailbox is named length.

Here's an example of a procedure we already know that needs an input: forward. Whenever we type forward, we have to put a number after it for input. Somewhere, somebody has already written a procedure for forward, which starts with to and has a variable name in the first line. Now our square procedure will be like that, requiring an input number.

So square now needs one input. Its jigsaw piece looks like this:

![](img/242aaa06c3a3208f16d97cdd92303648_51_1.png)
