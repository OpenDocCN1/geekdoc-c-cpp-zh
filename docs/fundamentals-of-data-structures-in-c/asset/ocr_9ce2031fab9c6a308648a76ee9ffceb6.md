```
7.
void main()
{
 int i;
 i = abc();
 printf("%d",i);
}
abc()
{
 _AX = 1000;
}
```

8. The following notations of defining functions are known as?
i. int abc(int a,float b)
{ /* some code
}
ii. int abc(a,b)
int a; float b;
{ /* some code
}

```
9. void main()
{
 char a[100];
 a[0] = 'A';
 a[1] = 'b';
 a[2] = 'c';
 a[3] = 'd';
 func(a);
}
func(char a[])
{
 a++;
 printf("%c",*a);
 a++;
 printf("%c",*a);
}
```

```
10. func(int a, int b)
{
 return(a == b);
}
void main()
{
 int Process(), func();
 printf("The value of process
 is %d",Process(func,3,6));
}
process(int (*pf)(),int val1,int val2)
{
 (*pf) ();
 return((*pf) (val1,val2));
}
```

```
11. int func(int);
void main()
{
 int a = func(sizeof(float));
 printf("Value is %d",+a);
}
int func(int func)
{
 func += 2.5;
 return(func);
}
```

```
12. void pascal func(int, int, int);
void main()
{
 int i = 10;
 func(i++, i++, i++);
 printf("%d %d",i);
}
void pascal func(integer;i,
 integer:j, integer:k)
{
 write(i, j, k);
}
```

```
13. void pascal funl(int i,int j,int k)
{
 printf("%d %d %d",i,j,k);
}
void cdecl fun2(int i,int j,int k)
{
 printf("%d %d %d",i,j,k);
}
void main()
{
 int i = 5;
 fun1(i++, i++, i++);
 printf("%d\n",i);
 i = 5;
 fun2(++i, ++i, ++i);
 printf("%d",i);
}
```

14. Describe the C statement.
void(* abc(int,void(*def)())) () {

```
15. int DIM(int array[])
{
 return sizeof(array)/sizeof(int);
}
void main()
{
 int arr[10];
 printf("The array dimension is
 %d",DIM(arr));
}
```