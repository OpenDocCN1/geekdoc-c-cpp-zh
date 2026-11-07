
- 6. The `private` members of a `class` are not directly accessible outside of the `class`.
- 7. The `public` members of a `class` are directly accessible outside of the `class`.
- 8. By default, all members of a `class` are `private`.
- 9. The `public` members are declared using the member access specifier `public` and the colon, `:`.
- 10. The `private` members are declared using the member access specifier `private` and the colon, `:`.
- 11. A member of a `class` can be a function or a variable.
- 12. If any member of a `class` is a function, you usually use the function prototype to declare it.
- 13. If any member of a `class` is a variable, it is declared like any other variable.
- 14. In the definition of a `class`, you cannot initialize a variable when you declare it.
- 15. A member function of a `class` is called a constant function if its heading contains the reserved word `const` at the end. Moreover, a constant member function of a `class` cannot modify the member variables of the `class`.
- 16. In the Unified Modeling Language (UML) diagram of a `class`, the top box contains the name of the `class`. The middle box contains the member variables and their data types. The last box contains the member function name, parameter list, and the return type of the function. A `+` (plus) sign in front of a member indicates that this member is a `public` member. A `-` (minus) sign preceding a member indicates that this is a `private` member. The symbol `#` before the member name indicates that the member is a `protected` member.
- 17. In C++, a `class` is a definition. No memory is allocated for the `class` itself; memory is allocated for the `class` variables when you declare them.
- 18. In C++, `class` variables are called `class` objects or `class` instances or, simply, objects.
- 19. A `class` member is accessed using the `class` variable name, followed by the dot operator (`.`), followed by the member name.
- 20. The only built-in operations on classes are the assignment and member selection.
- 21. As parameters to functions, classes can be passed either by value or by reference.
- 22. A function can return a value of type `class`. For example, a function can return a value of `clockType`.
- 23. Any program (or software) that uses a `class` is called a client of the `class`.
- 24. A member function of a `class` that modifies the value(s) of the member variable(s) is called a mutator function.
- 25. A member function of a `class` that only accesses (that is, does not modify) the value(s) of the member variable(s) is called an accessor function.
- 26. A constant member function of a `class` can only call the other constant member functions of the `class`.
- 27. Constructors guarantee that the member variables are initialized when an object is declared.
- 28. The name of a constructor is the same as the name of the class.
- 29. A class can have more than one constructor.
- 30. A constructor without parameters is called the default constructor.
- 31. Constructors automatically execute when a class object enters its scope.
- 32. Destructors automatically execute when a class object goes out of scope.
- 33. A class can have only one destructor, and the destructor has no parameters.
- 34. The name of a destructor is the tilde (~), followed by the class name (no spaces in between).
- 35. Constructors and destructors are functions without any type; that is, they are neither value-returning nor void. As a result, they cannot be called like other functions.
- 36. A data type that separates the logical properties from the implementation details is called an abstract data type (ADT).
- 37. Classes were specifically designed in C++ to handle ADTs.
- 38. To implement an ADT, you must represent the data and write related algorithms to implement the operations.
- 39. A precondition is a statement specifying the condition(s) that must be true before the function is called.
- 40. A postcondition is a statement specifying what is true after the function call is completed.
- 41. A public static member, function or variable, of a class can be accessed using the class name and the scope resolution operator, `::`.
- 42. For each static variable of a class, C++ allocates only one memory space. All objects of the class refer to the same memory space.
- 43. `static` member variables of a class exist even when no object of the class type exists.
- 44. Non-static member variables of a class are called the instance variables of the class.

## EXERCISES

The number in parentheses at the end of an exercise refers to the learning objective listed at the beginning of the chapter.

- 1. Mark the following statements as true or false.
  - a. The member variables of a class must be of the same type. (1)
  - b. The member functions of a class must be public. (2)
  - c. A class can have more than one constructor. (5)
  - d. A `class` can have more than one destructor. (5)
  - e. Both constructors and destructors can have parameters. (5)

- 2. Find the syntax errors in the following `class` definition. (1, 2, 5)

```cpp
class mystery                         //Line 1
{                                      //Line 2
public:                                //Line 3
    void print() const;                //Line 4
    void setXY(double, double);        //Line 5
    int add();                         //Line 6
    double mystery();                  //Line 7
private:                               //Line 8
    double x;                          //Line 9
    double y;                          //Line 10
};                                     //Line 11
```

- 3. Find the syntax errors in the following `class` definition. (1, 2, 5)

```cpp
class temp                            //Line 1
{                                      //Line 2
public:                                //Line 3
    bool isEqual();                    //Line 4
    print() const;                     //Line 5
    void temp(int = 0, int = 0);       //Line 6
private:                               //Line 7
    int first;                         //Line 8
    int second;                        //Line 9
};                                     //Line 10
```

- 4. Find the syntax errors in the following `class` definition. (1, 2, 5)

```cpp
class secret                          //Line 1
{                                      //Line 2
public:                                //Line 3
    set (int x, int y);                //Line 4
    get (int& x, int& y);              //Line 5
    int multiply();                    //Line 6
    void print() const;                //Line 7
    secret(int = 0, int = 0) const;    //Line 8
private:                               //Line 9
    int num1;                          //Line 10
    int num2;                          //Line 11
};                                     //Line 12
```

- 5. Find the syntax errors in the following `class` definition. (1, 2, 5)

```cpp
class discover()                      //Line 1
{                                      //Line 2
public:                                //Line 3
    void set(string, int, int);        //Line 4
    void print() const;                //Line 5
    discover();                        //Line 6
    discover(string, int, int);        //Line 7
    bool discover(string, int, int);   //Line 8
private;
    string type;                  //Line 9
    int l;                        //Line 10
    int w;                        //Line 11
                                  //Line 12
}                                 //Line 13
```

- 6. Consider the following declarations: (1, 2, 5, 7)

```cpp
class bagType
{
public:
    void set(string, double, double, double, double);
    void print() const;
    string getStyle() const;
    double getPrice() const;
    void get(double, double, double, double);
    bagType();
    bagType(string, double, double, double, double);
private:
    string style;
    double l;
    double w;
    double h;
    double price;
};
```

```cpp
bagType newBag;  //variable declaration
```

  - a. How many members does `class bagType` have?
  - b. How many **private** members does `class bagType` have?
  - c. How many constructors does `class bagType` have?
  - d. How many constant functions does `class bagType` have?
  - e. Which constructor is used to initialize the object `newBag`?

- 7. Assume the definition of `class bagType` as given in Exercise 6. Answer the following questions: (1, 2, 3, 5, 7)
  - a. Write the definition of the member function `set` so that **private** members are set according to the parameters.
  - b. Write the definition of the member function `print` that prints the values of the data members.
  - c. Write the definition of the default constructor of the `class bagType` so that the **private** member variables are initialized to `"", 0.0, 0.0, 0.0, 0.0`, respectively.
  - d. Write a C++ statement that prints the value of the object `newBag`.
  - e. Write a C++ statement that declares the object `tempBag` of type `bagType`, and initializes the member variables of `tempBag` to `"backPack", 15, 8, 20, and 49.99`, respectively.
