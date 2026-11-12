
- Write the first character of s
- Write the rest of s

These steps simply write the string s. Naming the function writeBackward does not guarantee that it will actually write the string backward—recursion really is not magic!

You can write s backward correctly by using the following recursive formulation:

- Write s minus its first character backward
- Write the first character of s

In other words, you write the first character of s only after you have written the rest of s backward.

This approach leads to the following pseudocode solution:

```
writeBackward2(s: string)
if (the string s is empty)
    Do nothing—this is the base case
else
    writeBackward2(s minus its first character)
    Write the first character of s
}
```

The translation of writeBackward2 into C++ is similar to that of the original writeBackward function and is left as an exercise.

It is instructive to carefully trace the actions of the two pseudocode functions writeBackward and writeBackward2. First, add statements to each function to provide output that is useful to the trace, as follows:

```
writeBackward(s: string)
cout << "Enter writeBackward with string: " << s << endl;
if (the string is empty)
    Do nothing—this is the base case
else
    cout << "About to write last character of string: "
    << s << endl;
    Write the last character of s
    writeBackward(s minus its last character) // Point A
}
cout << "Leave writeBackward with string: " << s << endl;
```

cout statements can help you trace the logic of a recursive function

```
writeBackward2(s: string)
cout << "Enter writeBackward2 with string: "
<< s << endl;
if (the string is empty)
    Do nothing—this is the base case
else
    writeBackward2(s minus its first character) // Point A
    cout << "About to write first character of string: "
    << s << endl;
    Write the first character of s
}
cout << "Leave writeBackward2 with string: " << s << endl;
```

Figures 2-8 and 2-9 show the output of the revised pseudocode functions writeBackward and writeBackward2, when initially given the string "cat".

## FIGURE 2-8 Box trace of writeBackward("cat") in pseudocode

The initial call is made, and the function begins execution:

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_88_0.png)

Output stream:

```
Enter writeBackward with string: cat
About to write last character of string: cat
t
```

Point A is reached, and the recursive call is made. The new invocation begins execution:

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_88_1.png)

Output stream:

```
Enter writeBackward with string: cat
About to write last character of string: cat
t
Enter writeBackward with string: ca
About to write last character of string: ca
a
```

Point A is reached, and the recursive call is made. The new invocation begins execution:

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_88_2.png)

Output stream:

```
Enter writeBackward with string: cat
About to write last character of string: cat
t
Enter writeBackward with string: ca
About to write last character of string: ca
a
Enter writeBackward with string: c
About to write last character of string: c
c
```

Point A is reached, and the recursive call is made. The new invocation begins execution:

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_88_3.png)

This invocation completes execution, and a return is made.

Output stream:

```
Enter writeBackward with string: cat
About to write last character of string: cat
t
Enter writeBackward with string: ca
About to write last character of string: ca
a
Enter writeBackward with string: c
About to write last character of string: c
c
Enter writeBackward with string:
Leave writeBackward with string:
```

This invocation completes execution, and a return is made.

Output stream:

```
Enter writeBackward with string: cat
About to write last character of string: cat
t
Enter writeBackward with string: ca
About to write last character of string: ca
a
Enter writeBackward with string: c
About to write last character of string: c
c
Enter writeBackward with string:
Leave writeBackward with string: c
```

This invocation completes execution, and a return is made.

Output stream:

```
Enter writeBackward with string: cat
About to write last character of string: cat
t
Enter writeBackward with string: ca
About to write last character of string: ca
a
Enter writeBackward with string: c
About to write last character of string: c
c
```

## FIGURE 2-8 Box trace of writeBackward("cat") in pseudocode (continued)

```
c
Enter writeBackward with string:
Leave writeBackward with string:
Leave writeBackward with string: c
Leave writeBackward with string: ca
```

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_90_0.png)

This invocation completes execution, and a return is made.

### Output stream:

```
Enter writeBackward with string: cat
About to write last character of string: cat
t
Enter writeBackward with string: ca
About to write last character of string: ca
a
Enter writeBackward with string: c
About to write last character of string: c
c
Enter writeBackward with string:
Leave writeBackward with string:
Leave writeBackward with string: c
Leave writeBackward with string: ca
Leave writeBackward with string: cat
```

You need to be comfortable with the differences between these two functions. The recursive calls that the two functions make generate a different sequence of values for the argument s. Despite this fact, both functions correctly write the string argument backward. They compensate for the difference in the sequence of values for s by writing different characters in the string at different times relative to the recursive calls. In terms of the box traces in Figures 2-8 and 2-9, writeBackward writes a character just before generating a new box (just before a new recursive call), whereas writeBackward2 writes a character just after crossing off a box (just after returning from a recursive call). When these differences are put together, the result is two functions that employ different strategies to accomplish the same task.

This example also illustrates the value of the box trace, combined with well-placed cout statements, in debugging recursive functions. The cout statements at the beginning, interior, and end of the recursive functions report the value of the argument s. In general, when debugging a recursive function, you should also report both the values of local variables and the point in the function where each recursive call occurred, as in this example:

```
abc(...);
cout << "Calling function abc from point A.\n";
abc(...); // This is point A
cout << "Calling function abc from point B.\n";
abc(...); // This is point B
```

Realize that the cout statements do not belong in the final version of the function.

- Well-placed but temporary cout statements can help you debug a recursive function
- Remove cout statements after you have debugged the function

## FIGURE 2-9 Box trace of writeBackward2("cat") in pseudocode

The initial call is made, and the function begins execution:

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_91_0.png)

Output stream:

```
Enter writeBackward2 with string: cat
```

Point A is reached, and the recursive call is made. The new invocation begins execution:

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_91_1.png)

Output stream:

```
Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at
```

Point A is reached, and the recursive call is made. The new invocation begins execution:

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_91_2.png)

Output stream:

```
Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at
Enter writeBackward2 with string: t
```

Point A is reached, and the recursive call is made. The new invocation begins execution:

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_91_3.png)

This invocation completes execution, and a return is made.

Output stream:

```
Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at
Enter writeBackward2 with string: t
Enter writeBackward2 with string:
Leave writeBackward2 with string:
```

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_91_4.png)

This invocation completes execution, and a return is made.

Output stream:

```
Enter writeBackward2 with string: cat
Enter writeBackward2 with string: at
Enter writeBackward2 with string: t
