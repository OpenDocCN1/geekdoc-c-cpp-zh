# Chapter 9

# Inheritance

# Learning Objectives

+   - Introduction to inheritance
+   - Implementation of inheritance in C++ object model
+   - Access specifiers and their use in inheritance
+   - Access declaration
+   - Multiple inheritance and their limitations
+   - Virtual base class
+   - Abstract classes
+   - Role of constructors and destructors in inheritance
+   - Advantages of memberwise initialization list (MIL)
+   - Exception handling during inheritance
+   - Composite and inherited objects

# 9.1 INTRODUCTION

Inheritance is an important feature of object-oriented programming. It is a mechanism to create a new class from an already defined class. The new class contains all the attributes of the old class in addition to some of its own attributes. In addition, it can also override some of the features of the old class.

Inheritance allows us to draw the functionalities of an already existing class and modify it to suit our requirement. There is no need to start from scratch. Another advantage is that a class once defined can be used multiple times by other applications after being inherited into a class that suits that application. In simple terms, inheritance allows reusability.

Proper use of inheritance helps in getting better and robust solutions quickly. For example, if one designs a class that helps to create and process windows on the screen, then the properties of the designed class can be extended to other applications that provide windows-based user interface. All such applications can inherit the designed class into a new class. The generic class may contain the caption of the window, specific borders, corners, size, look, and feel, and maybe minimize, maximize, and close buttons as well. The application may or may not need all these functionalities, or it may need some additional functionalities than what is provided in the generic class. The inheritance approach is better in this case because one has to concentrate only on the additional part and there is no need to start from scratch. It is more robust because the class one inherits from has already been used by others before, and bugs, if any, have higher probability of being found out and removed.

Inheritance is a mechanism to obtain a derived class from a base class. Such inheritance relationships are very common in the real-world scenario. For example, mammal is a class derived from living things, people is a class derived from mammal, man and woman are classes derived from people, and Indian people is also derived from people. In all these cases, the properties of the base class are automatically available in the derived class. People give birth to child. This attribute is derived from mammals. Indian people have two hands, two legs, etc., and this attribute is derived from people. Similar hierarchy is possible in C++ classes as well. Inheritance is the natural solution when such real-world hierarchy is to be modelled in a C++ program.

> Many real-world cases fall under the category of multiple inheritance. Modelling such hierarchy becomes simple in C++ because the feature comes inbuilt with the program.

> Object-based approach is more efficient than object-oriented approach. Hence, C++ applications generally choose the object-based approach when the stress is more on efficiency.