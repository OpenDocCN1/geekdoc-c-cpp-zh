objects, whose definitions encompass both data and permissible operations on the data; C is not an object-oriented programming language.)

There also is a software aspect—the program needs a way to access the object. This can be accomplished, for instance, by declaring a variable:

```
int entity = 3;
```

This declaration creates an *identifier* called *entity*. An identifier is a name, in this case one that can be used to designate the contents of a particular object. Identifiers satisfy the naming conventions for variables discussed in Chapter 2, “Introducing C.” In this case, the identifier *entity* is how the software (the C program) designates the object that’s stored in hardware memory. This declaration also provides a value to be stored in the object.

A variable name isn’t the only way to designate an object. For instance, consider the following declarations:

```
int * pt = &entity;
int ranks[10];
```

In the first case, *pt* is an identifier. It designates an object that holds an address. Next, the expression *pt is not an identifier because it’s not a name. However, it does designate an object, in this case the same object that *entity* designates. In general, as you may recall from Chapter 3, “Data and C,” an expression that designates an object is called an lvalue. So *entity* is an identifier that is an lvalue, and *pt is an expression that is an lvalue. Along the same lines, the expression *ranks + 2 * entity* is neither an identifier (not a name) nor an lvalue (doesn’t designate the contents of a memory location). But the expression *(ranks + 2 * entity)* is an lvalue because it does designate the value of a particular memory location, the seventh element of the *ranks* array. The declaration of *ranks*, by the way, creates an object capable of holding ten *ints*, and each member of the array also is an object.

If, as with all these examples, you can use the lvalue to change the value in an object, it’s a *modifiable lvalue*. Now consider this declaration:

```
const char * pc = "Behold a string literal!";
```

This causes the program to store the string literal contents in memory, and that array of character values is an object. Each character in the array also is an object, as it can be accessed individually. The declaration also creates an object having the identifier *pc* and holding the address of that string. The identifier *pc* is a modifiable lvalue because it can be reset to point to a different string. The *const* prevents you from altering the contents of a pointed-to string but not from changing which string is pointed to. So *pc, which designates the data object holding the 'B' character, is an lvalue, but not a modifiable lvalue. Similarly, the string literal itself, because it designates the object holding the character string, is an lvalue, but not a modifiable one.

You can describe an object in terms of its *storage duration*, which is how long it stays in memory. You can describe an identifier used to access the object by its *scope* and its *linkage*, which together indicate which parts of a program can use it. The different storage classes offer