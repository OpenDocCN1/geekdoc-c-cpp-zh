```
int main()
{
    cout << volume(10) << "\n";
    cout << volume(2.5,8) << "\n";
    cout << volume(100L,75,15) << "\n";
    return 0;
}

// Function definitions

int volume(int s)  // cube
{
    return(s*s*s);
}

double volume(double r, int h)  // cylinder
{
    return(3.14519*r*r*h);
}

long volume(long l, int b, int h) // rectangular box
{
    return(l*b*h);
}
```

PROGRAM 4.3

The output of Program 4.3 would be:

1000
157.26
112500

Overloading of the functions should be done with caution. We should not overload unrelated functions and should reserve function overloading for functions that perform closely related tasks. Sometimes, the default arguments may be used instead of overloading. This may reduce the number of functions to be defined.

Overloaded functions are extensively used for handling class objects. They will be illustrated later when the classes are discussed in the next chapter.

# 4.10 Friend and Virtual Functions

C++ introduces two new types of functions, namely, friend function and virtual function. They are basically introduced to handle some specific tasks related to class objects. Therefore, discussions on these functions have been reserved until after the class objects are discussed. The friend functions are discussed in Sec. 5.15 of the next chapter and virtual functions in Sec. 9.5 of Chapter 9.