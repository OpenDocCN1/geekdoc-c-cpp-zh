

```c
{
    int i,arr[5]={25,30,35,40,45},*p;
    p=&arr[4];
    for(i=0;i<5;i++)
        printf("%d\t%d\t",*(p-i),p[-i]);
}
```

```c
(5) main()
{
    int i,arr[5]={25,30,35,40,55},*p;
    for(i=0;i<5;i++)
    {
        printf("%d ",*arr);
        arr++;
    }
}
```

```c
(7) main()
{
    int i,arr[5]={25,30,35,40,45},*p=arr;
    for(i=0;i<5;i++)
    {
        (*p)++;
        printf("%d ",*p);
        p++;
    }
}
```

```c
(8) main()
{
    int i,arr[5]={25,40,55,70,85},*p=arr;

    for(i=0;i<5;i++)
        printf("%d ",*p++);
    printf("\n");

    for(i=0;i<5;i++)
        printf("%d ",*--p);
    printf("\n");
}
```

```c
(9) main()
{
    int i,arr[5]={25,40,55,70,85},*p=arr;
    for(i=0;i<8;i++)
        printf("%d ",*++p);
    printf("\n");
    for(i=0;i<7;i++)
        printf("%d ",(*p)++);
    printf("\n");
}
```

```c
(10) main()
{
    int arr[10]={25,30,35,40,55,60,65,70,85,90},*p;
    for(p=&arr[0];p<arr+10;p++)
        printf("%d ",*p);
}
```

```c
(11) main()
{
    int arr[10]={25,30,35,40,55,60,65,70,85,90},*p;
    for(p=arr+2;p<arr+8;p+=2)
        printf("%d ",*p);
}
```

```c
(12) main()
{
    int i,arr[10]={25,30,35,40,55,60,65,70,85,90};
    int *p=arr+9;
    for(i=0;i<10;i++)
        printf("%d ",*p--);
}
```

```c
(13) main()
{
    int arr[10]={25,30,35,40,55,60,65,70,85,90},*p;
    for(p=arr+9;p>=arr;p--)
        printf("%d ",*p);
}
```

```c
(14) main()
{
    int arr[4]={10,20,30,40};/*Assume base address of arr is 5000*/
    int x=100,*ptr=arr;
    printf("%u %d %d\n",ptr,*ptr,x);
    x=*ptr++;
    printf("%u %d %d\n",ptr,*ptr,x);
    x=*++ptr;
    printf("%u %d %d\n",ptr,*ptr,x);
    x=++*ptr;
    printf("%u %d %d\n",ptr,*ptr,x);
    x=(*ptr)++;
    printf("%u %d %d\n",ptr,*ptr,x);
}
```

```c
(15) main()
{
    int x, arr[8]={11, 22, 33, 44, 55, 66, 77, 88};
    x = (arr+2)[3];
    printf("%d\n", x);
}
```

```c
(16) main()
{
    int arr[8]={11,22,33,44,55,66,77,88};
    int *p,*q;
    q=arr/2;
    p=q*2;
    printf(" %d %d",*p,*q);
}
```

```c
(17) main()
{
    int arr[6]={1,2,3,4,5,6};
    int *p=arr;
    printf("Size of p = %u, Size of arr = %u\n",sizeof(p),sizeof(arr));
}
```

```c
(18) main()
{
    float a=5,*p,**pp;
    p=&a; /*Assume address of a is 5000*/
    pp=&p; /*Assume address of p is 5520*/
    printf("a = %f, p= %u, pp = %u\n",a,p,pp);
    a=a+1;
    p=p+1;
    pp=pp+1;
    printf("a = %f, p= %u, pp = %u\n",a,p,pp);
}
```

```c
(19) int a=5,b=10;
main()
{
    int x=20,*ptr=&x;
    printf("%d ",*ptr);
    change1(ptr);
    printf("%d ",*ptr);
    change2(&ptr);
    printf("%d\n",*ptr);
}
change1(int *p)
{
    p=&a;
}
change2(int **pp)
{
    *pp=&b;
}
```

