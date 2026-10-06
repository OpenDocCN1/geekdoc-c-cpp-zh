# 6.5 Strings

We introduced in Chapter 2 that a string constant is a sequence enclosed in a pair of double quotes. For example, "abcd", "China", and "This is a string" are all string constants. In memory, string constants are stored according to the order of characters in the string, and each character occupies a byte; at the end '\0' is added as the ending tag.
However, in C, a string variable is not a basic data type of C++. Then how does one store and process string variables? C uses character arrays to store strings, and C++ can still use this method. In addition, the standard C++ library defines the string class. We will introduce these two methods in this section.

# 6.5.1 Using Arrays to Store and Process Strings

# 1. Declaration and Reference of Character Arrays

The method of declaring and referencing character arrays is the same as arrays of other types. We can explain this by the following example.

Example 6.22: Output a string.

```
//6_22.cpp
#include<iostream>
using namespace std;
int main()
{
    static char c[10]=
    {'I', ' ', 'a', 'm', ' ', 'a', ' ', 'b', 'o', 'y'};
    //declaration and initialization of one-dimensional character array

    int i;
    for(i=0;i<10;i++) //output elements in the character array one by one

        cout<<c[i];
        cout<<endl;
}
```

The result is:

| I am a boy |

Example 6.23: Output a diamond figure.

```
//6_23.cpp
#include<iostream>
```