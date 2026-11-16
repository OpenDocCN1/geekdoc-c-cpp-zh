# # Chapter 14

# # Custom Objects

In earlier times programmers wrote software in the machine language of the computer system because compilers had yet to be invented. The introduction of variables in association with higher-level programming languages marked a great step forward in the late 1950s. No longer did programmers need to be concerned with the lower-level details of the processor and absolute memory addresses. Named variables and functions allow programmers to abstract away such machine-level details and concentrate on concepts such as integers and characters that transcend computer electronics. Objects provide a level of abstraction above that of simple variables. Objects allow programmers to go beyond simple values—developers can focus on more complex things like geometric shapes, bank accounts, and aircraft wings. Programming objects that represent these real-world things can possess capabilities that go far beyond the simple variables we have studied to this point.

A C++ object typically consists of a collection of data and code. By bundling data and code together, objects store information and provide services to other parts of the software system. An object forms a computational unit that makes up part of the overall computer application. A programming object can model a real-world object more naturally than a collection of simple variables since it can encapsulate considerable complexity. Objects make it easier for developers to build complex software systems.

C++ is classified as an object-oriented language. Most modern programming languages have some degree of object orientation. This chapter shows how programmers can define, create, and use custom objects.

# ## 14.1 Object Basics

Consider the task of dealing with geometric points. Mathematicians represent a single point as an ordered pair of real numbers, usually expressed as (x, y). In C++, the double type serves to approximate a subset of the mathematical real numbers. We can model a point with coordinates within the range of double-precision floating-point numbers with two double variables. We may consider a point as one thing conceptually, but we here we would be using two variables. As a consequence, a function that computes the distance between two points requires four parameters—x1, y1, x2, and y2—rather than two points—(x1, y1) and (x2, y2). Ideally, we should be able to use one variable to represent a point.

One approach to represent a point could use a two-element vector, for example:

```
std::vector<double> pt { 3.2, 0.0 };
```