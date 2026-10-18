public:
A(A&);
};

is valid. In such cases, the constructor is called the _copy constructor_.

# 6.4 Multiple Constructors in a Class

So far we have used two kinds of constructors. They are:

+   integer( ); // No arguments
+   integer( int ); // Two arguments

In the first case, the constructor itself supplies the data values and no values are passed by the calling program. In the second case, the function call passes the appropriate values from main( ).C++ permits us to use both these constructors in the same class. For example, we could define a class as follows:

```
class integer
{
int m, n;
public:
integer( ){m=0; n=0;} // constructor 1
integer( int a, int b)
{m = a; n = b;} // constructor 2
integer( integer & i)
{m = i.m; n = i.n;} // constructor 3
};
```

This declares three constructors for an integer object. The first constructor receives no arguments, the second receives two integer arguments and the third receives one integer object as an argument. For example, the declaration

```
integer l1;
```