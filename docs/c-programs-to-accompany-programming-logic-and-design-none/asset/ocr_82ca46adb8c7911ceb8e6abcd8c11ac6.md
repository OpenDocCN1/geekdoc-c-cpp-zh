As you can see in Figure 4-2, when parentheses are added, it still takes five steps, but the order of evaluation is changed and the result is also changed.

![](bbox=[0.235, 0.173, 0.795, 0.501])

Figure 4-2  Evaluation of expression using relational and logical operators with parentheses

# COMPARING STRINGS

In C++, you may use the same relational operators when you compare string objects that you use to compare numeric data types such as ints and doubles.

The following code shows how to use the equality operator to compare two string objects and also to compare one string object and one string constant:

```
```cpp
string s1 = "Hello";
string s2 = "World";
// The following test evaluates to false because "Hello" is not the
// same as "World".
if (s1 == s2)
    // code written here executes if true
else
    // code written here executes if false

// The following test evaluates to true because "Hello" is the same
// as "Hello".
if (s1 == "Hello")
    // code written here executes if true
else
    // code written here executes if false
```
```