much in common and are introduced here together.

# 2.3.1 Constructors

Constructors are methods that initialize objects of classes and create a working environment for other member functions. Sometimes such an environment includes resources like files, memory, or locks that have to be freed after their use. We come back to this later.

Our first constructor will set the real and imaginary values of our

complex:

![](bbox=[0.145, 0.315, 0.38, 0.328])

```
class complex
{
public:
    complex(double rnew , double inew)
    {
        r = rnew; i = inew;
    }
// ...
};
```

A constructor is a member function with the same name as the class itself. It has no return type and can possess an arbitrary number of parameters. The constructor above allows us to set the values of c1 directly in the definition:

![](bbox=[0.145, 0.585, 0.38, 0.598])

```
complex c1(2.0, 3.0); // Traditional constructor
```

To verify that we don’t lose accuracy here, we can use uniform initialization:

```
[ C++11 ] complex c1(2.0, 3.0); // Modern style
```

There is a special syntax for setting member variables and constants in constructors called Member Initialization List or for short Initialization List:

![](bbox=[0.145, 0.795, 0.38, 0.808])

```
class complex
{
public:
    complex(double rnew , double inew)
    : r(rnew), // Old-fashioned
```