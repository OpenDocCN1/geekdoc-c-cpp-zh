```
int sum = integer1 + integer2; // assign total to sum
```

which adds integer1 and integer2, then stores the result in the variable sum.

# ### Calculations in printf Statements

Calculations can also be performed inside printf statements. For example, lines 17–20 can be replaced with the statement

```
printf( "Sum is %d\n", integer1 + integer2 );
```

in which case the variable sum is not needed.

> > **Common Programming Error 2.4**
> > Forgetting to precede a variable in a scanf statement with an ampersand (&) when that variable should, in fact, be preceded by an ampersand results in an execution-time error. On many systems, this causes a "segmentation fault" or "access violation." Such an error occurs when a user's program attempts to access a part of the computer's memory to which it does not have access privileges. The precise cause of this error will be explained in Chapter 7.

> > **Common Programming Error 2.5**
> > Preceding a variable included in a printf statement with an ampersand when, in fact, that variable should not be preceded by an ampersand.

# ## 2.4 Memory Concepts

Variable names such as integer1, integer2 and sum actually correspond to locations in the computer's memory. Every variable has a name, a type and a value.

In the addition program of Fig. 2.5, when the statement (line 12)

```
scanf( "%d", &integer1 ); // read an integer
```

is executed, the value entered by the user is placed into a memory location to which the name integer1 has been assigned. Suppose the user enters the number 45 as the value for integer1. The computer will place 45 into location integer1, as shown in Fig. 2.6. Whenever a value is placed in a memory location, the value replaces the previous value in that location and the previous value is lost; thus, this process is said to be destructive.

![](bbox=[0.16, 0.716, 0.89, 0.812])

Returning to our addition program again, when the statement (line 15)

```
scanf( "%d", &integer2 ); // read an integer
```

executes, suppose the user enters the value 72. This value is placed into the location integer2, and memory appears as in Fig. 2.7. These locations are not necessarily adjacent in memory.