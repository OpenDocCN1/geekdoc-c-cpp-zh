# 9.6  Accessing Array of Objects using a Pointer

Recall from Chapter 8, Section 8.6, it is possible to access the full array using a pointer holds the starting address of an array. We will rewrite the program given in Section 9.3.1 to arrange Book objects in ascending order of price by using pointer p of type Book, to show accessing of the array of objects using pointers.

The statements,

```
```cpp
struct Book *p;
p=&b[0];
```
```

create a Book type pointer named as p and store the starting address of array b in p. This means following two things, as per our discussion in Chapter 8, Section 8.6

+   1. Every object b[i] in an array can be accessed using a pointer as *(p+i)
+   2. Address of an object b[i] can be obtained by an expression (p+i)

We know from Section 9.5 that, the syntax to access member of an object using a pointer which points to it, is as shown in the following:

```
```cpp
Pointer->Member;
```
```

Note that the left-hand side of the -> operator is a pointer name without a * operator. This means that the left-hand side of an arrow operator must be an address of the object whose member is required to be accessed using the pointer. Therefore, to access the members of object b[i] using a pointer, you will need the address of object b[i], which is (p+i). Hence, the members id, title, author, and price of object b[i] can be accessed by using pointer p as:

```
```cpp
(p+i)->id
(p+i)->title
(p+i)->author
(p+i)->price
```
```

If you need to obtain the address of any of the members, you can get it by applying an & operator to the expression which accesses the member. For example, address of member id of object b[i] by using pointer p can be obtained as:

```
```cpp
&((p+i)->id)
```
```

You can also rewrite the statement by avoiding the outer parenthesis because the priority of -> is anyway greater than the priority of &, but we have added them to make the expression more readable. Technically, this expression can also be written as:

```
```cpp
& (p+i)->id
```
```

The following for loop, inputs the details of n Book objects in array b:

```
```cpp
for(i=0;i<=n-1;i++)
```
```