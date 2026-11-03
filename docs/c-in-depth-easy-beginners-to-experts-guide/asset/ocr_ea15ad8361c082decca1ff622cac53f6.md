# (i) Call by value -

When arguments are passed by value then the copy of the actual parameters is transferred from calling function to the called function definition in formal parameters.

Now any changes made in the formal parameters in called function definition will not be reflected in actual parameters of calling function. Like in the above function to calculate the sum of two numbers the calling statement was written as:

```
ans = sum(a, b);
```

Here the values of variables a, b are passed from the main function to the calling function's definition.

In the definition variables x, y accept the values of a, b respectively. Here, the variables a, b are called the actual arguments while x, y will be called the formal arguments.

The scope of the actual and formal arguments is different so any change made in the formal arguments will not be seen in the actual arguments.

e.g:

```
void swap(int, int);
main()
{
    int a,b;
    printf("Enter 2 numbers");
    scanf("%o%d%o",&a,&b);
    swap(a,b);      /*In this call statement a,b are the actual parameters*/

    printf("%o%d\t%o%d"a,b);
}
void swap(int x,int y)  /*In this function definition x & y are the formal parameters */
{
    int t;
    t=x; x=y; y=t;
```