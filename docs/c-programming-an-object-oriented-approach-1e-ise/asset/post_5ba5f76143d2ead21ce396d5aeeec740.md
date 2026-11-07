
## 7 User-Defined Types: Classes

This is the first chapter in which we use C++ as an object-oriented language. In previous chapters we discussed the basics, and we will need what we learned in those chapters to understand the materials we use in this chapter and the rest of the book. In this chapter, we show how to create new types and how to use them. The mechanism for creating new types uses a *class* or an enumerated type. We will discuss classes in this chapter but we will ignore discussion on enumerated types because they are not common.

**Objectives**

After you have read and studied this chapter, you should be able to:

- Introduce object-oriented concepts, including types and instances, attributes and behaviors, and data members and member functions.
- Discuss the class definition that declares data members and member functions.
- Discuss three types of constructors: parameter constructors, default constructors, and copy constructors.
- Discuss destructors that are used to clean up the objects before they are recycled.
- Discuss instance data members and instance member functions.
- Discuss static data members and static member functions.
- Discuss how we divide the three sections of a program into three separate files—interface file, implementation file, and application file—and achieve one of the goals of object-oriented programming: encapsulation.

### 7.1 INTRODUCTION

In Chapter 1, we mentioned that C++ is a combination of a procedural and an object-oriented language. In previous chapters, we have used the language mostly as a procedural language; in this chapter we start using it as an object-oriented language.

#### 7.1.1 Types and Instances in Real Life

A *type* is a concept from which an *instance* is created. In other words, a type is an abstraction; an **instance** of that type is a concrete entity. The word *clock* is a type; it defines a general concept that we are familiar with. The clock in John's office, the clock in Sue's office, or the clock in a train station are instances of this type. The word *circle* is a type. We can draw circles with different radii as instances of that type. We can even go further and say that the word *person* is a type, and that John, Sue, and Michelle are instances of the type person.

The relationship between a type and its instances is a one-to-many relation. We can have many instances from one single type. Figure 7.1 shows the type *Circle* and four instances that we call *circle1*, *circle2*, *circle3*, and *circle4*.

![](img/d68f6199646ca63591a6d8419e0ed4ba_292_0.png)

**Figure 7.1** A type and its instances

Any instance we encounter in this world has a set of attributes and a set of behaviors.

##### Attributes

In real life an attribute is a characteristic ascribed to an instance. In computer science, an attribute is any characteristic that interests us in an instance. For example, if the instance is an employee, we may be interested only in the employee’s *name*, *address*, *position*, and *salary*. On the other hand, if the instance is a student in a university, we may be interested only in the student’s *name*, *year*, *courses taken*, and *grades*. If the instance is a circle, we may be interested only in its *radius*, *perimeter*, and *area*.

> An attribute is a characteristic of an instance that we are interested in.

##### Behaviors

When we think about instances, we also think about their behaviors. In this sense, a *behavior* is an operation that an instance can perform on itself. For example, if an instance is an employee, we assume that she can give her *name*, her *address*, and her *salary*. On the other hand, if an instance is a circle, we assume that it can give its *radius*, its *perimeter*, and its *area*. Note that in object-oriented programming, we assume that an instance is capable of performing an operation on itself.

> A behavior is an operation that we assume an instance can perform on itself.

#### 7.1.2 Classes and Objects in Programs

In object-oriented programming, we still use the terms *type* and *instance*. In C++, a user-defined type can be created using a construct named *class*. An instance of a class is referred to as an *object*. This means that we use *type* and *class*. We also use *instances* and *objects*. In object-oriented programming, attributes and behaviors of an object are represented as *data members* and *member functions*.

##### Data Members

A **data member** of an object is a variable whose value represents an attribute. For example, the radius of a circle object can be represented by the value of a variable of type *double*. In other words, the attribute of an object of type *circle* can be effectively represented as a variable of type *double* that holds the value of the radius for that instance. However, some attributes of an instance are not independent; they may depend on values of other attributes. For example, the perimeter and the area of a circle may be two attributes for a mathematician, but we do not represent them as data members because both depend on the value of the radius.

![](img/d68f6199646ca63591a6d8419e0ed4ba_293_0.png)

**Figure 7.2** Comparison of terms in real life and in object-oriented programming

> **Attributes of an object in object-oriented programming**  
> **are simulated using data members.**

##### Member Function

In programming, a function is an entity that can do something. A **member function** in object-oriented programming is a function that simulates one of the behaviors of an object. For example, we can write a function that allows a circle to give its radius, its area, and its perimeter. We can also write a function that a circle can use to set its radius, but we should be aware of dependent attributes when we do so.

> **Behaviors of an object in object-oriented programming**  
> **are simulated using member functions.**

#### 7.1.3 Comparison

Figure 7.2 shows the terms we use in real life and in object-oriented programming. The figure can be used throughout the chapter to better understand the concepts we discuss.

![](img/d68f6199646ca63591a6d8419e0ed4ba_294_0.png)

**Figure 7.3** Three sections of a C++ program in object-oriented paradigm

### 7.2 CLASSES

Although C++ has many predefined (built-in) types such as *int*, *double*, *char*, and *bool*, it also allows programmers to create new types. In C++, new types are mostly created using a **class**. To write object-oriented programs, we need to create a class, as a type, and then instantiate objects as instances of that type. In procedural programming, we need only write an *application* program (the *main* function and some other functions) to use objects of built-in types. In object-oriented programming we need three sections: the *class definition*, the *member function definition*, and the *application* (which uses the objects created from the class). In other words, if we want to write object-oriented programs versus writing procedural programs, we should always think about these three sections. We will see that sometimes each section is designed and saved by different entities. We have seen that in some cases, the first two sections (class definition and member function definitions) are created and stored in the C++ library (like the string and file classes), but the principle is the same: We need all three sections, as shown in Figure 7.3.

In the *class definition* section, we declare the data members and member functions. In the *member function definition* section, we define all member functions. In the *application* section, we instantiate objects and apply the member function to those objects.

#### 7.2.1 An Example

Before we formally discuss these three sections, we use them in Program 7.1. We know that there are many issues that we have not discussed yet, but the program will be used to discuss them gradually.

**Program 7.1** Creating and handling two circle objects

```cpp
/*****************************************************
 * A program to use a class in object-oriented programming
 *****************************************************/
#include <iostream>
using namespace std;
/*****************************************************
 * Class definition: the declaration of data members and member
 * functions of the class
 *****************************************************/
class Circle
{
  private:
    double radius;
  public:
    double getRadius() const;
    double getArea() const;
    double getPerimeter() const;
    void setRadius(double value);
};
/*****************************************************
 * Member function definition. Each function declared in the
 * class definition section is defined in this section.
 *****************************************************/
// Definition of getRadius member function
double Circle::getRadius() const
{
  return radius;
}
```
