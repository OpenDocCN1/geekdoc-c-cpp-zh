# Pointer Variable Declarations

A variable that can hold pointers to other variables of type Type_Name is declared similar to the way you declare a variable of type Type_Name, except that you place an asterisk at the beginning of the variable name.

# SYNTAX

```
Type_Name *Variable_Name1, *Variable_Name2, ...;
```

# EXAMPLE

```
double *pointer1, *pointer2;
```

# Addresses and Numbers

A pointer is an address, and an address is an integer, but a pointer is not an integer. That is not crazy—that is abstraction! C++ insists that you use a pointer as an address and that you not use it as a number. A pointer is not a value of type int or of any other numeric type. You normally cannot store a pointer in a variable of type int. If you try, most C++ compilers will give you an error message or a warning message. Also, you cannot perform the normal arithmetic operations on pointers. (As you will see later in this chapter, you can perform a kind of addition and a kind of subtraction on pointers, but they are not usual addition and subtraction.)

Pointer variables, like p1 and p2 declared previously, can contain pointers to variables like v1 and v2. You can use the & operator to determine the address of a variable, and you can assign that address to a pointer variable. For example, the following will set the variable p1 equal to a pointer to the variable v1:

```
p1 = &v1;
```

You have two ways to refer to v1: You can call it v1 or you can call it "the variable pointed to by p1." In C++, the way you say "p1" is the same asterisk as when we declared p1, but it has yet another meaning. When the asterisk is used in this way it is called the dereferencing operator, and the pointer variable is said to be dereferenced.

Putting these pieces together can produce some surprising results. Consider the following code:

```
v1 = 0;
p1 = &v1;
*p1 = 42;
cout << v1 << endl;
cout << *p1 << endl;
```