
```cpp
private:
    int hr;
    int min;
    int sec;
};
```

### EXAMPLE 12-4

```cpp
class clockType
{
private:
    int hr;
    int min;
    int sec;

public:
    void setTime(int, int, int);
    void getTime(int&, int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;
};
```

### EXAMPLE 12-5

```cpp
class clockType
{
    int hr;
    int min;
    int sec;

public:
    void setTime(int, int, int);
    void getTime(int&, int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;
};
```

In Example 12-5, because the identifiers `hr`, `min`, and `sec` do not follow any member access specifier, they are **private**.

It is a common practice to list all of the **public** members first and then the **private** members. This way, you can focus your attention on the **public** members.

## Constructors

In the program in Example 12-2, when we printed the value of `yourClock` without calling the function `setTime`, the output was some strange numbers (see the output of Line 5 in the sample run). This is due to the fact that C++ does not automatically initialize the variables. Because the **private** members of a class cannot be accessed outside of the class (in our case, the member variables), if the user forgets to initialize these variables by calling the function `setTime`, the program will produce erroneous results.

To guarantee that the member variables of a class are initialized, you use constructors. There are two types of constructors: with parameters and without parameters. The constructor without parameters is called the **default constructor**.

Constructors have the following properties:

- The name of a constructor is the same as the name of the class.
- A constructor, even though it is a function, has no type. That is, it is neither a value-returning function nor a `void` function.
- A class can have more than one constructor. However, all constructors of a class have the same name.
- If a class has more than one constructor, the constructors must have different formal parameter lists. That is, either they have a different number of formal parameters or, if the number of formal parameters is the same, then the data type of the formal parameters, in the order you list, must differ in at least one position.
- Constructors execute automatically when a class object enters its scope. Because they have no types, they cannot be called like other functions.
- Which constructor executes depends on the types of values passed to the class object when the class object is declared.

Let us extend the definition of the class `clockType` by including two constructors:

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
    clockType(int, int, int); //constructor with parameters
    clockType();             //default constructor

private:
    int hr;
    int min;
    int sec;
};
```

This definition of the class `clockType` includes two constructors: one with three parameters and one without any parameters. Let us now write the definitions of these constructors:

```cpp
clockType::clockType(int hours, int minutes, int seconds)
{
    if (0 <= hours && hours < 24)
        hr = hours;
    else
        hr = 0;

    if (0 <= minutes && minutes < 60)
        min = minutes;
    else
        min = 0;

    if (0 <= seconds && seconds < 60)
        sec = seconds;
    else
        sec = 0;
}

clockType::clockType()   //default constructor
{
    hr = 0;
    min = 0;
    sec = 0;
}
```

From the definitions of these constructors, it follows that the default constructor sets the three member variables—`hr`, `min`, and `sec`—to 0. Also, the constructor with parameters sets the member variables to whatever values are assigned to the formal parameters. Moreover, we can write the definition of the constructor with parameters by calling the function `setTime`, as follows:

```cpp
clockType::clockType(int hours, int minutes, int seconds)
{
    setTime(hours, minutes, seconds);
}
```

## Invoking a Constructor

Recall that when a class object is declared, a constructor is automatically executed. Because a class might have more than one constructor, including the default constructor, next we discuss how to invoke a specific constructor.

### Invoking the Default Constructor

Suppose that a class contains the default constructor. The syntax to invoke the default constructor is:

```cpp
className classObjectName;
```

For example, the statement:

```cpp
clockType yourClock;
```

declares yourClock to be an object of type clockType. In this case, the default constructor executes, and the member variables of yourClock are initialized to 0.

**NOTE:** If you declare an object and want the default constructor to be executed, the empty parentheses after the object name are not required in the object declaration statement. In fact, if you accidentally include the empty parentheses, the compiler generates a syntax error message. For example, the following statement to declare the object yourClock is illegal:

```cpp
clockType yourClock();  //illegal object declaration
```

### Invoking a Constructor with Parameters

Suppose a class contains constructors with parameters. The syntax to invoke a constructor with a parameter is:

```cpp
className classObjectName(argument1, argument2, ...);
```

in which argument1, argument2, and so on are either a variable or an expression.

Note the following:

- The number of arguments and their type should match the formal parameters (in the order given) of one of the constructors.
- If the type of the arguments does not match the formal parameters of any constructor (in the order given), C++ uses type conversion and looks for the best match. For example, an integer value might be converted to a floating-point value with a zero decimal part. Any ambiguity will result in a compile-time error.

Consider the statement:

```cpp
clockType myClock(5, 12, 40);
```

This statement declares an object myClock of type clockType. Here, we are passing three values of type `int`, which matches the type of the formal parameters of the constructor with a parameter. Therefore, the constructor with parameters of the class `clockType` executes, and the three member variables of the object myClock are set to 5, 12, and 40.

Example 12-6 further illustrates how constructors are executed.

### EXAMPLE 12-6

Consider the following class definition:

```cpp
class inventory
{
public:
    inventory();                         //Line 1
    inventory(string);                   //Line 2
    inventory(string, int, double);      //Line 3
    inventory(string, int, double, int); //Line 4

    //Add additional functions

private:
    string name;
    int itemNum;
    double price;
    int unitsInStock;
};
```

This class has four constructors and four member variables. Suppose that the definitions of the constructors are as follows:

```cpp
inventory::inventory() //default constructor
{
    name = "";
    itemNum = -1;
    price = 0.0;
    unitsInStock = 0;
}
```

```cpp
inventory::inventory(string n)
{
    name = n;
    itemNum = -1;
    price = 0.0;
    unitsInStock = 0;
}
```

```cpp
inventory::inventory(string n, int iNum, double cost)
{
    name = n;
    itemNum = iNum;
    price = cost;
    unitsInStock = 0;
}
```

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
inventory item2("Dyer");
inventory item3("Washer", 2345, 278.95);
inventory item4("Toaster", 8231, 34.49, 200);
```

For item1, the default constructor in Line 1 executes because no value is passed to this variable. For item2, the constructor in Line 2 executes because only one parameter, which is of type string, is passed, and it matches with the constructor in Line 2. For item3, the constructor in Line 3 executes because three parameters are passed to item3, and they match with the constructor in Line 3. Similarly, for item4, the constructor in Line 4 executes (see Figure 12-7).

![](img/1fbe55537254baeb2b5b7dbaf64956ae_713_0.png)

**FIGURE 12-7** Effect of constructors on objects

**NOTE:** If the values passed to a class object do not match the parameters of any constructor and if no type conversion is possible, a compile-time error will be generated.
