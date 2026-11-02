type. When 0 is assigned, it's first converted to a pointer of the appropriate type. The value 0 is the only integer value that can be assigned directly to a pointer variable. Assigning a variable's address to a pointer is discussed in Section 7.3.

> > **Error-Prevention Tip 7.1.**
> > *Initialize pointers to prevent unexpected results.*

# 7.3 Pointer Operators

In this section, we present the address (&) and indirection (*) operators, and the relationship between them.

# *The Address (&) Operator*

The &, or address operator, is a unary operator that returns the *address* of its operand. For example, assuming the definitions

```
int y = 5;
int *yPtr;
```

the statement

```
yPtr = &y;
```

assigns the *address* of the variable y to pointer variable yPtr. Variable yPtr is then said to “point to” y. Figure 7.2 shows a schematic representation of memory after the preceding assignment is executed.

![](bbox=[0.143, 0.546, 0.857, 0.615])

**Fig. 7.2** | Graphical representation of a pointer pointing to an integer variable in memory.

# *Pointer Representation in Memory*

Figure 7.3 shows the representation of the preceding pointer in memory, assuming that integer variable y is stored at location 600000, and pointer variable yPtr is stored at location 500000. The operand of the address operator must be a variable; the address operator *cannot* be applied to constants or expressions.

![](bbox=[0.143, 0.765, 0.857, 0.834])

**Fig. 7.3** | Representation of y and yPtr in memory.

# *The Indirection (*) Operator*

The unary * operator, commonly referred to as the indirection operator or dereferencing operator, returns the *value* of the object to which its operand (i.e., a pointer) points. For example, the statement