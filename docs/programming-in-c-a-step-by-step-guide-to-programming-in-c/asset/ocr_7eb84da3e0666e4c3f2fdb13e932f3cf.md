```
datatype *variablename
```

where datatype represents the type of the data to which the pointer variablename points to. In simple terms, the variablename holds the address of the value of type datatype.

For example,

```
int *ip;
```

This declaration looks like our earlier declarations, with one obvious difference: that is the asterisk. The asterisk means that ip, the variable we're declaring, is not of type int, but rather of type pointer-to-int. (Another way of looking at it is that *ip, which as we'll see is the value pointed to by ip, will be an int.)

We may think of setting a pointer variable to point to another variable as a two-step process: first we generate a pointer to that other variable, and then we assign this new pointer to the pointer variable. We can say (but we have to be careful when we're saying it) that a pointer variable has a value, and that its value is “pointer to that other variable”. This will make more sense when we see how to generate pointer values.

Pointers (that is, pointer values) are generated with the “address-of” operator &, which we can also think of as the “pointer-to” operator. We demonstrate this by declaring (and initializing) an int variable i, and then setting ip to point to it:

```
int i = 5;
```

```
ip = &i;
```

The assignment expression ip = &i; contains both parts of the “two-step process”: &i generates a pointer to i, and the assignment operator assigns the new pointer to (that is, places it “in”) the variable ip. Now ip “points to” i, which we can illustrate with this picture: