```
```cpp
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
```

In this class definition, the data members **hr**, **min**, and **sec** are declared as well as initialized. This is called in-class initialization of the data members. When an object of the class **clockType** is declared without parameters, then the object is initialized using the in-class initialized values. If an object is declared with parameters, then the default values are overridden by the constructor with the parameters. For example, consider the following statements:

```
```cpp
clockType myTime;
clockType yourTime(3, 40, 18);
```
```

The **hr**, **min**, and **sec** of **myTime** are each set to 0, while the **hr**, **min**, and **sec** of **yourTime** are set to 3, 40, and 18, respectively.

Note that even though we have initialized the data members of the class **clockType**, we have still included the default constructor. This is required if you want to declare **clockType** objects, such as **myTime**, without passing any values to them. Also let us look at the statement that includes the default constructor in the class definition:

```
```cpp
clockType() {}
```
```

This is a complete definition of the default constructor. The `{}` specifies the empty body of the default constructor’s definition. This is an example of in-line function definition of a class member. Because the complete definition is included in the class definition, we do not need to provide its definition in the implementation file. We will discuss in-line member functions of a class later in this chapter.

# Arrays of Class Objects (Variables) and Constructors

If a class has constructors and you declare an array of that class’s objects, the class should have the default constructor. The default constructor is typically used to initialize each (array) class object.

For example, if you declare an array of 100 class objects, then it is impractical (if not impossible) to specify different constructors for each component. (We will further clarify this at the end of this section.)

Suppose that you have 100 employees who are paid on an hourly basis, and you need to keep track of their arrival and departure times. You can declare two arrays—**arrivalTimeEmp** and **departureTimeEmp**—of 100 components each, wherein each component is an object of type **clockType**.