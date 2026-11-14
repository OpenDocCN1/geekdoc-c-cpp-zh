more elaborate (more complex than our `complex`).

# C++11 2.3.1.5 Default Values for Members

Another new feature in C++11 is default values for member variables. Then we only need to set values in the constructor that are different from the defaults:

Click here to view code image

```
class complex
{
public:
    complex(double r, double i) : r(r), i(i) {}
    complex(double r) : r(r) {}
    complex() {}
    ...
private:
    double r = 0.0, i = 0.0;
};
```

Again, the benefit is certainly more pronounced for large classes.

# 2.3.2 Assignment

In Section 2.3.1.2, we have seen that we can copy objects of user classes without getters and setters—at least during construction. Now, we want to copy into existing objects by writing:

```
x= y;
u= v= w= x;
```

To this end, the class must provide an assignment operator (or refrain from stopping the compiler to generate one). As usual, we consider first the class `complex`. Assigning a `complex` value to a `complex` variable requires an operator like

Click here to view code image

```
complex& operator=(const complex& src)
{
    r = src.r; i = src.i;
    return *this;
}
```