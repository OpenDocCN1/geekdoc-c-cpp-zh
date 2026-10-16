
example, suppose a program uses a class for vectors and one for matrices, and a subprogram is needed to multiply a matrix object by a vector object. In C++, the multiply function can be made a friend of both classes.

As previously stated, C++ provides multiple inheritance. As an example, suppose we wanted a class for drawing that needed the behavior of a class written for drawing figures and the methods of the new class needed to run in a separate thread. We might define the following:

```
class Thread { . . . };
class Drawing { . . . };
class DrawThread : public Thread, public Drawing { . . . };
```

Class DrawThread inherits all of the members of both Thread and Drawing. If both Thread and Drawing happen to include members with the same name, they can be unambiguously referenced in objects of class DrawThread by using the scope resolution operator (::). This example of multiple inheritance is shown in Figure 12.5.

Some issues with the C++ implementation of multiple inheritance are discussed in Section 12.5.

Overriding methods¹² in C++ must have exactly the same parameter profile as the overridden method. If there is any difference in the parameter profiles, the method in the subclass is considered a new method that is unrelated to the method with the same name in the ancestor class. The return type of the overriding method either must be the same as that of the overridden method or must be a publicly derived type of the return type of the overridden method.

## 12.4.2.3 Dynamic Binding

All of the member functions we have defined thus far are statically bound; that is, a call to one of them is statically bound to a function definition. A C++ object could be manipulated through a value variable, rather than a pointer or a reference. (Such an object would be static or stack dynamic.) However, in that

## Figure 12.5
Multiple inheritance

![](img/e382387aad0004c80a0dd0a70be9a623_533_0.png)

> 12. Recall that an overriding method is one that is defined in the derived class to replace a virtual method inherited from an ancestor class. Calls to an overriding method must be dynamically bound.

## Chapter 12 Support for Object-Oriented Programming

```
ptr_shape = sq; // Now ptr_shape points to a
// Square object
ptr_shape->draw(); // Dynamically bound to the draw
// in the Square class
rect->draw(); // Statically bound to the draw
// in the Rectangle class
```

This situation is shown in Figure 12.6.

Notice that the draw function in the definition of the base class shape is set to 0. This peculiar syntax is used to indicate that this member function is a pure virtual function, meaning that it has no body and it cannot be called. It must be redefined in derived classes if they call the function. The purpose of a pure virtual function is to provide the interface of a function without giving any of its implementation. Pure virtual functions are usually defined when an actual member

![](img/e382387aad0004c80a0dd0a70be9a623_535_0.png)

| Types | Pointers | Bindings | Objects |
|-------|----------|----------|---------|
| Shape* | ptr_shape | → Square | Square |
| Square* | sq | → Square | Square |
| Rectangle* | rect | → Rectangle | Rectangle |

definition and the derivation access controls, and also the possibility of friend functions and friend classes, the C++ programmer has highly detailed control over access to class members. Although C++ provides multiple inheritance and Smalltalk does not, there are many who feel that is not an advantage for C++. The downsides of multiple inheritance weigh heavily against its value. In fact, C++ is the only language discussed in this chapter that supports multiple inheritance. On the other hand, languages that provide alternatives to multiple inheritance, such as Objective-C, Java, and C#, clearly have an advantage over Smalltalk in that area.

In C++, the programmer can specify whether static binding or dynamic binding is to be used. Because static binding is faster, this is an advantage for those situations where dynamic binding is not necessary. Furthermore, even the dynamic binding in C++ is fast when compared with that of Smalltalk. Binding a virtual member function call in C++ to a function definition has a fixed cost, regardless of how distant in the inheritance hierarchy the definition appears. Calls to virtual functions require only five more memory references than statically bound calls (Stroustrup, 1988). In Smalltalk, however, messages are always dynamically bound to methods, and the farther away in the inheritance hierarchy the correct method is, the longer it takes. The disadvantage of allowing the user to decide which bindings are static and which are dynamic is that the original design must include these decisions, which may have to be changed later.

The static type checking of C++ is an advantage over Smalltalk, in which all type checking is dynamic. A Smalltalk program can be written with messages to nonexistent methods, which are not discovered until the program is executed. A C++ compiler finds such errors. Compiler-detected errors are less expensive to repair than those found in testing.

Smalltalk is essentially typeless, meaning that all code is effectively generic. This provides a great deal of flexibility, but static type checking is sacrificed. C++ provides generic classes through its template facility (as described in Chapter 11), which retains the benefits of static type checking.

The primary advantage of Smalltalk lies in the elegance and simplicity of the language, which results from the single philosophy of its design. It is purely and completely devoted to the object-oriented paradigm, devoid of compromises necessitated by the whims of an entrenched user base. C++, on the other hand, is a large and complex language with no single philosophy as its foundation, except to support object-oriented programming and include the C user base. One of its most significant goals was to preserve the efficiency and flavor of C while providing the advantages of object-oriented programming. Some people feel that the features of this language do not always fit well together and that at least some of the complexity is unnecessary.

According to Chambers and Ungar (1991), Smalltalk ran a particular set of small C-style benchmarks at only 10 percent of the speed of optimized C. C++ programs require only slightly more time than equivalent C programs (Stroustrup, 1988). Given the great efficiency gap between Smalltalk and C++, it is little wonder that the commercial use of C++ is far more widespread than that

to the subclass. Recall that although access to methods can be controlled by specifiers in C++, in Objective-C all methods are public, and that cannot be changed. A method that is defined in the subclass and has the same name, same return type, and same number and types of parameters overrides the inherited method. The overridden method can be called in another method of the subclass through super, a reference to the parent object. There is no way to prevent the overriding of an inherited method. Because all public members of a base class are also public in subclasses derived from that base class, all subclasses can be subtypes.

As in Smalltalk, in Objective-C any method name can be called on any object. If the run-time system discovers that the object has no such method (with the proper protocol), an error occurs.

Objective-C does not support the private and protected derivations of C++. As in other languages that support object-oriented programming, the constructor of an instance of a subclass should always call the constructor of the parent class before doing anything else. If the name of the parent class constructor is init, this is done with the following statement:

```
[super init];
```

Objective-C includes two ways to extend a class besides subclassing: categories and protocols. A collection of methods can be added to a class with a construct called a category. A category is a secondary interface of a class that contains declarations of methods. No new instance variables can be included in the secondary interface. The syntactic form of such an interface is exemplified by the following:

```
#import "Stack.h"
@interface Stack (StackExtend)
- (int) secondFromTop;
- (void) full;
@end
```

The name of this category is StackExtend. The original interface is accessible because it is imported, so the parent class need not be mentioned. The new methods are mixed into the methods of the original interface. Consequently, categories are sometimes called mixins. Mixins are sometimes used to add certain functionalities to different classes. And, of course, the class still has a normal superclass from which it inherits members. So, mixins provide some of the benefits of multiple inheritance, without the naming collisions that could occur if modules did not require module names on their functions. Of course, a category must also have an implementation section, which includes the name of the category in parentheses after the class name on the implementation directive, as in the following:

```
@implementation Stack (StackExtend)
```

The implementation need not implement all of the methods in the category.
