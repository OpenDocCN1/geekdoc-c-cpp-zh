# Chapter 7

# Decision Making and Looping

# 7.1 INTRODUCTION

We have seen in the previous chapter that it is possible to execute a segment of a program repeatedly by introducing a counter and later testing it using the if statement. While this method is quite satisfactory for all practical purposes, we need to initialize and increment a counter and test its value at an appropriate place in the program for the completion of the loop. For example, suppose we want to calculate the sum of squares of all integers between 1 and 10. We can write a program using the if statement as follows:

![](bbox=[0.25, 0.6, 0.8, 0.78])

This program does the following things:

+   1. Initializes the variable n.
+   2. Computes the square of n and adds it to sum.
+   3. Tests the value of n to see whether it is equal to 10 or not. If it is equal to 10, then the program prints the results.
+   4. If n is less than 10, then it is incremented by one and the control goes back to compute the sum again.