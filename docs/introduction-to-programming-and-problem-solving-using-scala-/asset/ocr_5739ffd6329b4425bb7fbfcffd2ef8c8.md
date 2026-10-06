# Scala Basics

what makes the String type immutable. The trim method used above demonstrates this same behavior. Most of the types we will deal with are immutable.^{15}

# 2.9 Sequential Execution

Sequential execution is used when we write a program and want the instructions to execute in the same order that they appear in the program, without repeating any instructions from the sequence. So far, all of the program instructions we have written have executed one after another in the same order that we have typed them in. The instructions have been executed sequentially.

Working in REPL is for certain tasks, but what if you have a sequence of things you want to do, and you want to do it multiple times. The way of giving sets of instructions repeatedly is not a good option. The conversation above is a perfect example of that. If we want to do this for a different number of times, we have to repeat all the commands we just performed. Indeed, you cannot really say that what you have programmed until you put in a fixed set of instructions for solving a problem that you can easily run multiple times. What a program really is. Now it is time to write your first program of any magnitude.

We have used the REPL to enter commands one at a time. This is a great way to test out in Scala and see what a command does. A second way of giving commands to Scala is to write little programs as SCRIPTS. The term script is used to describe small programs that perform specific tasks. There are languages, called scripting languages, that have been created specifically to make the task of writing small programs easier. Scala is not technically a scripting language, but it can be used in that way. The syntax created to mirror a lot of the things that are commonly put into scripting languages, and if you run the scala command and give it the name of a file that contains Scala code, that file will run as a script. The statements in it are executed in order.^{16} The script for time conversion looks like

Listing 2.1: TimeConvert.scala

```
val totalSeconds = 123456
val displaySeconds = totalSeconds%60
val totalMinutes = totalSeconds/60
val displayMinutes = totalMinutes%60
val sec = displaySeconds.toString
val min = displayMinutes.toString
val finalString = displayHours+++":"
```

If you put this into a file TimeConvert.scala and then run scala TimeConvert.scala, you will get the output 34:17:36. The println statement is required for the script because unlike the REPL, the script does not print out values of all statements. You can run through with

> 15The first mutable type we will encounter is the Array type in chapter 6. That chapter will go further in demonstrating the significance of this distinction.

> 16We will see that the statements are not always executed in order because there are statements that alter the flow of control through the program. Since we have not gotten to those yet though, execution is completely sequential at this point.