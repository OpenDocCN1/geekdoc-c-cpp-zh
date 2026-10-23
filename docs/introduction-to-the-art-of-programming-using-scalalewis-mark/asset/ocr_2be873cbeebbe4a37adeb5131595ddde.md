# Chapter 4

# Conditionals

+   4.1 Motivating Example ......................................................... 71
+   4.2 The if Expression ........................................................... 72
+   4.3 Comparisons ............................................................... 75
+   4.4 Boolean Logic .............................................................. 76
+   4.5 Bigger Expressions ......................................................... 79
+   Bit-wise Arithmetic ........................................................... 81
+   4.6 End of Chapter Material .................................................... 83
+   4.6.1 Problem-Solving Approach ............................................... 83
+   4.6.2 Summary of Concepts .................................................... 84
+   4.6.3 Self-Directed Study ..................................................... 84
+   4.6.4 Exercises ............................................................... 85
+   4.6.5 Projects ............................................................... 87

We solved some basic problems in the last chapter, but the techniques that we have access to are fundamentally limited at this point. The real problem is that all the lines in a script execute in the same order from top to bottom every time the script is run. In most real problems we need to be able to do what is called conditional execution, where something happens only in certain situations. In this chapter we will learn the most fundamental method for doing conditional execution in Scala and see how we can use it to solve more complex problems.

In order to do this properly, we need to develop a formalized way to express logic and put it into our programs. This system, called Boolean logic, will allow us to state the conditions under which various parts of our program will or will not happen.

# 4.1 Motivating Example

You have been asked to write a program that will calculate charges for people visiting a local amusement park. There are different charges for adult vs. child, whether they are bringing in a cooler, and whether they want to also get into the water park. We need to write code that will tell us how much the person pays. We will have the user input the needed information such as an Int for the persons age, a Boolean for whether they have a cooler, and another Boolean for whether they want to get into the water park.

This is something that we could not do last chapter because we did not have a way of performing logic. We could not say that we wanted to do something only in a particular situation. This ability to do different things in different situations is called conditional execution and it is a very important concept in programming. It is also critical for problem solving in general. Conditional execution gives you the ability to express logic and to solve much more complex problems than you could do without it.