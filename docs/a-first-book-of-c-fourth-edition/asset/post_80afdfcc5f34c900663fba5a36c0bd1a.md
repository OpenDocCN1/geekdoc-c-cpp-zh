
The definition of a union has the same form as a structure definition, with the keyword union used in place of the keyword struct. For example, the following declaration creates a union variable named val:

```
union
{
    char key;
    int num;
    double price;
} val;
```

If val were a structure, it would consist of three members. As a union, however, val contains a single member that can be a character variable named key, an integer variable named num, or a double-precision variable named price. In effect, a union reserves enough memory locations to accommodate its largest member's data type. This same set of locations is then referenced by different variable names, depending on the data type of the value currently stored in the reserved locations. Each value stored overwrites the previous value, using as many bytes of the reserved memory area as necessary.

Union members are referenced by using the same notation as structure members. For example, if the val union is currently being used to store a character, the correct variable name to access the stored character is val.key. Similarly, if the union is used to store an integer, the value is accessed by the name val.num, and a double-precision value is accessed by the name val.price. In using union members, it's the programmer's responsibility to make sure the correct member name is used for the data type currently stored in the union.

Typically, a second variable is used to keep track of the current data type stored in the union. For example, the following code could be used to select the appropriate member of val for display. The value in the uType variable determines the currently stored data type in the val union:

```
switch(uType)
{
    case 'c': cout << val.key;
        break;
    case 'i': cout << val.num;
        break;
    case 'd': cout << val.price;
        break;
    default : cout << "Invalid type in uType : " << uType;
}
```

As in structures, a data type can be associated with a union. For example, the declaration

```
union DateTime
{
    int days;
    double time;
};
```

provides a union data type without actually reserving any storage locations. This data type can then be used to define any number of variables. For example, the definition

```
DateTime first, second, *pt;
```

creates a union variable named first, a union variable named second, and a pointer that can be used to store the address of any union having the form DateTime. After a pointer to a union has been declared, the same notation for accessing structure members can be used to access union members. For example, if the assignment pt = &first; is made, pt->date references the date member of the union named first.

Unions can be members of structures or arrays, and structures, arrays, and pointers can be members of unions. In each case, the notation used to access a member must be consistent with the nesting used. For example, in the structure defined by

```
struct
{
    char uType;
    union
    {
        char *text;
        float rate;
    } uTax;
} flag;
```

the variable rate is referenced as

```
flag.uTax.rate
```

Similarly, the first character of the string whose address is stored in the pointer text is referenced as follows:

```
*flag.uTax.text
```

## EXERCISES 16.5

- 1. (Practice) Assume the following definition has been made:

```
union
{
    double rate;
    double taxes;
    int num;
} flag;
```

For this union, write cout statements to display the members of the union.

- 2. **(Practice)** Define a union variable named `car` containing an integer named `year`, an array of 10 characters named `name`, and an array of 10 characters named `model`.
- 3. **(Practice)** Define a union variable named `factors` that allows referencing a double-precision number by the variable names `watts` and `power`.
- 4. **(Practice)** Define a union data type named `Amt` containing an integer variable named `intAmt`, a double-precision variable named `dblAmt`, and a pointer to a character variable named `ptKey`.
- 5. **(Desk check)** a. What do you think the following section of code will display?

```cpp
union
{
    char ch;
    double btype;
} alt;
alt.ch = 'y';
cout << alt.btype;
```

b. Include the code in Exercise 5a in a program, and run the program to verify your answer to Exercise 5a.

## 16.6 Common Programming Errors

Three common errors are often made when using structures or unions:

- 1. Structures and unions, as complete entities, can't be used in relational expressions. For example, even if `TeleType` and `PhoneType` are two structures of the same type, the expression `TeleType == PhoneType` is invalid. Members of a structure or union can, of course, be compared if they're of the same data type, using any of C++'s relational operators.
- 2. When a pointer is used to “point to” a structure or a union or is a member of a structure or a union, take care to use the address in the pointer to access the correct data type. If you're confused about exactly what's being pointed to, remember: “If in doubt, print it out.”
- 3. Because a union can store only one of its members at a time, you must be careful to keep track of the currently stored variable. Storing one data type in a union and accessing it by the wrong variable name can result in an error that's particularly troublesome to locate.

## 16.7 Chapter Summary

- 1. A structure allows grouping variables under a common variable name. Each variable in a structure is accessed by its structure variable name, followed by a period and then its variable name. Another term for a data structure is a record. One form for declaring a structure variable is as follows:
```
struct
{
    // member declarations in here
} structureName;
```

- 2. A named data type can be created from a structure by using this declaration form:
```
struct DataType
{
    // member declarations in here
};
```
Structure variables can then be defined as this DataType. By convention, the first letter of the DataType name is always capitalized.

- 3. Structures are particularly useful as elements of arrays. Used in this manner, each structure becomes one record in a list of records.

- 4. Complete structures can be used as function arguments, in which case the called function receives a copy of each element in the structure. A structure's address can also be passed as a reference or a pointer, which gives the called function direct access to the structure.

- 5. Structure members can be any valid C++ data type, including other structures, unions, arrays, and pointers. When a pointer is included as a structure member, a linked list can be created. This list uses the pointer in one structure to "point to" (contain the address of) the next logical structure in the list.

- 6. Unions are declared in the same manner as structures. The definition of a union creates a memory overlay area, with each union member using the same memory storage locations. Therefore, only one member of a union can be active at a time.

## Table A.1 Summary of C++ Operators (continued)

| Operator | Description | Associativity |
|---|---|---|
| ++ | Increment | Right to left |
| -- | Decrement |  |
| - | Unary minus |  |
| ! | Logical negation |  |
| ~ | One's complement |  |
| (type) | Type conversion (cast) |  |
| sizeof | Storage size |  |
| & | Address of |  |
| * | Indirection |  |
| * | Multiplication | Left to right |
| / | Division |  |
| % | Modulus (remainder) |  |
| + | Addition | Left to right |
| - | Subtraction |  |
| << | Left shift | Left to right |
| >> | Right shift |  |
| < | Less than | Left to right |
| <= | Less than or equal to |  |
| > | Greater than |  |
| >= | Greater than or equal to |  |
| == | Equal to | Left to right |
| != | Not equal to |  |
| & | Bitwise AND | Left to right |
| ^ | Bitwise exclusive OR | Left to right |
| | | Bitwise inclusive OR | Left to right |
| && | Logical AND | Left to right |
| || | Logical OR | Left to right |
| ?: | Conditional expression | Right to left |
| = | Assignment | Right to left |
| += -= *= | Assignment |  |
| /= %= &= | Assignment |  |
| ^= |= | Assignment |  |
| <<= >>= | Assignment |  |
| , | Comma | Left to right |
