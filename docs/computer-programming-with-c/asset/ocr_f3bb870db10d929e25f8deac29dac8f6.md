Orange
Mango
Chikoo
Apple
Sorted order is:
Apple
Chikoo
Mango
Orange

# SCRATCH PAD

Logic to arrange the strings in ascending order is same as that of sorting integer values as discussed in Chapter 6 of this text book. The only difference is that, string is a array of characters and hence we cannot directly compare two string constants using relational operators as we do with integers. Therefore, we have written a user-defined function isGreater() that determines if string p is greater than string q as shown below.

```
```cpp
int isGreater(char p[], char q[])
{
    if(strcmp(p,q)>0)
    {
        return 1;
    }
    else
    {
        return 0;
    }
}
```
```

The function returns 1 if the string constant stored in p is greater than string constant stored in q and the function returns zero otherwise. Note that, we actually check the relationship between two strings using a strcmp() function which is defined in string.h. When the result of strcmp() is positive it indicates that string p is greater than string q and if the result of strcmp() is negative it indicates that the string p is less than string q. Therefore, we return 1 if the result of the function strcmp() is positive as seen in the code.

Now, the requirement of ascending order is that we need to swap two strings a[i] and a[j] in the array, if the string a[i] is greater than string a[j]. Hence, the condition to swap a[i] with a[j] is written as:

```
isGreater(a[i],a[j])
```

# Solved Example 7.6

Write a program to take two numbers as input from the user and to calculate the HCF of two numbers using recursion.

```
```cpp
#include <stdio.h>
int hcf(int, int);
void main()
```
```