```
```
x=1
y=2
Program Over
```
```

In Listing 10, the NumberInitialization class is created that has a constructor called NumberInitialization() to initialize the private members of the class.

Some characteristics of constructors are given as follows:

+   - Constructors are functions but their names must be the same as that of their class names.
+   - Constructors are intended to initialize the members of the class when an instance of that class is created.
+   - Constructors are invoked automatically when the objects are created.
+   - Similar to functions, constructors can have default arguments.
+   - Constructors do not have return types, therefore, they cannot return values.
+   - Constructors cannot be inherited.
+   - Constructors cannot be `virtual`.
+   - Multiple constructors for the same class can be defined. They must have different parameters to distinguish them.
+   - Constructors make implicit call to the `new` and `delete` operators when memory allocation is required.
+   - The address of a constructor cannot be used to refer to other constructors.
+   - A constructor cannot be invoked explicitly as a member function of a class using the dot(.) operator.

You can create the following types of constructors in a class:

+   - Default constructor
+   - Parameterized constructor
+   - A constructor with default arguments
+   - Inline constructor
+   - Copy constructor
+   - Dynamic constructor

Let's now discuss each of these constructors in detail.

# Creating a Default Constructor

In C++, a constructor is the first member of a class that is invoked automatically when an object of the class is created. This means that whenever an object of a class is created, the constructor of the class is invoked. However, what would happen when you do not declare a constructor in a class? In that case, the C++ compiler creates a constructor for your class. This compiler created constructor is called the `default constructor`. A default constructor is a constructor that either has no parameter, or has parameters with default values.