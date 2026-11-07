```
```cpp
class Circle
{
    // Data Members
    private:
        double radius;
    // Member functions
    public:
        double getRadius()  const  { return radius; }
    ...
};
```
```

We have included the definition of the *getRadius* function in the class definition, which means that there is no need to include the definition of this function separately.

# ### Explicit Inline Function

A function is defined as an **explicit inline function** by adding the keyword *inline* in front of the function definition. In this case, the definition remained unchanged with the exception of adding the *inline* keyword.

```
```cpp
inline double Circle :: getRadius()    const
{
    return radius;
}
```
```

# ### 7.2.5 Application

The class definition and member function definition must be used. We need an application section—the *main* function, for example—to instantiate objects of the class and apply the member functions on those objects as shown in Program 7.1. We first instantiated one object named *circle1* using the following format (we discuss this format and similar ones later in the chapter).

# ### Object Instantiation

Before using any member function, we must instantiate an object of the class as shown below:

```
```cpp
Circle circle1;
```
```

After this line we have an object named *circle1* that encapsulates one single data member (variable) of type *double* named *radius*, which contains the garbage left over from the previous operation. We must change the value of this variable before using it.

# ### Applying Operation on Objects

After instantiation, we can let the object apply one or more operations defined in the member function definition on itself.

```
```cpp
circle1.setRadius (10.0);
cout << "Radius: " << circle1.getRadius() << endl;
cout << "Area: " << circle1.getArea() << endl;
cout << "Perimeter: " << circle1.getPerimeter() << endl << endl;
```
```