# 13. Flyweight Pattern

In this chapter we are discussing about Flyweight Design Pattern. It is one among the 23 design patterns and provides an improved way of managing objects.

# Challenge

You are working on an Id Card Creation web application. The application has 1 lakh Student records for which Id Cards to be created.

Following is the StudentCard class that performs the id card generation. We need to call the GenerateIdCard() method to get the Id Card image after assigning the student Name, Address, Photo properties. Each card image generated is saved to file system.

![](bbox=[0.18, 0.35, 0.36, 0.53])

The problem is the 1 Lakh class instances created. How to reduce the number of instances?

# Definition

GoF Definition: "Use sharing to support large numbers of fine-grained objects efficiently"

# Implementation

Using Flyweight pattern we can solve the above problem. We can see from the above problem that at a time only one instance is needed.

We can use only one instance of StudentCard class and share it inside the loop to assign the properties and generate id card.