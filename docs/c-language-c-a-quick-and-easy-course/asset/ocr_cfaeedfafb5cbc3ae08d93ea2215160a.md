# **Operations with pointers**

We cannot multiply or divide pointer variables. But there is a large number of operations that can be made with them. We have: (a) assigning value zero; (b) increment or decrement; (c) addition or subtraction of integers; (d) equality tests (=), intersection (&&) and union (||); (e) conversion between types of pointers; (f) operations and comparisons with arrays of elements.

# **Types of pointers**

In addition to simple variables pointers, we also have pointers to arrays, structures, pointers, pointers to functions and pointers to pointers.

An array declared as a pointer can work like any other array. That's what happens in this example:

```
```c
main( ) { int i; char *m[]={"o","l","g","a"};
for(i=0;i<4;i++) printf("%n%s\n ",m[i]);}
```
```

Note that the print format is "% s", string, not "% c", character. The significance of this is that the pointer *m points to an array of strings, which is how the compiler deals with the letters ‘o’, ‘l’, ‘g’ and ‘a’. We can therefore declare a pointer array as

```
```c
char *vector[] = {"not", "fear", "this."};
```
```

It is possible to execute, so, the following example:

```
```c
main(){char *ma[]={"Lily","Eve","Mary"};
int i,t=sizeof(ma)/sizeof(char*); for(i=0;i<t;i++)puts(ma[i]);}
```
```

A character pointer, like any other, can allocate dynamic memory in a program. We have the following mini-program:

```
```c
main( )
{char s,*ps; ps=(char*)malloc(2); s='c'; ps=&s; puts(ps);}
```
```

The puts() function is in the library stdio.h e the malloc() function, with its associated calloc(), realloc() and free(), are in stdlib.h. We do not need limit ourselves to what has