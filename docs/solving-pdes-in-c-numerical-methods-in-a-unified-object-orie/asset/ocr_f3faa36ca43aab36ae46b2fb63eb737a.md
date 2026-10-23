```
double x;
double y; // not object oriented
};
```

This is called a class block. The symbol "//" indicates the start of a comment line; the words that follow it are intended to describe or explain the code and are ignored by the C++ compiler.

The above block defines a new class called "point", which contains two data fields of type "double". The class can now be used to define variables of type "point". Once a concrete "point" variable 'P' is defined, "P.x" refers to its first field (representing the 'x'-coordinate) and "P.y" refers to its second field (representing the 'y'-coordinate). The reserved word "public:" in the above code indicates that these fields are accessible by every user of the class.

This implementation, however, is not in the spirit of object-oriented programming. Because the data fields 'x' and 'y' are accessible, the "point" object cannot be viewed as a complete "black box" implementation of the point. Because users are not familiar with the internal structure, they could change it inadvertently and spoil the object. Furthermore, if Programmer A, who wrote the "point" class, wanted to change the implementation at some stage, then he/she would have to tell all the users, who would have to change their own codes accordingly. This problem is avoided in the following object-oriented implementation:

```
class point{
    double x;
    double y; // an object-oriented implementation
public:
    double X() const{
        return x;
    } // read x

    double Y() const{
        return y;
    } // read y

    void zero(){
        x=y=0.;
    } // set to zero
};
```

In this version, the data fields 'x' and 'y' are no longer accessible to external users. Because they appear before the reserved word "public", they are considered by default "private": users who define a "point" object 'P' cannot access its coordinates simply by "P.x" or "P.y" as before. The data in the "point" object are thus safe from inadvertent change by careless users. Still, users can read (but not change) the data fields in 'P' only through the public interface functions "X()" and "Y()". For instance, "P.X()" returns the 'x'-coordinate of 'P', and "P.Y()" returns the 'y'-coordinate of 'P'. We refer to 'P' as the current object or variable with which the function "X()" or "Y()" is called. The calls "P.X()" and "P.Y()" are no more expensive than the corresponding calls "P.x" and "P.y" in the previous