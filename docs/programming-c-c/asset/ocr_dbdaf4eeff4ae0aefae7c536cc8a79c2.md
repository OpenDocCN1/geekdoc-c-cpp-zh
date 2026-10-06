This implies that although a union may contain many members of different types, it cannot handle all the members at the same time. A union is declared using the union keyword.

# Defining a Union

To define a union, you must use the union statement in the same way as you did while defining a structure. The union statement defines a new data type with more than one member for your program.

The format of the union statement is as follows:

```
union[union tag]{
    member definition;
    member definition;
    ...
    member definition;
}[one or more union variables];
```

The union tag is optional and each member definition is a normal variable definition, as int i; or float f; or any other valid definition. At the end of union's definition, before the final semicolon, you can specify one or more union variables but it is optional. Here is the way you would define a union type named Data having three members i, f, and str

```
unionData{
int i;
float f;
char str[20];
data};
```

Now, a variable of Data type can store an integer, a floating-point number, or a string of characters. It means a single variable, i.e., same memory location, can be used to store multiple types of data. You can use any built-in or user-defined data types inside a union based on your requirement.

The memory occupied by a union will be large enough to hold the largest member of the union. For example, in the above example, data type will occupy 20 bytes of memory space because this is the maximum space which can be occupied by a character string. The following example displays the total memory size occupied by the above union.