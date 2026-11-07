
The important things to remember about classes and constructors are the following:

- If a class has no constructor(s), C++ *automatically* provides the default constructor. However, the object declared is still uninitialized.
- On the other hand, suppose a class, say, `dummyClass`, includes constructor(s) with parameter(s) and does not include the default constructor. In this case, C++ *does not* provide the default constructor for the class `dummyClass`. Therefore, when an object of the class `dummyClass` is declared, we must include the appropriate arguments in its declaration.

The following code further explains this. Consider the definition of the following class:

```cpp
class dummyClass
{
public:
    void print() const;

    dummyClass(int dX, int dY);

private:
    int x;
    int y;
};
```

The class `dummyClass` has a constructor with parameters. It *does not* have a default constructor written for it and C++ will not provide one automatically because at least one constructor has been written for it. Given this definition of the class `dummyClass`, the following object declaration is legal:

```cpp
dummyClass myObject(10, 25);  //object declaration is legal
```

However, because the class `dummyClass` does not contain the default constructor, the following class declaration is incorrect and would generate a syntax error:

```cpp
dummyClass dummyObject;  //incorrect object declaration
```

Therefore, to avoid such pitfalls, if a class has constructor(s), the class should also include the default constructor.

## In-Class Initialization of Data Members and the Default Constructor

C++11 standard allows the initialization of data members when they are declared in a class. For example, the definition of the class `clockType` can also be written as follows:

```cpp
class clockType
{
public:
    void setTime(int, int, int);
    void getTime(int&, int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;

    clockType() {}
    clockType(int, int, int);  // constructor with parameters

private:
    int hr = 0;
    int min = 0;
    int sec = 0;
};
```

In this class definition, the data members **hr**, **min**, and **sec** are declared as well as initialized. This is called in-class initialization of the data members. When an object of the class **clockType** is declared without parameters, then the object is initialized using the in-class initialized values. If an object is declared with parameters, then the default values are overridden by the constructor with the parameters. For example, consider the following statements:

```cpp
clockType myTime;
clockType yourTime(3, 40, 18);
```

The **hr**, **min**, and **sec** of **myTime** are each set to 0, while the **hr**, **min**, and **sec** of **yourTime** are set to 3, 40, and 18, respectively.

Note that even though we have initialized the data members of the class **clockType**, we have still included the default constructor. This is required if you want to declare **clockType** objects, such as **myTime**, without passing any values to them. Also let us look at the statement that includes the default constructor in the class definition:

```cpp
clockType() {}
```

This is a complete definition of the default constructor. The `{}` specifies the empty body of the default constructor’s definition. This is an example of in-line function definition of a class member. Because the complete definition is included in the class definition, we do not need to provide its definition in the implementation file. We will discuss in-line member functions of a class later in this chapter.

## Arrays of Class Objects (Variables) and Constructors

If a class has constructors and you declare an array of that class’s objects, the class should have the default constructor. The default constructor is typically used to initialize each (array) class object.

For example, if you declare an array of 100 class objects, then it is impractical (if not impossible) to specify different constructors for each component. (We will further clarify this at the end of this section.)

Suppose that you have 100 employees who are paid on an hourly basis, and you need to keep track of their arrival and departure times. You can declare two arrays—**arrivalTimeEmp** and **departureTimeEmp**—of 100 components each, wherein each component is an object of type **clockType**.

The statement in Line 4 outputs the arrival time of an employee in the form **hr:min:sec**.

To keep track of the departure time of each employee, you can use the array **departureTimeEmp**.

Similarly, you can use arrays to manage a list of names or other objects.

![](img/b217c421655b51e7494cf3b89bb5432d_730_0.png)

Before leaving our discussion of arrays of class objects, we would like to point out the following: The beginning of this section stated that if you declare an array of class objects and the class has constructor(s), then the class should have the default constructor. The compiler uses the default constructor to initialize the array of objects. If the array size is large, then it is impractical to specify a different constructor with parameters for each object. For a small-sized array, we can manage to specify a different constructor with parameters.

For example, the following statement declares `clocks` to be an array of two components. The member variables of the first component are initialized to 8, 35, and 42, respectively. The member variables of the second component are initialized to 6, 52, and 39, respectively.

```cpp
clockType clocks[2] = {clockType(8, 35, 42),
                    clockType(6, 52, 39)};
```

In fact, the expression `clockType(8, 35, 42)` creates an anonymous object of the class `clockType`, initializes its member variables to 8, 35, and 42, respectively; and then uses a member-wise copy to initialize the object `clocks[0]`.

Consider the following statement, which creates the object `myClock` and initializes its member variables to 10, 45, and 38, respectively. This is how we have been creating and initializing objects. In fact, the statement:

```cpp
clockType myClock(10, 45, 38);
```

is equivalent to the statement:

```cpp
clockType myClock = clockType(10, 45, 38);
```

However, the first statement is more efficient. It does not first require that an anonymous object be created and then member-wise copied in order to initialize `myClock`.

The main point that we are stressing here, and that we discussed in the preceding section, is the following: To avoid any pitfalls, if a class has constructor(s), it should also have the default constructor.

## Destructors

Like constructors, destructors are also functions. Moreover, like constructors, a destructor does not have a type. That is, it is neither a value-returning function nor a void function. However, a class can have only one destructor, and the destructor has no parameters. The name of a destructor is the *tilde* character (`~`), followed by the name of the class. For example, the name of the destructor for the class `clockType` is:

```cpp
~clockType();
```

The destructor automatically executes when the class object goes out of scope. The use of destructors is discussed in subsequent chapters.

## Data Abstraction, Classes, and Abstract Data Types

For the car that we drive, most of us want to know how to start the car and drive it. Most people are not concerned with the complexity of how the engine works. By separating the design details of a car’s engine from its use, the manufacturer helps the driver focus on how to drive the car. Our daily life has other similar examples. For the most part, we are concerned only with how to use certain items, rather than with how they work.

Separating the design details (that is, how the car’s engine works) from its use is called **abstraction**. In other words, abstraction focuses on what the engine does and not on how it works. Thus, abstraction is the process of separating the logical properties from the implementation details. Driving the car is a logical property; the construction of the engine constitutes the implementation details. We have an abstract view of what the engine does but are not interested in the engine’s actual implementation.

Abstraction can also be applied to data. Earlier sections of this chapter defined a data type **clockType**. The data type clockType has three member variables and the following basic operations:

- 1. Set the time.
- 2. Return the time.
- 3. Print the time.
- 4. Increment the time by one second.
- 5. Increment the time by one minute.
- 6. Increment the time by one hour.
- 7. Compare two times to see whether they are equal.

The actual implementation of the operations, that is, the definitions of the member functions of the class clockType, was postponed.

Data abstraction is defined as a process of separating the logical properties of the data from its implementation. The definition of clockType and its basic operations are the logical properties; the storing of clockType objects in the computer and the algorithms to perform these operations are the implementation details of clockType.

**Abstract data type (ADT):** A data type that separates the logical properties from the implementation details.

Like any other data type such as int, an ADT has three things associated with it: the name of the ADT, called the type name; the set of values belonging to the ADT, called
