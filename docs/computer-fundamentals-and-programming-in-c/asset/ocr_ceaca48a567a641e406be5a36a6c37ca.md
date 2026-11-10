```
```c
{
    struct A a;
    a=read();
    show(a);
    return 0;
}
struct A read(void)
{
    struct A p;
    printf("\n Enter ch, in and f:");
    fflush(stdin);
    scanf("%c %d %f",&p.ch,&p.in,&p.f);
    return p;
}
/*** function show() ***/
void show(struct A b)
{
    printf("\n ch=%c, in=%d, f=%f",b.ch,b.in,b.f);
}
/*** function linkfloat() ***/
void linkfloat()
{
    float a=0.0,*x;
    x=&a;
    a=*x;
}
```
```

# Output

```
```text
Enter ch, in and f: 30 92.55
ch=g, in=30, f=92.550003
```
```

From the preceding examples, it is evident that to modify the value of the members of the structure by a function, the programmer must pass a pointer to that structure to the function. This is just like passing a pointer to an int type argument whose value is to be changed.

If the programmer is only interested in one member of a structure, it is probably simpler to just pass that member to the function. This will make for a simpler function, which is easier to reuse. But, of course, if the value of that member has to be changed, a pointer to it should be passed to the function.

However, when a structure is passed as an argument to a function, each member of the structure is copied. This can prove expensive where structures are large or functions are called frequently. Passing and working with pointers to large structures may be more efficient in such cases.

+   - A pointer to a structure is not itself a structure, but merely a variable that holds the address of a structure.
+   - Passing and working with pointers to large structures may be more efficient while passing structures to a function and working within it.

# 14.3 UNION

A union is a structure, the members of which share the same storage. The amount of storage allocated to a union is sufficient to hold its largest member. At any given time, only one member of the union may actually reside in that storage. The way in which a union’s storage is accessed depends on the member name that is employed during the access. It is the programmer’s responsibility to keep track of which member currently resides in a union.

A union is identified in C through the use of the keyword `union` in place of the keyword `struct`. Virtually, all other methods for declaring and accessing unions are identical to those for structures.

# 14.3.1 Declaring a Union and its Members

The general construct for declaring a union is given as follows.

```
```c
union tag_name
{
    member1;
    member2;
    .
    .
    memberN;
}variable1,variable2,variable3,...,variableX;
```
```

Similar to structure, the union also has a tag name, members, and variable names. In the preceding declaration construct, the variable names, variable1, variable2, variable3,...,variableX, are optional and therefore these may not be mentioned.

The general construct of declaring the individual union variables is

```
```c
union tag_name variable1,variable2,...,variableX;
```
```

As an example, consider the following declarations for a union that has a tag named mixed.

```
```c
union mixed
{
    char letter;
    float radian;
    int number;
};
union mixed all;
```
```