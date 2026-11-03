That is a is equal to &a[0] is equal to100.

If we declare the pointer p as an integer pointer, then we can make the pointer p to point to the array a –

```
p= a;
    or
    p = &a[0];
```

Now we can access every value of this array a using p++ to move from one element to another. The relationship between p and a is shown below:

+   - p is equals to &a[0];      (=100)
+   - p+1 is equals to &a[1];    (=102)
+   - p+2 is equals to &a[2];    (=104)
+   - p+3 is equals to &a[3];    (=106)
+   - p+4 is equals to &a[4];    (=108)

When handling an array we can either use the array index or pointers to access array elements. Thus we can point to the third element of the array as:

```
a[2] or *(p+2)      (remember the array index starts from 0).
```

# Pointers and Functions-

As discussed earlier the function passing the array as a parameter uses call by reference mechanism.

# WAP (Write a program) to swap two numbers.

| Using call by value:
void swap(int ,int);
main()
{
    int a,b;
    printf("Enter two numbers");
    scanf("%d %d",&a,&b); | Using call by reference:
void swap(int * ,int*);
main()
{
    int a,b;
    printf("Enter two numbers");
    scanf("%d %d",&a,&b); |