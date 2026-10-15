# 1. Singleton Pattern

This is most popular pattern among the 23 Design Patterns. This pattern talks about efficient instance management.

# Challenge

You are working on an application which requires Logging information into a file named **Application.Log**. The logging is managed by a class named **LogManager**. The LogManager through its constructor keeps a lock on the File.

The LogManager instance an be created throughout the application and it will result in Exceptions. Above that there is only instance requirement for the LogManager class.

The above problem can be solved using Singleton Pattern.

# Definition

> GoF Definition: "Ensure a class only has one instance, and provide a global point of access to it"

# Implementation

To implement the specification above we have to perform the following:

+   - Make the Constructor Private and Create only 1 Instance
+   - Create a Static Property to Access the Instance

Following is the modified class definition according to Singleton Pattern.

![](bbox=[0.188, 0.634, 0.498, 0.873])