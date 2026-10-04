# Structures

increment is applied. If you enclose the prefix increment operator and pointer in parentheses, as in the expression ((pt)->hours, the address stored in pt is incremented before the hours member is accessed. Similarly, the expression (pt++)hours uses the postfix increment operator to increment the address in pt after the hours member is accessed. In both cases, however, there must be defined structures to ensure that the incremented pointers actually point to legitimate structures.

As an example, Figure 13.4 illustrates an array of three structures of type Employee. Assuming the address of emp[1] is stored in the pointer variable, the emp++ changes the address to the starting address of emp[2], and the expression --pt changes the address to point to emp[0].

```
pt
&emp[1]> The address in pt currently points to emp[1]

Decrementing the address in pt
causes the pointer to point here
Incrementing the address in pt
causes the pointer
to point here
emp[0].idNum emp[0].payRate emp[0].hours
emp[1].idNum emp[1].payRate emp[1].hours
emp[2].idNum emp[2].payRate emp[2].hours
```

Figure 13.4 Changing pointer addresses

# Returning Structures

In practice, structure-handling functions get direct access to a structure by receiving a structure reference or address. Then any changes to the structure can be made directly from the function. If you want to have a function return a separate structure, however, you must follow the procedures for returning data structures as for returning scalar values. These procedures include declaring the function appropriately and alerting any calling function to the type of structure being returned. For example, the getVals() function in Program 13.6 returns a data structure to main().

The following output is displayed when Program 13.6 runs:

```
The employee id number is 6789
The employee pay rate is $16.25
The employee hours are 38-
```