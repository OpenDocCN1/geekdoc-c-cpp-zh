
任何递归函数的执行都可能无限持续，因此为了使执行结束，需要应用终止条件。

使用递归函数是为了解决这样的问题：该问题的解可以表示为对问题的子集依次应用相同解。

但递归函数也有一些缺点：

- 1. 这些函数更耗时，因此程序的执行速度较慢。
- 2. 由于形成栈来保存等待值，占用了更多的内存空间。

## 填空 -
- 1. 函数在最后的 __ 或 __ 上将控制权返回给调用函数。
- 2. 为了不向调用函数返回任何内容，可以使用 ________。
- 3. 传递给函数的参数列表使用 ______ 分隔。
- 4. C 中函数的默认返回类型是 ________。
- 5. 在 C 中，函数传递的所有参数都是通过 ________。
- 6. 通过 ________ 可以实现按引用调用。
- 7. main 是一个 ________ 函数。
- 8. ________ 在函数中是强制性的。
- 9. ________ 是函数调用自身的 ability。
- 10. 程序停止递归的点称为 ____________。
- 11. 递归使用比迭代方法 __________ 的内存。

## 答案 -
- 1. `}` or return statement;
- 2. void
- 3. `,`
- 4. int
- 5. call-by-value
- 6. pointers
- 7. user defined
- 8. arguments
- 9. recursion
- 10. terminating condition
- 11. more

## 已解决的程序

### 1. 编写程序通过用户自定义函数计算数字 n 的 p 次幂。
```
int pow(int,int); /*declaration*/
main()
{
        int n,i,ans,p;
        printf("Enter two numbers: ");
        scanf("%d %d",&n,&p);
        ans=pow(n,p); /*call*/
        printf("%d to the power %d is %d",n,p,ans);
}
int pow(int n,int p) /*definition*/
{
        int i,ans=1;
        for(i=1;i<=p;i++)
                ans=ans*n;
        return(ans);
}
```

### 2. 编写程序使用递归函数计算两个数的最大公约数。
```
int gcd(int, int);
main()
{
int n,m;
int ans;
printf("\n Enter two integer numbers");
scanf("%d %d",&n,&m);
ans = gcd(n,m);
printf("GCD of %d and %d is %d",n,m,ans);
}
int gcd(int n, int m)
{
    if(n >= m && n%m == 0)
        return(m);
    else
        return gcd(m,n%m);
}
```

### 3. 编写程序使用非递归函数计算两个数的最大公约数。
```
int gcd(int,int);
main()
{
    int n,m,ans;
    printf("Enter two integers");
    scanf("%d %d",&n,&m);
    ans = gcd(n,m);
    printf("GCD of %d and %d is %d",n,m,ans);
}
int gcd(int n, int m)
{
    int t;
    while(m!=0)
    {
        t = m;
        m = n % m;
        n = t;
    }
    return (n);
}
```

### 4. 编写程序使用指针搜索子字符串。
```
int strsearch(char [],char []);
main()
{
    char s1[50],s2[10];
    int ans=0;
    printf("Enter a string");        /*input of string */
    gets(s1);
    printf("Enter a string");        /*input of substring to search*/
    gets(s2);
    ans = strsearch(s1,s2);           /*function call*/
    if(ans == -1)                     /*using the returned value*/
        printf("String is not found");
    else
        printf("String is found at pos %d",ans+1);
}
int strsearch(char s1[],char s2[])        /*definition*/
{
    int i,j;
    i=j=0;
    while(s1[i] != '\0')
    {
        if(s1[i] == s2[j])
        {
            while(s1[i+j] == s2[j] && s2[j] != '\0')
                j++;
            if(s2[j] == '\0')
                return (i);
            j=0;
        }
        i++;
    }
    return (-1);
}
```

### 5. 编写程序计算矩阵的行列式*/
```
#define MAXROW 4
#define MAXCOL 4
int det_mat(int [] [MAXCOL],int,int);
main()
{
    int mat[MAXROW][MAXCOL]={0};
    int r,c,i,j,sum;
    printf("Enter dimension of matrix");
    scanf("%d%d",&r,&c);
    /*Input Matrix */
    for(i=0;i<r;i++)
        for(j=0; j<c;j++)
        {
            printf("Enter element %d %d",i+1,j+1);
            scanf("%d",&mat[i][j]);
        }
    /*function call*/
    sum= det_mat(mat,r,c);
    /*output*/
    printf("%d",sum);
}
int det_mat(int mat[] [MAXCOL], int r, int c)
{
    int i,j,k,sign,sum,a;
    int mat2[MAXROW][MAXCOL]={0};
    sign = 1;
    sum = 0;
    if(c == 1)
        return(mat[0][0]);

    for(i=0 ; i<c; i++,sign *= -1)
    {
        for(j=1; j<r; j++)
        {
            for(k=0; k<c; k++)
            {
                if(k == i)
                    continue;
                if(k<i)
                    mat2[j-1][k-1]=mat[j][k];
                else
                    mat2[j-1][k]=mat[j][k];
            }
        }

}
}
    sum = sum + mat[0][i] * sign * det_mat(mat2,r-1,c-1);
}
    return (sum);
}
```

## 填空 –
return 语句只返回 ________。

通过包含适当的表达式并将控制转移到程序的其他部分，可以为 ________ 分配初始值。

一旦控制权从定义它的函数中转移出来，自动变量不会保留 ________。

extern 变量声明必须以存储类说明符 ________ 开始。

如果行 int sp;
    出现在任何函数之外，它 ______________ 外部变量 sp。

if the line
static char buffer[max];
Appears in one file of a program, then the variable name will not conflict with the same name in ________________ of the same program.

外部变量定义不得以存储类说明符 ________ 开始。

## 以下程序的输出会是什么？

| 1. main() { printf("\n welcome in c:"); display(); } | 5. main() { int i = 40,c; c = check(i); printf("\n%d",c); } |

```
display()
{
    printf("History of C:");
    main();
}
```
输出：两个消息将无限打印。

因为当 main( ) 调用 display 控制跳转到 display，并且因为在 display 的主体中再次调用 main 然后控制再次跳转到 main，这个过程会重复。

### 2. main()
```
main()
{
    float area;
    int radius = 1;
    area = circle (radius);
    printf("\n%f",area);
}
circle( int r)
{
    float a;
    a = 3.14*r*r;
    return(a);
}
```
输出：3.000000

因为在函数定义中没有显式的返回类型，默认返回类型是 int，所以当返回 a 即 3.14 时会降为 3。而当 3 以 float 形式打印时，会提升为浮点格式并打印为 3.000000。

### 3. main()
```
}
check(int ch)
{
    if(ch>=40)
        return(100);
    else
        return(10*10);
}
```
输出：100

因为值 i 传递给 ch 即 40。当在函数定义中检查条件时，它为真，所以 if 块被执行并返回 100。

### 6. main()
```
main()
{
    int i = 5, j = 2;
    hello (i, j);
    printf("\n%d %d",i,j);
}
hello(int i, int j)
{
    i = i*i;
    j = j*j;
}
```
输出：5 2

这里函数是按值调用，所以对形式参数的任何更改都不会影响实际参数。因此在 main( ) 函数中 i 和 j 仍然相同。

### 7. main()
```
main()
{
    int x = 5, y = 2;
    hello(&x ,&y);
    printf("\n%d %d",x,y);
}
hello(int *i,int *j)
{
```
```
main();
```
输出：消息将无限打印。

因为 main 再次调用 main()，这将是没有任何终止条件的递归调用，所以消息会无限打印。

```
4. main() {
static int i = 0;
i++;
if (i<=5) {
printf("%d\t",i);
}
else
exit();
}
```
输出：1 2 3 4 5

这里首先执行 i++，每次 i 的值增加 1。第一次它为 1，条件为真并打印 i 的值即 1，现在再次调用 main 函数，我们知道 i 声明为 static，所以它的值不会再次初始化，现在这次递增时它变为 2，以此类推，直到 i 不再为 5，i 会被打印并重复调用 main 函数，但当 i 变为 6 时条件为假，控制跳转

```
*i = *i * *i;
*j = *j * *j;
}
```
输出：25 4

在上述程序中，因为函数是按引用调用，x 和 y 的地址传递给 i 和 j，通过解引用 [*i = *i * *i] 变为 [x = x*x] 得到 25，类似地下一条语句得到 4。因为这里函数是按引用调用，所以它会改变实际参数，然后 x=25 和 y = 4 通过 printf() 打印。

```
8. main() {
int i = 5, j = 3;
calc( &i , j);
printf("\n %d %d",i,j);
}
calc(int *i, int j)
{
*i = *i * *i;
j = j*j
}
```
输出：25 3

这里两个参数传递给被调用函数，首先是 i 的地址，其次是 j 的值，所以当我们解引用 i 时它会改变实际参数，但对 j 的操作不会影响实际参数，所以 j 的值保持不变而 i 得到改变。
