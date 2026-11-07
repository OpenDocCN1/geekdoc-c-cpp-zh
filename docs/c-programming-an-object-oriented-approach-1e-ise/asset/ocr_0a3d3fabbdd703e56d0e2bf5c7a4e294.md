```
```cpp
return ...;                         return ...;
}                                   }
```
```

**PR-12.** Which of the following can be a mutator function for the class *Sample*?

```
```cpp
void Sample :: setValue() const        void Sample :: setValue()
{                                       {
    ...;                                    ...;
}                                       }
```
```

**PR-13.** Assume we have the following class definition. Write the definition of the two member functions.

```
```cpp
class Fun
{
    private:
        int x;
    public:
        Fun(int);
        Fun(const Fun&);
};
```
```

**PR-14.** Show how an application can use the parameter constructor and the copy constructor defined in PR-13.

# Programs

**PRG-1.** Create a class named One with two integer data members, *x* and *y*, and two member functions getX and getY. Define the interface file, the implementation file, and an application file that instantiates one object from the class and prints the values of *x* and *y*.

**PRG-2.** Create a class named Two with one integer data member named *a* and one character data member named *a*. Define four member functions getX, getA, setX, and setA. Define the interface file, the implementation file, and an application file that instantiates one object from the class and prints the values of data members. Then set the values of data members through the mutator functions and print their values again.

**PRG-3.** A point in planar Cartesian coordinates is normally defined with two integer values (*x* and *y*). Define a class named Point with two data members. Define a print function that returns the coordinates of a Point object. Define functions to tell the user if a point is on the left side, right side, above, or below another point. Define a function to find the distance between two points as shown below:

```
```text
distance = sqrt ( ( x₂ − x₁)² + ( y₂ − y₁)² )
```
```

**PRG-4.** Code the interface file, the implementation file, and the application file for a class name *Person* with the following members:

+   a. Data members are *name* and *age*.
+   b. Accessor member functions are getName and getAge.