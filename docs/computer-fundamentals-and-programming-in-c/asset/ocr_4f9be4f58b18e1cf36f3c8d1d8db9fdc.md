11. Given the following array declaration and function prototype, choose all the correct ways of calling the function from main() and giving it a reference to myArray[].

```
```c
void myFun(int a[]);
int main()
{
    int myArray[] =
    {10,20,30,40,50,60,70,80};
    /* function call here */
}
```
```

+   - (a) myFun(myArray);
+   - (b) myFun(myArray[]);
+   - (c) myFun(&myArray[0]);
+   - (d) myFun(myArray[0]);
+   - (e) myFun(myArray[8]);

12. What will be the output of the following program?

```
```c
#define swap(a,b) temp=a; a=b; b=temp;
int main()
{
    static int a=5,b=6,temp;
    if(a > b)
        swap(a,b);
    printf("%d %d",a,b);
    return 0;
}
```
```

+   - (a) a=5 b=6
+   - (b) a=6 b=5
+   - (c) a=6 b=0
+   - (d) None of these

13. The following code is not well written. What is the output?

```
```c
int main()
{
    int a=1,b=2;
    printf("%d",add(a,b));
    return 0;
}
int add(int a,int b)
{
    return(a+b);
}
```
```

+   - (a) Run-time error
+   - (b) Compile-time error
+   - (c) 3
+   - (d) None of these

14. What will be the output of the following program?

```
```c
int add(int a,int b)
{
    int c=a+b;
}
int main()
{
    int a=10,b=20;
    printf("%d %d %d",a,b,add(a,b));
    return 0;
}
```
```

+   - (a) 10 20 0
+   - (b) Compile-time error
+   - (c) 10 20 30
+   - (d) None of these

15. What will be the output of the following program?

```
```c
int add(int a,int b)
{
    int c=a+b;
    return;
}
int main()
{
    int a=10,b=20;
    printf("%d %d %d",a,b,add(a,b));
    return 0;
}
```
```

+   - (a) 10 20 0
+   - (b) Compile-time error

+   - (c) 10 20 30
+   - (d) None of these

16. What will be the output of the following program?

```
```c
int main()
{
    int add(int,int);
    int a=7,b=13;
    printf("%d",add(add(a,b),
    add(a,b)));
    return 0;
}
int add(a,b)
int a,b;
{
    return(a+b);
}
```
```

+   - (a) Compile-time error
+   - (b) 20
+   - (c) 40
+   - (d) None of these

17. What will be the output of the following program?

```
```c
int add(a,b)
{
    int c=a+b;
    return c;
}
int main()
{
    int a=10,b=20;
    printf("%d",add(a,b));
    return 0;
}
```
```

+   - (a) 30
+   - (b) Compile-time error
+   - (c) 0
+   - (d) None of these

18. What will be the output of the following program?

```
```c
int func2(int b)
{
    if(b == 0)
        return b;
    else
        func1(b--);
}
int func1(int a)
{
    if(a == 0)
        return a;
    else
        func2(a--);
}
int main()
{
    int a=7;
    printf("%d",func1(a));
    return 0;
}
```
```

+   - (a) 0
+   - (b) Compile-time error
+   - (c) Infinite loop
+   - (d) 7

19. What will be the output of the following program?

```
```c
int func1(int a)
{{(;)};{return a;}}
int main()
{
    int a=7;
    printf("%d",func1(a));
    return 0;
}
```
```

+   - (a) 0
+   - (b) Compile-time error