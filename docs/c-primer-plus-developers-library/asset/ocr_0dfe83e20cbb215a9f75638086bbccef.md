```
```cpp
s1 = s2 + s1 + s2;
// safe to return reference passed to function
return s1;
}

const string & version3(string & s1, const string & s2)    // bad design
{
    string temp;

    temp = s2 + s1 + s2;
// unsafe to return reference to local variable
    return temp;
}
```
```

Here is a sample run of the program in Listing 8.7:

```
```text
Enter a string: It's not my fault.
Your string as entered: It's not my fault.
Your string enhanced: ***It's not my fault.***
Your original string: It's not my fault.
Your string enhanced: ###It's not my fault.###
Your original string: ###It's not my fault.###
Resetting original string.
```
```

At this point the program crashed.

# Program Notes

Version 1 of the function in Listing 8.7 is the most straightforward of the three:

```
```cpp
string version1(const string & s1, const string & s2)
{
    string temp;

    temp = s2 + s1 + s2;
    return temp;
}
```
```

It takes two string arguments and uses string class addition to create a new string that has the desired properties. Note that the two function arguments are const references. The function would produce the same end result if it just passed string objects:

```
```cpp
string version4(string & s1, string s2)    // would work the same
```
```

In this case, s1 and s2 would be brand-new string objects. Thus, using references is more efficient because the function doesn’t have to create new objects and copy data from the old objects to the new. The use of the const qualifier indicates that this function will use, but not modify, the original strings.

The temp object is a new object, local to the version1() function, and it ceases to exist when the function terminates. Thus, returning temp as a reference won’t work, so the