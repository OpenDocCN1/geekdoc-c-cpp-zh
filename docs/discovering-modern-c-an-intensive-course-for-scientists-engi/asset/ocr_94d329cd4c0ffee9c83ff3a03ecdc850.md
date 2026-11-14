We will focus more on the default constructor in the next section.
The three different constructors above can be combined into a single one by using default arguments:

```
class complex ,
{
    public:
    complex(double r = 0, double i = 0) : r(r), i(i) {}
    // ...
};
```

This constructor now allows various forms of initialization:

```
complex z1,       // default-constructed
        z2(),     // default-constructed ???????
        z3(4),    // short for z3(4.0, 0.0)
        z4= 4,    // short for z4(4.0, 0.0)
        z5(0, 1);
```

The definition of z2 is a mean trap. It looks absolutely like a call for the default constructor but it is not. Instead it is interpreted as the declaration of the function named z2 that takes no argument and returns a complex. Scott Meyers called this interpretation the Most Vexing Phrase. Construction with a single argument can be written with an assignment-like notation using = as for z4. In old books you might read sometimes that this causes an overhead because a temporary is first built and then copied. This is not true; it might have been in the very early days of C++ but today no compiler will do that.

C++ knows three special constructors:

+   - The before-mentioned default constructor,
+   - The Copy Constructor, and
+   - The Move Constructor (in C++11 and higher; §2.3.5.1).

In the following sections, we will look more closely at them.

# 2.3.1.1 Default Constructor

A Default Constructor is nothing more than a constructor without arguments or one that has default values for every argument. It is not mandatory that a class contains a default constructor.

At first glance, many classes do not need a default constructor. However, in real life it is much easier having one. For the complex class, it seems that we could live without a default