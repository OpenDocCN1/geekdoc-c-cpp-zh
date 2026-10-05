
Go to the Help screen and look up random. Remember how? In MicroWorlds 2.0, just click on Help and Vocabulary. In EX, click on Help, then vocabulary, then on the Web page adjust the level from Basic to Advanced in the upper right, and choose the Vocabulary tab (allow the active content to get there if you need). Now click on the letter R in the alphabet to the left.

Reports a random non-negative integer (including 0) less than number. The maximum number is 9999.

- random number
Reports a random non-negative integer less than number.
Example:
show random 100
22

Random is a procedure that has one input, a number, and one output, also a number.

![](img/242aaa06c3a3208f16d97cdd923036488_103_0.png)

Random 100 generates a random number less than 100. Let's investigate. Write the following code on your Procedures Page:

```
to Main
wander
end
to Start
Main
end
to wander
show random 100
end
```

Click on the Start button several times. We see random numbers, all less than 100, displayed in the Control Center.

In our wander procedure, we will want to change the direction of the turtle by a negative amount or a positive amount. Random, however, only outputs positive numbers. How can we make random give us numbers that are less than zero? Think about that one for a minute. Hint: we'll need to do some subtracting.

We need to do a little more sandboxing because we need some experience subtracting one number from another. A look in the MicroWorlds Help index turns up **difference**. Difference is a lot like sum. It requires two inputs and has one output. Its output is the result of subtracting the second input from the first input. Here is what the puzzle piece looks like.

![](img/242aaa06c3a3208f16d97cdd923036488_104_0.png)

Let's sandbox with **difference**. Change your code to the following:

```
to wander
  ;show random 100
  ;show difference 25 10
end
```

Notice that we put a ";" in front of the second line; this makes it a comment, not read by the computer. This is called “commenting out” some code. Try different numbers as inputs for **difference** until you are sure you understand **difference**.

Now, can you figure out how to make our procedure come up with random numbers, *half of which are less than zero?* (Hint: Use **difference** to subtract something from **random 100**, the random number less than 100.)

Don't turn the page until you think about it and try five solutions in the Command Center, using **show**. Here's how it will look, with the _ under the number you will supply:

```
show difference random 100 _
```

Here's a solution: show difference random 100 50. Fifty is half of 100.

We give random a number as input, 100. Random gives us an output number, say 76. We then subtract half the input number of 100 from the 76. Seventy-six minus 50 is 26, the number that will print out.

If the number random puts is less than 50, for example 30, then the number that prints out is 30 minus 50 equals -20, a negative number. So about half the time, we should be getting a negative number.

Here's the code for this solution:

```
to wander
show difference random 100 50
end
```

Do you have difficulty figuring out that line? When you “walk through” it, starting at the left, it is a bit easier. Just be sure to think of the outputs and inputs.

- show - takes one input
- difference - has one output; good, show needs that; takes two inputs
- random - has one output; good, that is one of the two needed by difference; needs one input
- 100 - has one output; good, that is the one needed by random, so now random is happy
- 50 - has one output; good. that is the other of the two needed by difference, so now difference is happy and it makes show happy.

In other words, we are subtracting 50 from the output of random 100, and we are showing the result.

We'll be changing our turtle's heading. There are several ways to do this, but here's a simple one: how about a right turn? In the Help vocabulary, let's look at the procedure right:

- right
right (rt) number
Turns the turtle to the right.
Example:
pd repeat 10 [fd 40 bk 20 rt 36]

If right has a positive input, the turtle turns to the right. If it has a negative input, the turtle turns to the left. So, half the time we will have a negative number, and half the time the turtle will be turning left.

# Write Pseudocode

Now that we have acquired some necessary knowledge, it is time to write this up as pseudocode. It is what I want for the wander procedure:

```
to wander
;change the turtle's heading by a random amount
```