```c
(20) main()
{
    int a=2,b=6;
    func(a,&b);
    printf("a = %d, b = %d\n",a,b);
}
func(int x,int *y)
{
    int temp;
    temp=x;
    x=*y;
    *y=temp;
}
```

```c
(21) int *ptr;
main()
{
    func();
    printf("%d\n",*ptr);
}
func()
{
    int num=10;
    ptr=&num;
}
```

```c
(22) main()
{
    int a=5,b=8;
    func(a,b);
    printf("a = %d , b = %d\n",a,b);
}
func(int x, int y)
{
    int temp;
    temp=*(&x),*(&x)=*(&y),*(&y)=temp;
}
```

```c
(23) main()
{
    int arr[5]={1,2,3,4,5};    /*Assume base address of arr is 2000*/
    int *p=&arr;
    printf("p = %u,\t",p);
    func1(p);
    printf("p = %u,\t",p);
    func2(&p);
    printf("p = %u\n",p);
}
void func1(int *ptr)
{
    ptr++;
}
void func2(int **pptr)
{
    (*pptr)++;
}
```

```c
(24) main()
{
    int arr[10];
    func(arr);
}
func(int a[10])
{
    int b[10];
    int x=5,y=4;
    a=&x;
    b=&y;
}
```

```c
(25) main()
{
    int arr[3][4]; /*Assume base address of arr is 5000*/
    printf("%u\t",arr);
    printf("%u\t",arr[0]);
    printf("%u\n",&arr[0][0]);
    printf("%d\t",sizeof(arr));
    printf("%d\t",sizeof(arr[0]));
    printf("%d\n",sizeof(arr[0][0]));
}
```

```c
(26) main()
{
    int arr[3][4][5];  /*Assume base address of arr is 2000*/
    printf("%u\t",arr);
    printf("%u\t",arr[0]);
    printf("%u\t",arr[0][0]);
    printf("%u\n",&arr[0][0][0]);
    printf("%d\t",sizeof(arr));
    printf("%d\t",sizeof(arr[0]));
    printf("%d\t",sizeof(arr[0][0]));
    printf("%d\n",sizeof(arr[0][0][0]));
}
```

```c
(27) main()
{
    int arr[10] = {1,2,3,4,5,6,7,8,9,10};
    func(arr+3);
}
func(int a[])
{
    int i;
    for(i=0;a[i]!=8;i++)
        printf("%d ",a[i]);
}
```

```c
(28) main()
{
    int i,j;
    int arr[10]={3,2,4,1,5,9,8,10,7,6};
    for(i=0;i<10;i++)
        for(j=0;j<9-i;j++)
            if(*(arr+j)>*(arr+j+1))
                swap(arr+j,arr+j+1);
    for(i=0;i<10;i++)
        printf("%d\t",arr[i]);
    printf("\n");
}
swap(int *b,int *c)
{
    int temp;
    temp=*b;*b=*c;*c=temp;
}
```

```c
(29) main()
{
    int i,arr[3][4] = {{10,11,12,13},{20,21,22,23},{30,31,32,33}};
    int *pa[3];
    int (*p)[4];
    p=arr;
    for(i=0;i<3;i++)
        pa[i]= arr[i];
    printf("%d %d %d\n",pa[0][0],pa[0][1],pa[2][3]);
    printf("%d %d %d\n",p[0][0],p[0][1],p[2][3]);
}
```

```c
(30) int *func1(void);
int *func2(void);
main()
{
    int *ptr1,*ptr2;
    ptr1=func1();
    ptr2=func2();
    printf("%d %d\n",*ptr1,*ptr2);
}
int *func1(void)
{
    int a=8,*p=&a;
    return p;
}
int *func2(void)
{
    int *p;
    p=(int *)malloc(sizeof(int));
    *p=9;
    return p;
}
```

