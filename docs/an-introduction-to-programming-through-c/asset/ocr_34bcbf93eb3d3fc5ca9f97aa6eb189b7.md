Now you could call the constructor with either no argument, or upto 3 arguments – parameters corresponding to arguments that have not been given will get the default values, in this case 0. Note that if you include our new constructor in the definition, you cannot include any of the constructors we gave earlier. Say you specified the new bundled constructor and also constructor 2. Then a call V3() would be ambiguous, it would not be clear whether to execute the body of constructor 2, or the body of the new constructor in which all 3 parameters are initialized to their specified defaults.

# 16.1.3 “Default” Constructor

We have said that C++ supplies a constructor, if no constructor is given in the definition of a struct. This constructor takes no arguments, and its body is empty. Such constructor is called a default constructor, however the term is actually used more generally: it has come to mean a constructor that can be called with no arguments, even if such a constructor has been explicitly defined by the programmer. Thus for V3 our constructor 2 is a default constructor. Likewise, the bundled constructor defined above would also be a default constructor.

A default constructor is needed if you wish to define arrays of a structure, because each element of the array will be constructed only using the default constructor.

Note that C++ does not supply a default constructor if you give any constructor whatsoever. So if you define a non-default constructor (i.e. a constructor which must take at least one argument), then the structure would not have a default constructor. Thus you would not be able to create arrays of that structure.

The default constructor is important also when we nest a structure inside another. We discuss this next.

# 16.1.4 Constructors of nested structures

Suppose a structure X has other structures Y,Z,... as members. Then during the call to a constructor for X, the constructors of Y,Z,... are called before the body of the constructor of X is executed. This happens recursively, i.e. if Y in turn has members which are structures.

This rule sounds reasonable, but applying it can sometimes be tricky. Consider the Point and Circle classes as follows.

```
struct Point{
    double x,y;
    Point(double p, double q){x=p; y=q;}
};
struct Circle{
    Point center;
    double radius;
};
```

Consider what happens when we execute

```
Circle c;
```