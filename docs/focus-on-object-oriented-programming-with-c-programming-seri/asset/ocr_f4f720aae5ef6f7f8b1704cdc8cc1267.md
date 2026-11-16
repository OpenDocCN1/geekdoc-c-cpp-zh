# # Overloading the Array Subscript Operator []

The subscript operator [] is normally used to index arrays. In fact, the subscript operator is a binary operator that requires two arguments. For example:

```
```
p = x[i];

[ ] : operator
x : first argument
i : second argument
```
```

The subscript operator actually performs a useful function, it hides pointer arithmetic for us! For example, if we have the following array:

```
```
char name[20];
```
```

and we execute a statement such as:

```
```
ch = name[12];
```
```

The [] operator directs the assignment statement to add 12 to the base address of the array name to locate the data stored in this memory location.

```
```
ch = name[12] implements pointer arithmetic: *(name + 12)
```
```

You can overload the array subscript operator [] to provide array-like access to a class's data members, even though that data might be stored as individual members.

Let's overload the [] operator for a class that stores four integer values as separate data members.