```c
(31) main()
{
    int i, arr[3][4] = {{10,11,12,13},{20,21,22,23},{30,31,32,33}};
    int *p=arr;
    for(i=0;i<12;i++)
        printf("%d ",p[i]);
    printf("\n");
}
```

# 答案

- **1.** 16 16
- **2.** ptr 未初始化，它包含垃圾值，可能指向内存中的任意位置，使用前应初始化 ptr。
- **3.** 5000 5002 5004 5006 5008  
  Enter 5 numbers : 1 2 3 4 5  
  1 2 3 4 5

  第一个 for 循环打印数组元素的地址，第二个 for 循环向数组中输入数字，第三个 for 循环打印数组元素。
- **4.** 25 25 30 30 35 35 40 40 45 45
- **5.** 45 45 40 40 35 35 30 30 25 25
- **6.** 错误，因为 arr 是常量指针，不能被改变。
- **7.** 26 31 36 41 46  
  通过 (*p)++，我们递增 p 所指向的值；通过 p++，我们递增指针。
- **8.** 25 40 55 70 85  
  85 70 55 40 25
- **9.** 26 27 28 29 30 31 32 33  
  33 34 35 36 37 38 39
- **10.** 25 30 35 40 55 60 65 70 85 90
- **11.** 35 55 65
- **12.** 90 85 70 65 60 55 40 35 30 25
- **13.** 90 85 70 65 60 55 40 35 30 25
- **14.** 5000 10 100  
  5002 20 10  
  5004 30 30  
  5004 31 31  
  5004 32 31
- **15.** (arr+2)[3] 将被解释为 *(arr+2+3) 或 *(arr+5)，这与 arr[5] 相同。
- **16.** 错误，因为指针不支持乘法和除法运算。
- **17.** Size of p = 2, Size of arr = 12
- **18.** a = 5.000000, p= 5000, pp = 5520  
  a = 6.000000, p= 5004, pp = 5522
- **19.** 20 20 10  
  因为我们需要改变 ptr 的值，所以必须传递它的地址；在函数中，我们需要接收指针的地址，因此需要一个指向指针的指针，所以函数 change2( ) 能够改变 ptr 的值，而 change1( ) 不能改变 ptr 的值。
- **20.** a = 2, b=2  
  因为传递的是 b 的地址，所以它的值会改变；而 a 的值不会改变，因为传递的是它的值。
- **21.** 在这个程序中，我们把局部变量 num 的地址赋给了 ptr。当函数 func( ) 终止时，变量 num 失效，它使用的内存可能被用于其他用途。该程序可能输出 10，但内存随时可能被覆盖。
- **22.** a = 5 b = 8  
  我们传递的是变量 a 和 b 的值，因此它们的值不会改变。写 *(&x) 与写 x 相同。
- **23.** p = 2000, p = 2000, p = 2002  
  推理与第 19 题相同。
- **24.** 错误，a = &x 没问题，因为 a 被声明为指针变量；但 b = &y 不可以，因为 b 是数组名，因此是常量指针。
- **25.** 5000 5000 5000  
  24 8 2
- **26.** 2000 2000 2000 2000  
  120 40 10 2
- **27.** 4 5 6 7  
  arr[3] 的地址被传递给函数。在函数内部，a 被声明为指针变量，并用 arr[3] 的地址初始化。
- **28.** 1 2 3 4 5 6 7 8 9 10  
  这些数字通过冒泡排序进行排序
- **29.** 10 11 33  
  10 11 33  
  pa 是一个包含 3 个指针的数组，每个指针的基类型为 int；而 p 是指向包含 4 个整数的数组的指针。
- **30.** -20 9  
  返回局部变量的地址是错误的，但可以返回动态分配内存的地址。
- **31.** 10 11 12 13 20 21 22 23 30 31 32 33

