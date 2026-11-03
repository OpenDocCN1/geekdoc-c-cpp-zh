```
```c
struct emp e1 = {"David", 23};
struct emp e2=e1;
strupr(e2.n);
printf("%s\n",e1.n);
```
```

Answer: David

When a structure is assigned, passed, or returned, the copying is done monolithically. This means that the copies of any pointer fields point to the same place as the original.

In other words, anything pointed to is not copied. Hence, on changing the name through e2.n it automatically changed e1.n

Question- Point out the error if any in the following code:

```
```c
main()
{
struct emp
{
char n[20];
int age;
};
struct emp e1 = {"David", 23};
struct emp e2=e1;
if(e1 == e2)
printf("The structures are equal");
}
```
```

Structures cannot be compared using the built in == and != operators. This is because there is no single, good way for a compiler to implement structure comparison. A single byte by byte comparison of the bits present in unused paddings in the structure (such padding is used to keep the alignment of later fields correct). A field by field comparison might require unacceptable amounts of repetitive code for large structures. Also, any compiler generated comparison could not be expected to compare pointer fields with strcmp rather than with ==.

Question- How would you check whether the contents of two structure variables are same or not?

Answer: { struct emp