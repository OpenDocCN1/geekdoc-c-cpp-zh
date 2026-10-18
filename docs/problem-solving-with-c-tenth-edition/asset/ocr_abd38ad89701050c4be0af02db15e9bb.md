![](bbox=[0.073, 0.055, 0.209, 0.165])

> > *With all appliances and means to boot.*
> >
> > WILLIAM SHAKESPEARE, *King Henry IV, Part III*

# INTRODUCTION

Object-oriented programming is a popular and powerful programming technique. Among other things, it provides for a new dimension of abstraction known as *inheritance*. This means that a very general form of a class can be defined and compiled. Later, more specialized versions of that class can be defined and can inherit all the properties of the previous class. Facilities for inheritance are available in all versions of C++.

# PREREQUISITES

Section 15.1 uses material from Chapters 2 to 8 and 10 to 12. Sections 15.2 and 15.3 use material from Chapters 9 and 13 in addition to Chapters 2 to 8, 10 to 12, and Section 15.1.

# 15.1 INHERITANCE BASICS

> > *If there is anything that we wish to change in the child, we should first examine it and see whether it is not something that could better be changed in ourselves.*
> >
> > CARL GUSTAV JUNG, *The Integration of the Personality*

One of the most powerful features of C++ is the use of inheritance to derive one class from another. **Inheritance** is the process by which a new class—known as a **derived class**—is created from another class, called the **base class**. A derived class automatically has all the member variables and functions that the base class has and can have additional member functions and/or additional member variables.

In Chapter 10, we noted that saying that class D is derived from another class B means that class D has all the features of class B and some extra, added features as well. When a class D is derived from a class B, we say that B is the base class and D is the derived class. We also say that D is the **child class** and B is the **parent class**.¹

¹ Some authors speak of a *subclass* D and *superclass* B instead of derived class D and base class B. However, we have found the terms *derived class* and *base class* to be less confusing. We only mention this in an effort to help you read other texts.