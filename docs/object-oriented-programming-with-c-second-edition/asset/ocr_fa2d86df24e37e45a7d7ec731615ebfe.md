# Object-Oriented Programming with C++

But, we did not provide a cast in the statement that we wrote. Then how did the conversion take place? As mentioned earlier, it is the constructor that is carrying out the conversion for us.

However, if the constructor is declared as an explicit constructor, statements like the one above will not compile. Explicit constructors do not allow implicit conversions like the one that occurred in the above example.

Constructors are declared explicit by prefixing their declarations with the explicit keyword. We will first look at the syntax for declaring an explicit constructor (see Listing 4.9). We will then look at a program that will illustrate the situation under which we can get the error if a constructor has been declared as an explicit constructor.

# Listing 4.9 The explicit constructor

```
/*Beginning of String.h*/
class String
{
    char *cStr;
    long unsigned int len;
public:
    /*no zero-argument constructor*/
    /
    The next statement declares an explicit constructor.
    Note the explicit keyword.
    explicit String(const char * p = NULL);
    const char * getCString();
    /*
    rest of the class String
*/
};
/*End of String.h*/
```

Let us look at Listing 4.10, which illustrates the error we can get when a constructor is declared as an explicit constructor.

# Listing 4.10 Error caused by the explicit StringMain.cpp

```
/*Beginning of StringMain.cpp*/
#include<iostream>
#include"String.h"
void main ()
{
    String s1 = "abc";    //ok: explicit constructor called
    String s2 = "def";    //error: will not compile due to
                         //the explicit constructor
}
/*End of StringMain.cpp*/
```

Note that the error in the program will go away if the statement is written as follows:

String s2 = (String)"def"; //ok

It is obvious that the explicit constructor is preventing an implicit conversion of string into an object of the class String and is forcing the programmer to do explicit conversion.