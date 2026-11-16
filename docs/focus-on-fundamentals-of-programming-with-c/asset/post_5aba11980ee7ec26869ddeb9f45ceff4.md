
## Dynamic (Run-Time) Binding

```
for each figure x
x.display()
```

![](img/7f36c52b5170b89b142dbb7b1ea4666b_612_0.png)

## Dynamic (Run-Time) Binding

- Clearly, the correspondence between the operation DISPLAY and the FIGURE is determined at execution-time, rather than at compile-time.

- This process of delaying the determination of the actual method to be invoked until runtime is termed late binding or dynamic binding.

- In an object-oriented language with dynamic binding, we must again implement a DISPLAY method for each of the triangle, rectangle, square, and circle figures. However, the same name can be used in each case.

- Moreover, it is no longer the programmer's responsibility to determine the correct method to invoke. A programmer can send the message DISPLAY to any figure.

- Based on the type of FIGURE, the correct DISPLAY method will be invoked.

## Polymorphism Summary

- Permits the use of generic reusable code which is independent of the objects involved.
  - specify general instructions
  - delegate implementation to objects

- Fewer dependencies in code.

- Maintenance easier.

- Allows the overloading of names. The same name can be used throughout a system to denote a commonly used and well-understood operation.

- Early binding compiles the method's execution address at compile time. This is most efficient, but least flexible because an object's class must be known at compile time.

- Late binding leaves options open until runtime.

## Object-Oriented Languages

A language is object-oriented if it satisfies the following requirements:

- It supports objects that are data abstractions with an interface of named operations and a hidden local state (encapsulation)

- Objects inherit behavior from existing classes (inheritance)

- Objects determine at runtime how to respond to messages (polymorphism)

AN INTRODUCTION TO THE C PROGRAMMING LANGUAGE EMPHASIZING TOP-DOWN DESIGN AND PRINCIPLES OF STRUCTURED PROGRAMMING. LANGUAGE SYNTAX IS COVERED, TOGETHER WITH OPERATORS, STANDARD CONTROL STRUCTURES, FUNCTIONS, INPUT/OUTPUT, ARRAYS, STRINGS, FILE MANIPULATION, PRE-PROCESSOR, POINTERS, STRUCTURES, DYNAMIC VARIABLES, AND LINEAR LINKED LISTS.
