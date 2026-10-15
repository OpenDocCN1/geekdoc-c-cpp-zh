# 22. Interpreter Pattern

In this chapter I would like to demonstrate the usage of Interpreter pattern. This is not a widely used pattern but reveals a good way of programming. It says about creating a language along with an interpreter for the language. The language can be used to represent states, actions, loops etc. depending on the programming requirement. Here we are using the pattern to resolve a persistence problem.

# Challenge

You are working on a Drawing application which allows creating lines and circles on a canvas. The classes Line and Circle do the job for you. You need to communicate the drawing with multiple users who have their own copy of the application. The current persistence of drawing using serialization of the above classes is creating large sized files and does not allow sending the message over a chat window. How to provide a better solution for persistence with smaller size and easier communication?

# Definition

GoF Definition: "Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the language"

# Implementation

We can use the Interpreter pattern to approach the problem. We need to construct a language to include the commands and an interpreter to execute the actions.

![](bbox=[0.18, 0.59, 0.83, 0.77])

Following are the classes involved for our drawing application:

+   - A Line Class
+   - A Circle Class