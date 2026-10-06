pointers is the subtraction of two pointers of the same type. The result of subtracting two pointers in Objective-C is the number of elements contained between the two pointers. Thus, if a points to an array of elements of any type and b points to another element somewhere further along in the same array, the expression b - a represents the number of elements between these two pointers. For example, if p points to some element in an array x, the statement

```
n = p - x;
```

assigns to the variable n (assumed here be an integer variable) the index number of the element inside x that p points to. Therefore, if p had been set setting to the 100th element in x by a statement such as

```
p = &x[99];
```

the value of n after the previous subtraction was performed would be 99.

# Pointers to Functions

Of a slightly more advanced nature, but presented here for the sake of completeness, is the notion of a pointer to a function. When working with pointers to functions, the Objective-C compiler needs to know not only that the pointer variable points to a function, but also the type of value returned by that function, well as the number and types of its arguments. To declare a variable, fnPtr, to be of type "pointer to function that returns an int and takes no arguments," you would write this declaration:

```
int (*fnPtr) (void);
```

The parentheses around *fnPtr are required; otherwise, the Objective-C compiler treats the preceding statement as the