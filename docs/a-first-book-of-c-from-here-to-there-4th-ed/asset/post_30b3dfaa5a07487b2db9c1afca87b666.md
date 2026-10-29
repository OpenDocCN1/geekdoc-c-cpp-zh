
## 10.6 Common Programming Errors

The common programming errors associated with constructing classes are as follows:

- 1. Failing to terminate the class declaration section with a semicolon.
- 2. Including a return type with the constructor's prototype or failing to include a return type with the other methods' prototypes.
- 3. Using the same name for a data member as for a member method.
- 4. Defining more than one default constructor for a class.
- 5. Forgetting to include the class name and scope operator, ::, in the header of all member methods defined in the class implementation section.
- 6. Using the static keyword when defining a static data member or member method. It should be used only in the class declaration section.
- 7. Using the friend keyword when defining a friend function. It should be used only in the class declaration section.
- 8. Failing to instantiate static data members before creating class objects that must access these data members.

## 10.7 Chapter Summary

- 1. A class is a programmer-defined data type. Objects of a class can be defined and have the same relationship to their class as variables do to C++'s built-in data types.
- 2. A class definition consists of declaration and implementation sections. The most common form of a class definition is as follows:

```
// class declaration section
class name
{
    private:
        // a list of variable declarations;
    public:
        // a list of method prototypes;
};
// class implementation section
// class method definitions
```

The variables and methods declared in the class declaration section are collectively called class members. The variables are referred to as class data members, and the methods are referred to as class member methods. The keywords private and public are access specifiers. After an access specifier is listed, it remains in force until another access specifier is given. The private keyword specifies that class members following it are private to the class and can be accessed only by member methods. The public keyword specifies that the class members following it can be accessed from outside the class. Generally, all data members should be specified as private and all member methods as public.

3. Class methods listed in the declaration section can be written inline, or their definitions can be included in the class implementation section. Except for constructor and destructor methods, all class methods defined in the class implementation section use this form for the header:

```
returnType className::methodName(parameter list);
```

Except for the addition of the class name and scope operator, ::, which are required to identify the method name with the class, this header is identical to the one for any user-written function.

4. A constructor is a special method that's called automatically each time an object is declared. It must have the same name as its class and can't have any return type. Its purpose is to initialize each declared object.

5. If no constructor is declared for a class, the compiler supplies a default constructor. It's a do-nothing method with the definition className::className(void) {}.

6. The term "default constructor" refers to any constructor that doesn't require arguments when it's called. The reason it doesn't require arguments is that no parameters are declared (as with the compiler-supplied default constructor) or all arguments have been given default values.

7. Each class can only have one default constructor. If a user-defined constructor is defined, the compiler doesn't create a default constructor.

8. Objects are created by using a C++ or C style of declaration. The C++ style of declaration has the form

```
className list-of-objectNames(list of initializers);
```

where the list of initializers is optional. An example of the C++ style, including initializers, for a class named Date is as follows:

```
Date a, b, c(12,25,2012);
```

The objects a and b are declared to be of type Date and are initialized by using the default constructor; the object c is initialized with the values 12, 25, and 2012.

The equivalent C style of declaration, including the optional list of initializers, has this form:

```
className objectName = className(list of initializers);
```

An example of the C style for a class named Date is as follows:

```
Date c = Date(12,25,2012)
```

The object c is created and initialized with the values 12, 25, and 2012.

9. Constructors can be overloaded in the same manner as any other user-written C++ method.

10. If a constructor is defined for a class, a user-defined default constructor should also be written, as the compiler doesn't supply it.

11. A destructor is called each time an object goes out of scope. Destructors must have the same name as their class but are preceded with a tilde (~). There can be only one destructor per class.

12. A destructor takes no arguments and returns no value. If a user-defined destructor isn’t included in a class, the compiler provides a do-nothing destructor.

13. Each class has an associated class scope, which is defined by the brace pair, {}, containing the class declaration. Data members and member methods are local to the scope of their class and can be used only by objects declared for the class. If a global variable name is reused in a class, the global variable is hidden by the class variable. Within the scope of the class variable, the global variable can be accessed by using the scope resolution operator, ::.

14. For each class object, a separate set of memory locations is reserved for all data members, except those declared as static. A static data member is shared by all class objects and provides a means of communication between objects. Static data members must be declared in the class declaration section and are defined outside the declaration section.

15. Static member methods apply to the class as a whole rather than to separate objects. Therefore, a static member method can access only static data members and other static member methods. Any static member methods must be declared in the class declaration section and are defined outside the declaration section.

16. A nonmember method can access a class’s private data members if it’s granted friend status by the class. This is done by declaring it as a friend in the class’s declaration section. Therefore, the class always determines which nonmember methods are friends; a method can never confer friend status on itself.

## 10.8 Chapter Supplement: Thinking in Terms of Objects

When solving any problem, often it’s helpful to start by creating a diagram or map or devising a theoretical analogy for the problem you’re trying to solve. In other words, you need to create some kind of model. Creating a model helps you see all parts of the problem and helps you understand what you need to do to solve it.

The first step in constructing an object-based program is developing an object-based model of the problem. Each class then becomes a description of the model written in C++. For example, if you’re writing an object-oriented program to calculate the area of a room, the first step is thinking about a room as an object. This step probably isn’t difficult, and assigning attributes of length, width, and height to a room correspond to physical characteristics you’re familiar with. To become a good object-oriented programmer, however, you need to be able to analyze more complex situations so that you can think of and organize programming problems as the interaction of different objects. In this section, you explore this object-based concept in more detail. You also learn how to develop programs systematically by using object-based models. Figure 10.7 illustrates the concepts discussed in this section.

![](img/e9bf940282dfb289356f077151cc69dd_505_0.png)

# Figure 10.8 An initial coin object description

As you expand your design for a program, often you have to refine and expand the object description. Refinement, or improving and modifying the model, is almost always required for all but extremely simple problems. In Section 12.6, you learn about a more structured approach to modeling, based on a methodology known as the Unified Modeling Language (UML). This methodology, like all object-oriented design and development techniques, requires identifying the necessary objects and then identifying the objects’ attributes and behaviors. After you build a model, you must then translate it into C++. The main point of this book is to teach you how to do just that. Your job as a programmer, however, will be much easier if you take the time first to master the techniques for modeling a program.

### Modeling Classes

Identifying the objects to be used in a program is only the first step in the modeling process. Attributes and behaviors actually define a category or type of object, out of which many objects can then be designated. For example, suppose you want to display a geometric object, such as a rectangle, onscreen. In its simplest representation, a rectangle has a shape and location, which can be represented by the object description in Figure 10.9.

![](img/e9bf940282dfb289356f077151cc69dd_505_1.png)

# Figure 10.9 An initial rectangle object description

Now you can refine this model to define more accurately what’s meant by shape and location. A rectangle’s shape attribute can actually be broken down into two more specific attributes: length and width. As for the behavior listed in Figure 10.9 (location), you can also break it down into more specific behaviors. For example, one approach might be listing the position of the rectangle’s upper-left corner in relation to the screen’s upper-left corner, and then do the same for the rectangle’s upper-right corner. These two positions, along with the rectangle’s length and width, are enough information to allow the program to generate a rectangle. However, simply specifying one location for the rectangle might not be enough. For example, you might want to give the rectangle the capability to move its position and change its length or width. Figure 10.10 shows a refined object description that takes this additional behavior into account.
