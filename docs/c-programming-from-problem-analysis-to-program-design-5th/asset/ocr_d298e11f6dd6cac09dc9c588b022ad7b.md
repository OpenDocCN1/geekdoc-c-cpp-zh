In the preceding program, after the statement:

```
int & y = a.addressOfX();
```

executes, **y** becomes an alias of the *private* member variable x of the object a. Thus, the statement:

```
y = 25;
```

changes the value of x.

Chapter 12 said that *private* member variables are not accessible outside of the class. However, by returning their addresses, the programmer can manipulate them. One way to resolve this problem is to never provide the user of the class with the addresses of the *private* member variables. Sometimes, however, it is necessary to return the address of a *private* member variable, as we will see in the next chapter. How can we prevent the program from directly manipulating the *private* member variables? To fix this problem, we use the word **const** before the return type of the function. This way, we can still return the addresses of the *private* member variables, but at the same time prevent the programmer from directly manipulating the *private* member variables. Let us rewrite the class testAddress using this feature.

```
#ifndef H_testAdd
#define H_testAdd

class testAddress
{
public:
    void setX(int);
    void printX() const;
    const & addressOfX(); //this function returns the
                          //address of the private data
                          //member

private:
    int x;
};

#endif
```

The definition of the function addressOfX in the implementation file is:

```
const int& testAddress::addressOfX()
{
    return x;
}
```

The same program will now generate a compile-time error.

# QUICK REVIEW

+   1. Pointer variables contain the addresses of other variables as their values.
+   2. In C++, no name is associated with the pointer data type.