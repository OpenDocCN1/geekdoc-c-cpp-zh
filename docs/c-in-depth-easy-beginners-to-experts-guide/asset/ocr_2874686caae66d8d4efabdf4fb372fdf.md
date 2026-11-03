```
main()
{
    int a = 5;
    int *p;                 /*pointer declaration*/
    p= &a;                  /*copying address of variable a to the pointer p*/
    *p = 10;                /*indirection or use of pointer to change the value of variable a*/
    printf("%d", a);
    printf("%d",*p);
    printf("%d",*(&a));
}
```

Mind Wash Drill - All the printf statements in the above program will give the output as 10. Since the variable p is not an ordinary variable like any other integer variable.

It is A variable which stores the address of some other variable (a in this case). Since p is a variable, the compiler must provide memory to this variable also. Any type of pointer gets two bytes in the memory.

```
int *p1;
float *p2;
char *p3;
All pointers p1, p2, p3 get 2 bytes each.
```

# Memory and pointer -

Suppose if three pointers are declared for int, float, char. All the three pointers will occupy 2 bytes in the memory. This is because all the memory addresses are integer values ranging from 0 to 65536. Thus we can say that a pointer irrespective of its type is storing the addresses as integer values and each integer requires only two bytes.

```
main()
{
    int a = 5,*p1;
    float b=2.5,*p2;
    char c='a',*p3;
    p1= &a;
    p2 = &b;
    p3=&c;
    printf("%d",sizeof(p1));
    printf("%d",sizeof(p2));
```