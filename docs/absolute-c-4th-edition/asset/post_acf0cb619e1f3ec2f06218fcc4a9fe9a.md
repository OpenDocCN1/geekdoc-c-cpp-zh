
inherited, so once a class has a virtual function table, then all its descendant classes have a virtual function table.)

Whenever an object of a class with one or more virtual functions is created, another pointer is added to the description of the object that is stored in memory. This pointer points to the class's virtual function table. When you make a call to a member function using a pointer (yep, another one) to the object, the runtime system uses the virtual function table to decide which definition of a member function to use; it does not use the type of the pointer.

Of course, this all happens automatically, so you need not worry about it. A compiler writer is even free to implement virtual functions in some other way as long as it works correctly (although it never actually is implemented in a different way).

## Self-Test Exercises

8. Why is the following illegal?

```
Pet vpet;
Dog vdog; //Dog is a derived class with base class Pet.
...
vdog = static_cast<Dog>(vpet); //ILLEGAL!
```

## Chapter Summary

- Late binding means that the decision of which version of a member function is appropriate is decided at runtime. In C++, member functions that use late binding are called virtual functions. *Polymorphism* is another word for late binding.
- A pure virtual function is a member function that has no definition. A pure virtual function is indicated by the word *virtual* and the notation = 0 in the member function declaration. A class with one or more pure virtual functions is called an *abstract class*.
- An abstract class is a type and can be used as a base class to derive other classes. However, you cannot create an object of an abstract class type (unless it is an object of some derived class).
- You can assign an object of a derived class to a variable of its base class (or any ancestor class), but the member variables that are not in the base class are lost. This is known as *the slicing problem*.
- If the domain type of the pointer pAncestor is a base class for the domain type of the pointer pDescendant, then the following assignment of pointers is allowed:

```
pAncestor = pDescendant;
```

Moreover, none of the data members or member functions of the dynamic variable being pointed to by pDescendant will be lost. Although all the extra fields of the dynamic variable are there, you will need virtual member functions to access them.

It is a good programming practice to make destructors virtual.

## ANSWERS TO SELF-TEST EXERCISES

- 1. In essence there is no difference among the three terms. They all refer to the same topic. There is only a slight difference in their usage. (Virtual function is a kind of member function, late binding refers to the mechanism used to decide which function definition to use when a function is virtual, and polymorphism is another name for late binding.)
- 2. The output would change to the following:
  
  Discounted item is not cheaper.
- 3. Yes, it is legal to have an abstract class in which all member functions are pure virtual functions.
- 4. a. Illegal, because Employee is an abstract class.
  b. Legal.
  c. Legal, because an abstract class is a type.
- 5. There would be no members to assign to the derived class's added members.
- 6. Although it is legal to assign a derived class object to a base class variable, this discards the parts of the derived class object that are not members of the base class. This situation is known as the slicing problem.
- 7. If the base class function carries the virtual modifier, then the derived class member function is called. If the base class member function does not have the virtual modifier, then the base class member function is called.
- 8. Since Dog can have more member variables than Pet, the object vpet may not have enough data for all the member variables of type Dog.

## PROGRAMMING PROJECTS

- 1. Consider a graphics system that has classes for various figures, say rectangles, squares, triangles, circles, and so on. For example, a rectangle might have data members height, width, and center point, while a square and circle might have only a center point and an edge length or radius, respectively. In a well-designed system these would be derived from a common class, Figure. You are to implement such a system.
  
  The class Figure is the base class. You should add only Rectangle and Triangle classes derived from Figure. Each class has stubs for member functions erase and draw. Each of these member functions outputs a message telling what function has been called and what the class of the calling object is. Since these are just stubs, they do nothing more than
  
  output this message. The member function center calls erase and draw to erase and redraw the figure at the center. Because you have only stubs for erase and draw, center will not do any "centering" but will call the member functions erase and draw. Also, add an output message in the member function center that announces that center is being called. The member functions should take no arguments. There are three parts to this project:
  
  a. Do the class definitions using no virtual functions. Compile and test.
  b. Make the base class member functions virtual. Compile and test.
  c. Explain the difference in results.

For a real example, you would have to replace the definition of each of these member functions with code to do the actual drawing. You will be asked to do this in Programming Project 2.

Use the following main function for all testing:

```
//This program tests Programming Problem 1.

#include <iostream>
#include "figure.h"
#include "rectangle.h"
#include "triangle.h"
using std::cout;
int main()
{
    Triangle tri;
    tri.draw();
    cout << "\nDerived class Triangle object calling center().\n";
    tri.center(); //Calls draw and center

    Rectangle rect;
    rect.draw();
    cout << "\nDerived class Rectangle object calling center().\n";
    rect.center(); //Calls draw and center
    return 0;
}
```

2. Flesh out Programming Problem 1. Give new definitions for the various constructors and member functions Figure::center, Figure::draw, Figure::erase, Triangle::draw, Triangle::erase, Rectangle::draw and Rectangle::erase so that the draw functions actually draw figures on the screen by placing the character '*' at suitable locations on the screen. For the erase functions, you can simply clear the screen (by outputting blank lines or by doing something more sophisticated). There are a lot of details in this and you will have to decide on some of them on your own.

For additional online Programming Projects, click the CodeMate icons below.

# 16 CHAPTER Templates

![](img/9505fd46e120aa9c1406715936ff6251_646_0.png)

- 16.1 FUNCTION TEMPLATES 654
- Syntax for Function Templates 656
- Pitfall: Compiler Complications 659
- Example: A Generic Sorting Function 661
- Tip: How to Define Templates 665
- Pitfall: Using a Template with an Inappropriate Type 665
  
- 16.2 CLASS TEMPLATES 667
- Syntax for Class Templates 667
- Example: An Array Template Class 671
- The vector and basic_string Templates 677
  
- 16.3 TEMPLATES AND INHERITANCE 678
- Example: Template Class for a Partially filled Array with Backup 678
- CHAPTER SUMMARY 684
- ANSWERS TO SELF-TEST EXERCISES 684
- PROGRAMMING PROJECTS 688

```
temp = variable1;
variable1 = variable2;
variable2 = temp;
}
```

Notice that the function swapValues applies only to variables of type int. Yet the algorithm given in the function body could just as well be used to swap the values in two variables of type char. If we want to also use the function swapValues with variables of type char, we can overload the function name swapValues by adding the following definition:

```
void swapValues(char& variable1, char& variable2)
{
    char temp;

    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

But there is something inefficient and unsatisfying about these two definitions of the swapValues function: They are almost identical. The only difference is that one definition uses the type int in three places and the other uses the type char in the same three places. Proceeding in this way, if we wanted to have the function swapValues apply to pairs of variables of type double, we would have to write a third almost identical function definition. If we wanted to apply swapValues to still more types, the number of almost identical function definitions would be even larger. This would require a good deal of typing and would clutter up our code with lots of definitions that look identical. We should be able to say that the following function definition applies to variables of any type:

```
void swapValues(Type_Of_The_Variables& variable1,
                Type_Of_The_Variables& variable2)
{
    Type_Of_The_Variables temp;

    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}
```

As we will see, something like this is possible. We can define one function that applies to all types of variables, although the syntax is a bit more complicated than what we have shown above. The proper syntax is described in the next subsection.
