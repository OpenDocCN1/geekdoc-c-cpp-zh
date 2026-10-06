# 4 Class and Object

Everything in the real world we are familiar with is an object. Objects can not only be visible, as houses, cars, airplanes, animals and plants, but also be invisible, as a plan. Objects can be a simple unit, like a person; and they can also be a combination of several objects; for example, there are multiple departments in a company, and each department has staff members. A class can be formed based on common attributes abstracted from similar objects. These are the concepts and methods we are familiar with the real world. The aim of programming is to describe and solve problems in the real world, the first step is to describe objects and classes faithfully in programs. C++, an object-oriented programming language, supports this kind of abstraction. A class in C++ is formed by the encapsulation of abstracted data and functions.

In this chapter, we will first introduce the main features of object-oriented design: abstraction, encapsulation, and polymorphism. We then focus on the core concept of object-oriented design – class, which includes how to define and implement a class, and how to use classes to solve problems.

# 4.1 Basic Features of Object-Oriented Design

# 4.1.1 Abstraction

As a fundamental way to understand problems, abstraction is not new to us. Abstraction in the object-oriented method is a procedure in which specific issues (objects) are summarized and abstracted into the common attributes of a class of objects; it also includes the procedure of describing these attributes. The procedure of abstraction is also a procedure of analyzing and understanding problems. In the development of object-oriented software, we should find the specific procedure to solve it. Generally, the abstraction of a problem includes two types: abstraction of data and abstraction of behavior (or code). The former describes the attributes or states of a class of objects, i.e., the characteristics used to distinguish this class of objects from other classes; the latter describes the common behavior or functional characteristics of a class of objects.

Let us see two simple examples: first we implement a simple clock program on a computer. From the analysis of the clock can we see that we need three integers to store time, which represent the hour, minute, and second respectively. This is an abstraction of the data that a clock possesses. In addition, a clock needs some simple functions, such as time display and time setup. This is an abstraction of the behavior of the clock. Using variables and functions in C++, we can describe the abstracted attributes of a clock like:

https://doi.org/10.1515/9783110471977-004