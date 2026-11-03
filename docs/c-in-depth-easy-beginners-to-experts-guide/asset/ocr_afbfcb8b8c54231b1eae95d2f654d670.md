This will cause the pointer p1 to point to the next value of its type and the dereference the value.

# Let us use an e.g. to illustrate the point:

```
main()
{
int a[5]={10,20,30,40,50},*p;
p=a        /*address of array can be pointed into the pointer without
the use of & operator*/
printf("%d,",*++p);        /*dereferencing the next address*/
printf("%d",*++p);        /*dereferencing the address and adding 1 to
the element */
}
```

output: 20, 21

3. As well as to subtract one pointer from another.

```
*p1--;
main()
{
int a[5]={10,20,30,40,50},*p;
p=a;
printf("%d,",*++p);        /*dereferencing the next address i.e. index 1*/
printf("%d",*p--);        /*dereferencing the index 1 and then the postfix will
affect*/
printf("%d",*p);        /*dereferencing the pointer*/
}
```

output: 20, 20, 10

4. If p1 and p2 are both pointers to the same array, then p2-p1 gives the number of elements between p1 and p2

```
*p3 = *p2 - *p1;
```