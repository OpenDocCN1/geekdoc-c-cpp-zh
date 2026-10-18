This version has a problem when used in an assignment with the same object on both sides of the assignment operator, like the following:

```
myString = my_string;
```

When this assignment is executed, the first statement executed is

```
delete [] value;
```

But the calling object is myString, so this means

```
delete [] myString.value;
```

So, the string value in myString is deleted and the pointer myString.value is undefined. The assignment operator has corrupted the object myString, and this run of the program is probably ruined.

One way to fix this bug is to first check whether there is sufficient room in the dynamic array member of the object on the left-hand side of the assignment operator and to delete the array only if extra space is needed. Our final definition of the overloaded assignment operator does just such a check:

```
```cpp
//This is our final version:
void StringVar::operator = (const StringVar& rightSide)
{
    int newLength = strlen(rightSide.value);
    if (newLength > maxLength)
    {
        delete [] value;
        maxLength = newLength;
        value = new char[maxLength + 1];
    }
    for (int i = 0; i < newLength; i++)
        value[i] = rightSide.value[i];
    value[newLength] = '\0';
}
```
```

For many classes, the obvious definition for overloading the assignment operator does not work correctly when the same object is on both sides of the assignment operator. You should always check this case and be careful to write your definition of the overloaded assignment operator so that it also works in this case.

# SELF-TEST EXERCISE

+   27.
+      a. Explain carefully why no overloaded assignment operator is needed when the only data consists of built-in types.
+      b. Same as part (a) for a copy constructor.
+      c. Same as part (a) for a destructor.