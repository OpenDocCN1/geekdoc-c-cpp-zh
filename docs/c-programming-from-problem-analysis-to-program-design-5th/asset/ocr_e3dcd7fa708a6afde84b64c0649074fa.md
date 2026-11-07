+   - On the other hand, suppose a `class`, say, `dummyClass`, includes constructor(s) with parameter(s) and does not include the default constructor. In this case, C++ *does not* provide the default constructor for the `class` `dummyClass`. Therefore, when an object of the `class` `dummyClass` is declared, we must include the appropriate arguments in its declaration.

The following code further explains this. Consider the definition of the following class:

```
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

The `class` `dummyClass` *does not* have the default constructor. It has a constructor with parameters. Given this definition of the `class` `dummyClass`, the following object declaration is legal:

```
dummyClass myObject(10, 25);  //object declaration is legal
```

However, because the `class` `dummyClass` does not contain the default constructor, the following declaration is incorrect and would generate a syntax error:

```
dummyClass dummyObject;  //incorrect object declaration
```

Therefore, to avoid such pitfalls, if a class has constructor(s), the class should also include the default constructor.

# Arrays of Class Objects (Variables) and Constructors

If a class has constructors and you declare an array of that class’s objects, the class should have the default constructor. The default constructor is typically used to initialize each (array) class object.

For example, if you declare an array of 100 class objects, then it is impractical (if not impossible) to specify different constructors for each component. (We will further clarify this at the end of this section.)

Suppose that you have 100 employees who are paid on an hourly basis, and you need to keep track of their arrival and departure times. You can declare two arrays—`arrivalTimeEmp` and `departureTimeEmp`—of 100 components each, wherein each component is an object of type `clockType`.

Consider the following statement:

```
clockType arrivalTimeEmp[100];                 //Line 1
```

The statement in Line 1 creates the array of objects `arrivalTimeEmp[0]`, `arrivalTimeEmp[1]`, ..., `arrivalTimeEmp[99]`, as shown in Figure 12-8.