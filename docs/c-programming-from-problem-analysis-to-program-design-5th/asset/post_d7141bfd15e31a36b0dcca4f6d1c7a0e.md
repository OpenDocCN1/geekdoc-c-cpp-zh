
```cpp
double rectangleType::perimeter() const
{
    return 2 * (length + width);
}

void rectangleType::print() const
{
    cout << "Length = " << length
         << "; Width = " << width;
}

rectangleType::rectangleType(double l, double w)
{
    setDimension(l, w);
}

rectangleType::rectangleType()
{
    length = 0;
    width = 0;
}
```

Now consider the definition of the following **class boxType**, derived from the **class rectangleType**:

```cpp
class boxType: public rectangleType
{
public:
    void setDimension(double l, double w, double h);
        //Function to set the length, width, and height
        //of the box.
        //Postcondition: length = l; width = w; height = h;

    double getHeight() const;
        //Function to return the height of the box.
        //Postcondition: The value of height is returned.

    double area() const;
        //Function to return the surface area of the box.
        //Postcondition: The surface area of the box is
        //              calculated and returned.

    double volume() const;
        //Function to return the volume of the box.
        //Postcondition: The volume of the box is
        //              calculated and returned.

    void print() const;
        //Function to output the length, width, and height of a box.

    boxType();
        //Default constructor
        //Postcondition: length = 0; width = 0; height = 0;

    boxType(double l, double w, double h);
        //Constructor with parameters
        //Postcondition: length = l; width = w; height = h;

private:
    double height;
};
```

Figure 13-3 shows the UML class diagram of the class `boxType` and the inheritance hierarchy.

![](img/1fbe55537254baeb2b5b7dbaf64956ae_771_0.png)

**FIGURE 13-3** UML class diagram of the class `boxType` and the inheritance hierarchy

From the definition of the class `boxType`, it is clear that the class `boxType` is derived from the class `rectangleType`, and it is a public inheritance. Therefore, all public members of the class `rectangleType` are public members of the class `boxType`. The class `boxType` also overrides (redefines) the functions `print` and `area`.

In general, while writing the definitions of the member functions of a derived class to specify a call to a public member function of the base class, we do the following:

- If the derived class overrides a public member function of the base class, then to specify a call to that public member function of the base class, you use the name of the base class, followed by the scope resolution operator, `::`, followed by the function name with the appropriate parameter list.
- If the derived class does not override a public member function of the base class, you may specify a call to that public member function by using the name of the function and the appropriate parameter list. (See the following note for member functions of the base class that are overloaded in the derived class.)

> **NOTE** If a derived class *overloads* a **public** member function of the base class, then while writing the definition of a member function of the derived class, to specify a call to that (overloaded) member function of the base class, you might need (depending on the compiler) to use the name of the base class, followed by the scope resolution operator, `::`, followed by the function name with the appropriate parameter list. For example, the `class` `boxType` overloads the member function `setDimension` of the `class` `rectangleType`. (See the definition of the function `setDimension` [of the `class` `boxType`], given later in this section.)

Next, let us write the definition of the member function `print` of the `class` `boxType`.

The `class` `boxType` has three member variables: length, width, and height. The member function `print` of the `class` `boxType` prints the values of these member variables. To write the definition of the function `print` of the `class` `boxType`, keep in mind the following:

- The member variables length and width are private members of the `class` `rectangleType`, so they cannot be directly accessed in the `class` `boxType`. Therefore, when writing the definition of the function `print` of the `class` `boxType`, we cannot access length and width directly.
- The member variables length and width of the `class` `rectangleType` are accessible in the `class` `boxType` through the public member functions of the `class` `rectangleType`. Therefore, when writing the definition of the member function `print` of the `class` `boxType`, we first call the member function `print` of the `class` `rectangleType` to print the values of length and width. After printing the values of length and width, we output the values of height.

To call the member function `print` of `rectangleType` in the definition of the member function `print` of `boxType`, we must use the following statement:

