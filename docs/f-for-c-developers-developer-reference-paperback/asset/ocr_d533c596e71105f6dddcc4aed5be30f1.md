The design pattern is the reusable solution template for a problem. It can speed up the development process by providing tested, proven development paradigms. The effective software design requires considering problems that may not become obvious until later in the implementation. Reusing design patterns helps to prevent subtle issues that can cause major problems, and it improves code readability for coders and architects who are familiar with the patterns.

From the preceding statements, you can see that design patterns are not necessarily tied to specific languages or programming paradigms. Given that the object-oriented programming (OOP) paradigm is the most used, most design-pattern implementations and discussions are based on languages that target OOP—for example, some people from the functional programming community have suggested that design patterns are merely a means to address flaws in OOP languages. I will not go into the details of this topic, instead, I will cover how to use F# to implement patterns.

First, I'll cover three basic concepts in programming languages that primarily target OOP:

+   * Encapsulation is a construct that facilitates the bundling of data with methods (or functions) that operate on that data.

+   * Inheritance is a way to compartmentalize and reuse code. It creates a subtype based on an existing type.

+   * Polymorphism: subtype polymorphism, which is almost universally just polymorphism in the context of object-oriented programming, is the ability to create a variable, function, or an object that has more than one form.

The typical C# implementations of design patterns often use three of these concepts. In the rest of the chapter, you will see how F# can use both OOP and functional features to implement most common design patterns.

Before demonstrating these design patterns, I'd like to remind you that a design pattern can have more than one implementation. Each of the implementations in the following examples shows different F# language features in practice. Additionally, they provide a better way to apply F# in competency or system design than would be achieved by simply portant over a C# implementation.

# Working with F# and Design Patterns

Let's start by looking at some of the design patterns that will be discussed in this chapter along with the definitions of each. Note that the following definitions are from an OOP perspective, so the definitions occasionally use object-oriented terminology:

+   * The chain of responsibility pattern avoids coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. It chains the receiving objects and passes the request along the chain until an object handles it.