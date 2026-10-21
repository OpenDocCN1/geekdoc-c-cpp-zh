# Chapter 5

# Constructors and Destructors

# Learning Objectives

+   - Application of constructors and destructors
+   - Default constructors
+   - User-defined default constructors
+   - Single-argument constructors
+   - Explicit constructors
+   - Parameterized constructors
+   - Multiple constructors
+   - Default arguments
+   - Constructors with dynamic allocation
+   - Copy constructors
+   - Member-wise initialization list (MIL) and its applications
+   - Lifetime of objects

# 5.1 SIMILAR-TO-BUILT-IN BEHAVIOUR CONCEPT

One of the major thrusts during C++ design was to make the user-created C++ objects behave in a similar way to the built-in objects as much as possible. C++ provides a host of facilities to make this possible such as the automatic initialization (and destruction) of data types. Let us try to understand this with an example. When we write int i = 25 in a C++ program, it is similar to writing int i(25). Here, i is initialized with the value 25 while being defined.

It is possible to write the following statement to initialize CaptainStudent while defining it:

```
student CaptainStudent(1, "Brian Lara", "West Indies");
```

Constructors are special functions that provide this service; they enable us to initialize user-defined objects while defining them, as shown in the examples. Suppose a class for customer has already been defined. It is possible to write

```
customer Javed("Miandad", "Pakistan", "Cricketer", "Cricket bats");
```

which not only defines Javed to be a customer, but also initializes his data such as the surname, address, category, and what items he is interested in. We have used the Init function in Chapter 4 in Programs 4.13, 4.14, 4.16 and 4.17 involving the class employee. A constructor for providing the same services in an automated way can be written to replace the Init function.

Once proper constructors are introduced in the class, the need for object initialization automatically arises.

# 5.2 NEED FOR OBJECT INITIALIZATION

The need for initialization of objects arises from various reasons, some of which are listed as follows:

+   1. When an object is declared, it may be needed to initialize the individual data members to some specific default values. Initializing integer variables to zero and pointer variables to null are two very common initializations. For example, when a stack object is defined, the stack pointer may be initialized to null using a constructor. The following is a sample from the program given in Section 5.3: