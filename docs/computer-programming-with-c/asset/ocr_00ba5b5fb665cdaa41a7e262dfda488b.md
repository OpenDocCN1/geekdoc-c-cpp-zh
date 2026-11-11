```
```cpp
Person p1;
Student s1;
```
```

The function `inputP()` is invoked using object `p1` and `inputS()` is invoked using object `s1` to accept the member variables of both the objects as input from the user.

The following is the description of each of the `output()` function calls made from `main()`:

| C++ Statement | Description |
|---|---|
| `p1.output();` | As `p1` is of type Person, this statement calls the `output()` function defined inside class Person which prints the id and name of the Person object on the computer screen. |
| `s1.output();` | As `s1` is of type Student, this statement calls the `output()` function defined inside class Student which prints the id, name and marks of the Student object on the computer screen. |

# NOTES

> Although function `output()` is overridden, compiler correctly calls `output()` function of class **Person** when invoked using `p1` and calls `output()` function of class **Student** when invoked using a `s1`. This is because, the compiler determines which function to call based on the **data type of the object** using which the function is actually invoked.

# Are there any rules to be followed while overriding a function?

![](bbox=[0.141, 0.548, 0.183, 0.57])

> So as to override a function, the signature of the function defined in parent class must be exactly same as the signature of the function defined inside the child class.
> 
> The signature of the function includes:
> 
> 1. Name of the function
> 2. Number of arguments the function takes
> 3. Data type of the arguments
> 4. Order of arguments
> 
> If all of the above properties of the function defined in “parent” class exactly match with the function defined in the “child” class then the function is said to be overridden. Note that the return type of the function is not included in the function signature and hence it is possible that the two functions have a different return type in the overriding process.

# 14.10  Pointers and Inheritance

With inheritance implemented in the program, we can create a ‘parent’ type pointer or a ‘child’ type pointer. A pointer of type ‘parent’ can point to a ‘parent’ object as well as to any of the ‘child’ objects. Whereas, the pointer of type ‘child’ can only point to the object of the same child for which it is created.

Let us reuse the classes `Person` and `Student` from the previous section so as to understand the working of ‘pointers’ with inheritance.