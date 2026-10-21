
# Chapter 9
# Inheritance

## Learning Objectives

- Introduction to inheritance
- Implementation of inheritance in C++ object model
- Access specifiers and their use in inheritance
- Access declaration
- Multiple inheritance and their limitations
- Virtual base class
- Abstract classes
- Role of constructors and destructors in inheritance
- Advantages of memberwise initialization list (MIL)
- Exception handling during inheritance
- Composite and inherited objects

## 9.1 INTRODUCTION

Inheritance is an important feature of object-oriented programming. It is a mechanism to create a new class from an already defined class. The new class contains all the attributes of the old class in addition to some of its own attributes. In addition, it can also override some of the features of the old class.

Inheritance allows us to draw the functionalities of an already existing class and modify it to suit our requirement. There is no need to start from scratch. Another advantage is that a class once defined can be used multiple times by other applications after being inherited into a class that suits that application. In simple terms, inheritance allows reusability.

Proper use of inheritance helps in getting better and robust solutions quickly. For example, if one designs a class that helps to create and process windows on the screen, then the properties of the designed class can be extended to other applications that provide windows-based user interface. All such applications can inherit the designed class into a new class. The generic class may contain the caption of the window, specific borders, corners, size, look, and feel, and maybe minimize, maximize, and close buttons as well. The application may or may not need all these functionalities, or it may need some additional functionalities than what is provided in the generic class. The inheritance approach is better in this case because one has to concentrate only on the additional part and there is no need to start from scratch. It is more robust because the class one inherits from has already been used by others before, and bugs, if any, have higher probability of being found out and removed.

Inheritance is a mechanism to obtain a derived class from a base class. Such inheritance relationships are very common in the real-world scenario. For example, mammal is a class derived from living things, people is a class derived from mammal, man and woman are classes derived from people, and Indian people is also derived from people. In all these cases, the properties of the base class are automatically available in the derived class. People give birth to child. This attribute is derived from mammals. Indian people have two hands, two legs, etc., and this attribute is derived from people. Similar hierarchy is possible in C++ classes as well. Inheritance is the natural solution when such real-world hierarchy is to be modelled in a C++ program.

> Many real-world cases fall under the category of multiple inheritance. Modelling such hierarchy becomes simple in C++ because the feature comes inbuilt with the program.

> Object-based approach is more efficient than object-oriented approach. Hence, C++ applications generally choose the object-based approach when the stress is more on efficiency.

Finding common attributes of real classes and creating an abstract class of such common attributes is called the bottom-up design approach.

Finding common attributes of real classes and creating an abstract class of such common attributes is called the bottom-up design approach. This approach reduces the possibility of redundant data. In the given example, if there are 10 types of Student objects and the Student base class is not used, then the data (phone number) is to be kept at 10 places (10 classes), whereas in the second case, only the Student class contains it.

Redundancy reduction also reduces the code size and the chances of errors. It also adds to flexibility. Later on, if a BCAStudent class needs to be added, the normal attributes are in place. One just needs to inherit the BCAStudent class from the Student class and then add to the inherited class only the new items needed.

## 9.2.3 Mapping a Real-world Hierarchy

We have natural inheritance in a real-world situation. Objects such as rectangle and ellipse are shapes that are derived from the shape concept. Square is a concept derived from rectangle, whereas circle is a concept derived from ellipse. C++ provides the inheritance mechanisms to map these hierarchies as it is in its programs. This facility of C++ makes the programs more intuitive and readable.

## 9.3 IS-A AND PART OF RELATIONSHIPS

When it is possible to inherit and reuse a class, one may be tempted to do so arbitrarily. It is important to have some form of subset relationship between a derived class and the base class. All the examples mentioned earlier have subset relationships. A subset relationship is also known as an is-a relationship. At times, one may be confused between an is-a and a part of relationship.

In the CDialog example described earlier, MyDialog is a subset of CDialog whereas it is a part of the Employee class. We will be looking at the differences in details in Section 9.15.

It is important to note that it requires programming discipline not to inherit when the relationship is not a subset of or is-a. If one needs to use functions that are defined in that class, it is better to rewrite them in the new class or design in such a way that such inheritance does not take place.

> Note Though it is said time and again that inheritance provides reusability, it does not mean that it should be deployed whenever one needs to reuse. Inheritance must be used in a disciplined way only in places where the is-a relationship holds true.

## Meaning of Inheritance in C++

When a class is declared as derived from some other class, the data members of the class are made available to the derived class without redefining. The type of inheritance used determines which data members are available and in which form. This is also determined by the original access specifiers (private, public, or protected) associated with the base class members. We will be studying three different types of inheritance in this chapter and will be exploring the forms of inheritance in the following sections.

## 9.4 DEFINING DERIVED CLASSES

Let us have a look at an example of inheritance to understand the concept. We start with the simplest type of inheritance. Assume that there is a single base class from which a new class
is derived. The syntax of the derivation is very simple. If one has to derive a DerivedClass from a BaseClass, it needs to be specified while defining the DerivedClass. The syntax for defining the DerivedClass is as follows:

```
class DerivedClass : <access modifier> BaseClass;
```

Here, the access modifier can be either public, private, or protected. Some authors also use the word visibility mode to represent the types of these access modifiers. We have already studied public and private access modifiers. We will be learning about protected access specifier in Section 9.4.3.

### 9.4.1 Derivation using Public Access Modifier

If the program has the following statements

```
class Base
{
    // Body of the base
}

class Derived : public Base
{
    // Body of the derived
}
```

then the derivation is known as public derivation. The members of the base class are now treated as follows:

- 1. The public members of the base class are treated as the public members of the derived class.
- 2. The private members are not inherited.
- 3. If some members have been defined as protected in the base class, they are available as protected in the derived class.

This can be understood better with the help of Program 9.1.

## PROGRAM 9.1 Inheriting publicly

```
//PublicInheritance.cpp
class Base
{
    int PrivateBaseInt;
public:
    int PublicBaseInt;
    void SetPrivateBaseInt(int Value)
    {
        PrivateBaseInt = Value;
    }
};

// Public derivation
class DerivedPublic : public Base
{
    int PrivateDerivedInt;
public:
    int PublicDerivedInt;
```
