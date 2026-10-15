# 21. Bridge Pattern

In this chapter we can explore the Bridge pattern which is commonly used in applications.

# Challenge

You are working on an abstract business class. The class needs to log information to by writing to a file, email to user etc. We need to avoid tightly coupling of the business class and logger as in future newer versions of logger might appear.

# Tightly Coupled Design

![](bbox=[0.21, 0.31, 0.48, 0.52])

How to achieve a decoupled solution?

# Definition

GoF Definition: "Decouple an abstraction from its implementation so that the two can vary independently"

# Implementation

We can create an abstract class for representing the Logger. Let the abstract business class hold reference to the new abstract Logger. In the runtime we can specify the actual implementation instance of Logger class. (File writer or Emailer) Following is the snapshot of the class diagram after using the Bridge Pattern: