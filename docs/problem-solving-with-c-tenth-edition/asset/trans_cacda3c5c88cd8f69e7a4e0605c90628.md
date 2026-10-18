

(when you do not define =); it will not have anything to do with the base class assignment operator defined in Base.

It is natural that constructors, destructors, and the assignment operator are not inherited. To correctly perform their tasks, they need information that the base class does not possess. To correctly perform their functions, they need to know about the new member variables introduced in the derived class.

## Assignment Operators and Copy Constructors in Derived Classes

Overloaded assignment operators and constructors are not inherited. However, they can be, and in almost all cases must be, used in the definitions of overloaded assignment operators and copy constructors in derived classes.

When overloading the assignment operator in a derived class, you normally use the overloaded assignment operator from the base class. We will present an outline of how the code for doing this is written. To help understand the code outline, remember that an overloaded assignment operator must be defined as a member function of the class.

If Derived is a class derived from Base, then the definition of the overloaded assignment operator for the class Derived would typically begin with something like the following:

```
Derived& Derived::operator =(const Derived& rightSide)
{
    Base::operator =(rightSide);
}
```

The first line of code in the body of the definition is a call to the overloaded assignment operator of the Base class. This takes care of the inherited member variables and their data. The definition of the overloaded assignment operator would then go on to set the new member variables that were introduced in the definition of the class Derived.

A similar situation holds for defining the copy constructor in a derived class. If Derived is a class derived from Base, then the definition of the copy constructor for the class Derived would typically use the copy constructor for the class Base to set up the inherited member variables and their data. The code would typically begin with something like the following:

```
Derived::Derived(const Derived& object)
    : Base(object), <probably more initializations>
{
```

The invocation of the base class copy constructor Base(object) sets up the inherited member variables of the Derived class object being created. Note that since object is of type Derived, it is also of type Base; therefore, object is a legal argument to the copy constructor for the class Base.

Of course, these techniques do not work unless you have a correctly functioning assignment operator and a correctly functioning copy constructor for the base class. This means that the base class definition must include a copy constructor and that either the default automatically created assignment operator must work correctly for the base class or the base class must have a suitable overloaded definition of the assignment operator.

## Destructors in Derived Classes

If a base class has a correctly functioning destructor, then it is relatively easy to define a correctly functioning destructor in a class derived from the base class. When the destructor for the derived class is invoked, it automatically invokes the destructor of the base class, so there is no need for the explicit writing of a call to the base class destructor; it always happens automatically. The derived class destructor therefore need only worry about using delete on the member variables (and any data they point to) that are added in the derived class. It is the job of the base class destructor to invoke delete on the inherited member variables.

If class B is derived from class A and class C is derived from class B, then when an object of the class C goes out of scope, first the destructor for the class C is called, then the destructor for class B is called, and finally the destructor for class A is called. Note that the order in which destructors are called is the reverse of the order in which constructors are called.

## SELF-TEST EXERCISES

- 7. You know that an overloaded assignment operator and a copy constructor are not inherited. Does this mean that if you do not define an overloaded assignment operator or a copy constructor for a derived class, then that derived class will have no assignment operator and no copy constructor?

- 8. Suppose Child is a class derived from the class Parent, and the class Grandchild is a class derived from the class Child. This question is concerned with the constructors and destructors for the three classes Parent, Child, and Grandchild. When a constructor for the class Grandchild is invoked, what constructors are invoked and in what order? When the destructor for the class Grandchild is invoked, what destructors are invoked and in what order?

- 9. Give the definitions for the member function addValue, the copy constructor, the overloaded assignment operator, and the destructor for the following class. This class is intended to be a class for a partially filled array. The member variable numberUsed contains the number of array positions currently filled. The other constructor definition is given to help you get started.

```
#include <iostream>
#include <cstdlib>
using namespace std;

class PartFilledArray
{
public:
    PartFilledArray(int arraySize);
    PartFilledArray(const PartFilledArray& object);
    ~PartFilledArray();
    void operator=(const PartFilledArray& rightSide);
    void addValue(double newEntry);
    //There would probably be more member functions
    //but they are irrelevant to this exercise.
protected:
    double *a;
    int maxNumber;
    int numberUsed;
};
PartFilledArray::PartFilledArray(int arraySize)
    : maxNumber(arraySize), numberUsed(0)
{
    a = new double[maxNumber];
}
```

(Many authorities would say that the member variables should be private rather than protected. We tend to agree. However, using protected makes for a better practice assignment, and you should have some experience with protected variables because some programmers do use them.)

- 10. Define a class called PartFilledArrayWMax that is a derived class of the class PartFilledArray. The class PartFilledArrayWMax has one additional member variable named maxValue that holds the maximum value stored in the array. Define a member accessor function named getMax that returns the maximum value stored in the array. Redefine the member function addValue and define two constructors, one of which has an int argument for the maximum number of entries in the array. Also define a copy constructor, an overloaded assignment operator, and a destructor. (A real class would have more member functions, but these will do for an exercise.)

## 15.3 POLYMORPHISM

> All experience is an arch, to build upon.
> HENRY ADAMS, The Education of Henry Adams

Polymorphism refers to the ability to associate multiple meanings to one function name. As it has come to be used today, polymorphism refers to a very particular way of associating multiple meanings to a single function name.

That is, **polymorphism** refers to the ability to associate multiple meanings to one function name by means of a special mechanism known as *late binding*. Polymorphism is one of the key components of a programming philosophy known as *object-oriented programming*. Late binding, and therefore polymorphism, is the topic of this section.

### Late Binding

A *virtual function* is one that, in some sense, may be used before it is defined. For example, a graphics program may have several kinds of figures, such as rectangles, circles, ovals, and so forth. Each figure might be an object of a different class. For example, the Rectangle class might have member variables for a height, width, and center point, while the Circle class might have member variables for a center point and a radius. In a well-designed programming project, all of them would probably be descendants of a single parent class called, for example, Figure. Now, suppose you want a function to draw a figure on the screen. To draw a circle, you need different instructions from those you need to draw a rectangle. So, each class needs to have a different function to draw its kind of figure. However, because the functions belong to the classes, they can all be called draw. If r is a Rectangle object and c is a Circle object, then r.draw( ) and c.draw( ) can be functions implemented with different code. All this is not news, but now we move on to something new: *virtual functions* defined in the parent class Figure.

Now, the parent class Figure may have functions that apply to all figures. For example, it might have a function called center that moves a figure to the center of the screen by erasing it and then redrawing it in the center of the screen. Figure::center might use the function draw to redraw the figure in the center of the screen. When you think of using the inherited function center with figures of the classes Rectangle and Circle, you begin to see that there are complications here.

To make the point clear and more dramatic, let’s suppose the class Figure is already written and in use and at some later time we add a class for a brand-new kind of figure, say, the class Triangle. Now, Triangle can be a derived class of the class Figure, and so the function center will be inherited from the class Figure; thus, the function center should apply to (and perform correctly for!) all Triangles. But there is a complication. The function center uses draw, and the function draw is different for each type of figure. The inherited function center (if nothing special is done) will use the definition of the function draw given in the class Figure, and that function draw does not work correctly for Triangles. We want the inherited function center to use the function Triangle::draw rather than the function Figure::draw. But the class Triangle, and therefore the function Triangle::draw, was not even written when the function center (defined in the class Figure) was written and compiled! How can the function center possibly work correctly for Triangles? The compiler did not know anything about Triangle::draw at

