
```cpp
inventory::inventory(string n, int iNum, double cost, int inStock)
{
    name = n;
    itemNum = iNum;
    price = cost;
    unitsInStock = inStock;
}
```

Consider the following declarations:

```cpp
inventory item1;
inventory item2("Dryer");
inventory item3("Washer", 2345, 278.95);
inventory item4("Toaster", 8231, 34.49, 200);
```

For item1, the default constructor in Line 1 executes because no value is passed to this variable. For item2, the constructor in Line 2 executes because only one parameter, which is of type string, is passed, and it matches with the constructor in Line 2. For item3, the constructor in Line 3 executes because three parameters are passed to item3, and they match with the constructor in Line 3. Similarly, for item4, the constructor in Line 4 executes (see Figure 10-7).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_696_0.png)

**FIGURE 10-7** Effect of constructors on objects

> If the values passed to a class object do not match the parameters of any constructor and if no type conversion is possible, a compile-time error will be generated.

- On the other hand, suppose a class, say, `dummyClass`, includes constructor(s) with parameter(s) and does not include the default constructor. In this case, C++ does not provide the default constructor for the class `dummyClass`. Therefore, when an object of the class `dummyClass` is declared, we must include the appropriate arguments in its declaration.

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

The class `dummyClass` does not have the default constructor. It has a constructor with parameters. Given this definition of the class `dummyClass`, the following object declaration is legal:

```cpp
dummyClass myObject(10, 25);  //object declaration is legal
```

However, because the class `dummyClass` does not contain the default constructor, the following declaration is incorrect and would generate a syntax error:

```cpp
dummyClass dummyObject;  //incorrect object declaration
```

Therefore, to avoid such pitfalls, if a class has constructor(s), the class should also include the default constructor.

## Arrays of Class Objects (Variables) and Constructors

If a class has constructors and you declare an array of that class’s objects, the class should have the default constructor. The default constructor is typically used to initialize each (array) class object.

For example, if you declare an array of 100 class objects, then it is impractical (if not impossible) to specify different constructors for each component. (We will further clarify this at the end of this section.)

Suppose that you have 100 employees who are paid on an hourly basis, and you need to keep track of their arrival and departure times. You can declare two arrays—arrivalTimeEmp and departureTimeEmp—of 100 components each, wherein each component is an object of type clockType.

Consider the following statement:

```cpp
clockType arrivalTimeEmp[100];          //line 1
```

The statement in Line 1 creates the array of objects arrivalTimeEmp[0], arrivalTimeEmp[1], ..., arrivalTimeEmp[99], as shown in Figure 10-8.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_699_0.png)

**FIGURE 10-8** Array `arrivalTimeEmp`

You can now use the functions of the class `clockType` to manipulate the time for each employee. For example, the following statement sets the arrival time, that is, hr, min, and sec, of the 50th employee to 8, 5, and 10, respectively (see Figure 10-9).

```cpp
arrivalTimeEmp[49].setTime(8, 5, 10);        //Line 2
```

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_699_1.png)

**FIGURE 10-9** Array `arrivalTimeEmp` after setting the time of employee 49

To output the arrival time of each employee, you can use a loop, such as the following:

```cpp
for (int j = 0; j < 100; j++)                         //Line 3
{
    cout << "Employee # " << (j + 1)
         << " arrival time: ";
    arrivalTimeEmp[j].printTime();                  //Line 4
    cout << endl;
}
```

The statement in Line 4 outputs the arrival time of an employee in the form hr:min:sec.

To keep track of the departure time of each employee, you can use the array departureTimeEmp.

Similarly, you can use arrays to manage a list of names or other objects.

> Before leaving our discussion of arrays of class objects, we would like to point out the following: The beginning of this section stated that if you declare an array of class objects and the class has constructor(s), then the class should have the default constructor. The compiler uses the default constructor to initialize the array of objects. If the array size is large, then it is impractical to specify a different constructor with parameters for each object. For a small-sized array, we can manage to specify a different constructor with parameters.

For example, the following statement declares clocks to be an array of two components. The member variables of the first component are initialized to 8, 35, and 42, respectively. The member variables of the second component are initialized to 6, 52, and 39, respectively.

```cpp
clockType clocks[2] = {clockType(8, 35, 42), clockType(6, 52, 39)};
```

In fact, the expression clockType(8, 35, 42) creates an anonymous object of the class clockType; initializes its member variables to 8, 35, and 42, respectively; and then uses a member-wise copy to initialize the object clocks[0].

Consider the following statement, which creates the object myClock and initializes its member variables to 10, 45, and 38, respectively. This is how we have been creating and initializing objects. In fact, the statement:

```cpp
clockType myClock(10, 45, 38);
```

is equivalent to the statement:

```cpp
clockType myClock = clockType(10, 45, 38);
```

However, the first statement is more efficient. It does not first require that an anonymous object be created and then member-wise copied in order to initialize myClock.

The main point that we are stressing here, and that we discussed in the preceding section, is the following: To avoid any pitfalls, if a class has constructor(s), it should also have the default constructor.

## Destructors

Like constructors, destructors are also functions. Moreover, like constructors, a destructor does not have a type. That is, it is neither a value-returning function nor a void function. However, a class can have only one destructor, and the destructor has no parameters. The name of a destructor is the tilde character (~), followed by the name of the class. For example, the name of the destructor for the class clockType is:

```cpp
~clockType();
```

The destructor automatically executes when the class object goes out of scope. The use of destructors is discussed in subsequent chapters.

## Data Abstraction, Classes, and Abstract Data Types

For the car that we drive, most of us want to know how to start the car and drive it. Most people are not concerned with the complexity of how the engine works. By separating the design details of a car’s engine from its use, the manufacturer helps the driver focus on how to drive the car. Our daily life has other similar examples. For the most part, we are concerned only with how to use certain items, rather than with how they work.

Separating the design details (that is, how the car’s engine works) from its use is called **abstraction**. In other words, abstraction focuses on what the engine does and not on how it works. Thus, abstraction is the process of separating the logical properties from the implementation details. Driving the car is a logical property; the construction of the engine constitutes the implementation details. We have an abstract view of what the engine does but are not interested in the engine’s actual implementation.

Abstraction can also be applied to data. Earlier sections of this chapter defined a data type `clockType`. The data type `clockType` has three member variables and the following basic operations:

1. Set the time.
2. Return the time.
3. Print the time.
4. Increment the time by one second.
5. Increment the time by one minute.
6. Increment the time by one hour.
7. Compare two times to see whether they are equal.

The actual implementation of the operations, that is, the definitions of the member functions of the class `clockType`, was postponed.

Data abstraction is defined as a process of separating the logical properties of the data from its implementation. The definition of `clockType` and its basic operations are the logical properties; the storing of `clockType` objects in the computer and the algorithms to perform these operations are the implementation details of `clockType`.

**Abstract data type (ADT):** A data type that separates the logical properties from the implementation details.
