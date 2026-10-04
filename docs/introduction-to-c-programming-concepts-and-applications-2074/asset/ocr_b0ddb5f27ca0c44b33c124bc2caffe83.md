# Objects and Classes: Encapsulation in C++

+   IN THIS LECTURE:
Object-Oriented Programming
Program 16_1
Creating Classes
Sorting Data in Classes
Program 16_3_a
Program 16_3_b
Program 16_4
Program 16_5
Program 16_6
Public versus Private
Program 16_9_ERROR
Quiz
 Answers

Up until this point, the basic style of programming you've been learning is one you could have been doing in C, even though you've seen several C++-specific features that make things better. Called procedural programming, this style relies on functions, or procedures, to organize the computation. From now on, you'll need everything for you to learn one of the key advances in C++: object-oriented programming.

# // OBJECT-ORIENTED PROGRAMMING

There "pure" object-oriented languages before C++, and there have been languages developed after C++, such as Java, that only allow object-oriented programming. By contrast, C++ lets use both procedural and an object-oriented style. And compared to other languages that offer some of both, such as Python, C++ has a very complete set of object-oriented features. It enables you to program in a strict object-oriented style if you want to.

When you object-oriented programming, your development is centered around the creation of what are known as classes, which presents an overall way of organizing the computations in a program, where objects are particular instances of classes.

The feature of classes that is perhaps the most useful part of object-oriented programming is encapsulation.

Imagine that you want to write a program that would allow you to track what happens with a vending machine—money taken in, the number of items left inside, when it's time to reorder.

The focus in object-oriented programming is to identify objects. In the case of vending machines, any particular vending machine is an object. But you would like your program to handle vending machines more generally. So, you could also have a vending machine class—a way of referring to all vending machines.