```cpp
rectangleType::print();
```

This statement ensures that we call the member function `print` of the base `class` `rectangleType`, not of the `class` `boxType`.

The definition of the member function `print` of the `class` `boxType` is:

```cpp
void boxType::print() const
{
    rectangleType::print();
    cout << "; Height = " << height;
}
```

Let us write the definitions of the remaining member functions of the `class` `boxType`.

The definition of the function `setDimension` is:

```cpp
void boxType::setDimension(double l, double w, double h)
{
    rectangleType::setDimension(l, w);

    if (h >= 0)
        height = h;
    else
        height = 0;
}
```

Notice that in the preceding definition of the function `setDimension`, a call to the member function `setDimension` of the `class` `rectangleType` is preceded by the name of the class and the scope resolution operator, even though the `class` `boxType` overloads—not overrides—the function `setDimension`.

The definition of the function `getHeight` is:

```cpp
double boxType::getHeight() const
{
    return height;
}
```

The member function `area` of the `class` `boxType` determines the surface area of a box. To determine the surface area of a box, we need to access the length and width of the box, which are declared as `private` members of the `class` `rectangleType`. Therefore, we use the member functions `getLength` and `getWidth` of the `class` `rectangleType` to retrieve the length and width, respectively. Because the `class` `boxType` does not contain any member functions that have the names `getLength` or `getWidth`, we call these member functions of the `class` `rectangleType` without using the name of the base class.

```cpp
double boxType::area() const
{
    return  2 * (getLength() * getWidth()
               + getLength() * height
               + getWidth() * height);
}
```

The member function `volume` of the `class` `boxType` determines the volume of a box. To determine the volume of a box, you multiply the length, width, and height of the box or multiply the area of the base of the box by its height. Let us write the definition of the member function volume by using the second alternative. To do this, you can use the member function area of the `class` `rectangleType` to determine the area of the base. Because the `class` `boxType` declares the member function area, to specify a call to the member function area of the `class` `rectangleType`, we use the name of the base class and the scope resolution operator, as shown in the following definition:

```cpp
double boxType::volume() const
{
    return rectangleType::area() * height;
}
```

In the next section, we discuss how to specify a call to the constructor of the base class when writing the definition of a constructor of the derived class.

## Constructors of Derived and Base Classes

A derived class can have its own private member variables, so a derived class can explicitly include its own constructors. A constructor typically serves to initialize the member variables. When we declare a derived class object, this object inherits the members of the base class, but the derived class object cannot directly access the private (data) members of the base class. The same is true for the member functions of a derived class. That is, the member functions of a derived class cannot directly access the private members of the base class.

As a consequence, the constructors of a derived class can (directly) initialize only the (public data) members inherited from the base class of the derived class. Thus, when a derived class object is declared, it must also automatically execute one of the constructors of the base class. Because constructors cannot be called like other functions, the execution of a derived class’s constructor must trigger the execution of one of the base class’s constructors. This is, in fact, what happens. Furthermore, a call to the base class’s constructor is specified in the heading of the definition of a derived class constructor.

In the preceding section, we defined the class rectangleType and derived the class boxType from it. Moreover, we illustrated how to override a member function of the class rectangleType. Let us now discuss how to write the definitions of the constructors of the class boxType.

The class rectangleType has two constructors and two member variables. The class boxType has three member variables: length, width, and height. The member variables length and width are inherited from the class rectangleType.

First, let us write the definition of the default constructor of the class boxType. Recall that, if a class contains the default constructor and no values are specified when the object is declared, the default constructor executes and initializes the object. Because the class rectangleType contains the default constructor, when writing the definition of the default constructor of the class boxType, we do not specify any constructor of the base class.

```cpp
boxType::boxType()
{
    height = 0.0;
}
```

Next, we discuss how to write the definitions of constructors with parameters. To trigger the execution of a constructor (with parameters) of the base class, you specify the name of a constructor of the base class with the parameters in the heading of the definition of the constructor of the derived class.
