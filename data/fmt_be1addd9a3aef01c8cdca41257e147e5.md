
为字符类型的指针 `p` 分配 10 字节的空间。如下所示：

![](img/fde4da1552d785764c1c370e22af795_202_0.png)

存储 10 个字符的空间
第一个字节的地址

`malloc` 可用于复杂数据类型（如结构体）分配空间：
`str_p=(struct **)malloc(sizeof(struct store));` 其中 `str_p` 是 `struct store` 类型的指针。

`malloc` 用于分配连续字节内存。如果内存空间不足以满足请求，请求可能会失败。如果失败，它返回 `NULL`。

# 分配多个块 (calloc)

`calloc` 也是一种内存分配函数，通常用于为数组和结构体分配内存。`malloc` 用于分配单个存储块，而 `calloc` 分配多个大小相同的存储块，并将其初始化为零。`calloc` 的通用语法是：

```c
P=(cast type*) calloc(n, array size);
P=(int*)calloc (10 , sizeof(int));
```

现在让我们来看：

上面的语句为 10 个块分配连续空间，每个块的大小为 2 字节（因为 `int` 需要两个字节）。所有字节都初始化为零，指针获取分配块的起始地址。像 `malloc` 一样，如果无法满足内存请求也会返回 `NULL`。

# 修改块的大小

我们可能会以后发现之前分配的内存不足，需要额外的空间，或者分配的内存比需要的大。

在这两种情况下，块的大小必须修改，这可以通过使用函数 `realloc`（重新分配内存）来实现。`realloc` 的通用语法是：

```c
P=realloc(P, new size);
```

# 脑操训练

新的大小可以比之前的大，也可以小。现在让我们来看：假设存储 10 个整数的块是用 `malloc` 分配的：

```c
P=(int*)malloc(10 * sizeof(int));
```

现在为了修改大小以便多存储 5 个数字，语句为：

```c
P=realloc(P, 15);
```

该函数为指针 `P` 分配大小为 15 的新内存空间，并返回新块第一个字节的指针。

# 脑操训练

还要记住，新的内存块可能位于旧块相同的位置。在这种情况下，会在其他地方创建一个新的内存空间，将所有旧数据复制那里并将块地址返回给指针。

# 释放使用的空间

如果变量是在编译时声明的，它们将根据销毁

它们的存储类，但如果使用了动态分配，则由程序员负责在不再使用时释放该空间。

当存储空间有限时，这也是必要的。我们可以通过使用函数 `free(p);` 在该空间的数据不再需要时释放内存：

## 1. 编写一个程序从字符串中提取子字符串。

```c
#include<stdio.h>
#include<conio.h>
#include<string.h>
main()
{
    char str[20],news[20];
    char *s,*t;
    int pos, n, i;
    printf("Enter the string:");
    scanf("%s",str);
    printf("Enter the position and number of characters to extract:");
    scanf("%d%d",&pos,&n);
    s=str;
    t=news;
    if(n==0)
        n=strlen(str);
    s=s+pos-1;
    for(i=0;i<n;i++)
    {
        *t=*s;
        s++;
        t++;
    }
    *t='0';
    printf("The substring is: %s\n",news);
    getch();
}
```

## 2. 编写一个程序对 4x4 矩阵的所有元素进行排序。

```c
int mat[4][4],arr, i, j, k, t;
printf("Enter the elements of 4x4 matrix:");
/*matrix输入*/
for(i=0; i<4; i++)
{
    for(j=0; j<4; j++)
    {
        printf("Enter element %d%d",i+1,j+1);
        scanf("%d",&mat[i][j]);
    }
}
/*对矩阵元素排序*/
arr = mat; /*矩阵数组的基地址*/
/*使用指针打印输入时形成的矩阵*/
printf("\nThe matrix formed is...\n");
for(i=0; i<15; i++)/*循环次数*/
{
    for(j=i+1; j<16; j++)
    {
        if(*(arr + i)>(arr+j))
        {
            t = *(arr+i);
            *(arr+i)= *(arr+j);
            *(arr+j)=t;
        }
    }
}
/*打印排序后的矩阵*/
printf("\nT sorted matrix is:\n");
for(i=0; i<4; i++)
{
    for(j=0; j<4; j++)
        printf("%d",mat[i][j]);
    printf("\n");
}
printf("\n\nPress any key to exit...");
getch();
```

## 3. 编写一个程序输入任何字符串并删除其中存在的多余空格。

```c
#include<stdio.h>
#include<conio.h>
#include<string.h>
main() {
    static char s1[50];
    char s2[50];
    char *s, *t;
    int i, l;
    printf("Enter a string");
    gets(s1);
    s=s1;
    t=s2;
    l=strlen(s);
    for(i=0;i<=l-1;i++) {
        if(*s==' '){/*检查空格*/
            if(*s+1)!=' ') {
                *t=*s;
                t++;
            }
            s++;
        } else {
            *t=*s;
            t++;
            s++;
        }
    }
    *t='\0';
    printf("Original Statement:%s\n",s1);
    printf("Modified Statement:%s",s2);
getch();
}
```

## 4. 编写一个程序使用指针拼接字符串。不要使用 strcat 函数。

```c
main()
{
    char s1[20],s2[20],p1,*p2;
    /*输入第一个字符串*/
    printf("Enter 1st string");
    gets(s1);
    /*输入第二个字符串*/
    printf("Enter 2nd string");
    gets(s2);
    /*将字符串地址赋值给两个指针*/
    p1 = s1;
    p2 = s2;
    /*将指针 1 移动到第一个字符串的末尾*/
    while(*p1 != '\0')
        p1++;
    /*将第二个字符串加到第一个字符串的末尾*/
    while(*p2 != '\0')
        *p1++ = *p2++;
    /*在字符串末尾添加 NULL*/
    *p1 = '\0';
    /*输出拼接后的字符串*/
    puts(s1);
    getch();
}
```

## 5. 编写一个程序从键盘接收整数类型的月份和年份，并按照以下格式打印日历。

```c
static char *months[] = {
    "January",
    "February",
    "March",
    "April",
    "May",
    "June",
    "July",
    "August",
    "September",
    "October",
    "November",
    "December"
};
```

```c
int main()
{
    static int days[12]={31,28,31,30,31,30,31,31,30,31,30,31};
    long ndays, tydays;
    int d, i;
    char ch;
    int m, y;
    clrscr();
    printf("Enter year (1900 onwards) month (number):");
    scanf("%d %d",&y,&m);
    ndays=(y-1)*365;
    tydays=(y-1)/4-(y-1)/100+(y-1)/400;
    tydays=ndays+tydays;
    if((y%100==0&&y%400!=0)|(y%4==0&&y%100!=0))
        days[1]=29;
    else
        days[1]=28;
    d=0;
    for(i=0;i<m-2; i++)
        tydays=tydays+days[i];
    tydays=tydays+days[m-1];
    fday=tydays%7;
    cal(y, m, d);
}
```

```c
cal(int yr, int mo, int da)
{
    int i, r, c;
    char a;
    clrscr();
    gotoxy(5,2);
    printf("%s %d",months[mo-1],yr);
    gotoxy(5,5);
    printf("--------------------------------------");
    gotoxy(10,6);
    printf("Mon Tue Thu Fri Sat");
    gotoxy(5,7);
    printf("--------------------------------------");
    r = 9;
    c=11+6*fd;
    for(i=0;i<=da; i++)
    {
        gotoxy(c,r);
        printf("%d",i);
        if(c<=41)
            c=c+6;
        else
        {
            c=11;
            r=r+1;
        }
    }
    gotoxy(5,15);
    printf("--------------------------------------");
    printf("\n\Press any key to exit...");
    getch();
}
```

## 6. 编写一个程序读取一行并删除其中所有的 'the' 单词。

```c
main()
{
    char str[80], str2[80];
    char *s,*q,*p;
    int i;
    clrscr();
    printf("\nEnter a sentence not 80 chars");
    gets(str);
    s = str; /*字符串的基地址*/
    p = str2; /*新字符串的基地址*/
    while(*s)
    {
        q = s;
        if(*s=='t' || *s=='T')
        {
            s++;
            if(*s=='h')
            {
                s++;
                if(*s=='e')
                {
                    s++;
                }
                else
                {
                    for(i=0;i<2;i++)
                        *p++=q++;
                }
            }
        }
        else
        {
            *p++=q++;
            s++;
        }
    }
    // 注意：原文中的逻辑似乎不完整/损坏，但保留了结构。
    // 原文有一个没有匹配的额外 'else'。
    // 根据上下文修正流程：
    if(*s){
        *p++=*s;
        s++;
    }
    *p='\0';
    printf("\n\nSentence after deleting all occurrences of 'the' is:\n");
    puts(str2);
    getch();
}
```

以下程序的输出是什么：

## 1. char *s1,*s2; printf("%d",sizeof(s1),sizeof(s2));

## 26. 你如何动态分配一个二维数组？

输出: 4

```c
Output:
#include<alloc.h>
#define MAXROW 10
#define MAXCOL 10
main() {
    int *p, i, j;
    p=(int *) malloc (MAXROW * MAXCOL * sizeof(int));
    /*矩阵输入*/
}
```

## 2. 表达式 `*p++` 和 `++*p` 相同吗？

输出: 不同。
`*p++` 增加指针本身而不是它所指向的值，而 `++*p` 增加指针 `p` 所指向的值。

## 3. 是否有另一个语句可以完成与 `++*p` 相同的工作？

```c
for(i=0;i<MAXROW;i++) {
    for(j=0;j<MAXCOL;j++) {
        p[i*MAXCOL+j]=i;
        printf("%d",p[i*MAXCOL+j]);
    }
    printf("\n");
}
```

输出: `(*p)++`

## 4. 引用与 `a[i][j][k]` 元素的等效指针表达式是什么？

输出: `*(*(a+i)+j)+k`

## 5. 以下程序的输出是什么：`int a[]={12, 13, 14, 15, 16}; printf("%d %d %d", sizeof(*a), sizeof(a[0]));`

输出: 10 2 2

## 27. 你如何动态分配一个整数二维数组，以便能够使用下标 `a[i][j]` 访问？

## 6. 假设数组位于位置 100，以下程序的输出是什么？

```c
Output:
#include<alloc.h>
#define MAXROW 10
#define MAXCOL 10
main() {"
```

```c
int a[3][4]={1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12};
printf("%u %u", a[0]+1, *(a+0)+1);
```

输出: 100 2

```c
int **p, i, j;
p=(int **) malloc (MAXROW
*sizeof(int*));
```

## 7. 在以下程序中，你会使用 `p` 打印 50 吗？

```c
main())
{
  int a[]={10, 20, 30, 40, 50};
  char *p;
  p=(char*)a);
}
```

输出: `printf("%d",*(int*)p+4);`

```c
for(i=0;i<MAXROW;i++)
np[i]=(int *)malloc(MAXCOL *
sizeof(int));
{
  for(j=0;j<MAXCOL;i++)
    p[i][j] = i;
    printf("%d",p[i][j]);
  }
  printf("\n");
}
```

## 8. 在以下程序中，在 `fun()` 函数中添加一条语句，使 `a` 的地址存储在 `j` 中

```c
void fun(int**);
main()
{
  int *j;
  fun(&j);
  void fun(int**k)
{
    int a=10;
    /*在此处添加语句*/
  }
}
```

输出: `*k=&a;`

## 9. 你如何声明一个指针数组，每个函数接收两个整数并返回一个浮点数？

```c
Output:
#include<alloc.h>
#define MAXROW 3
#define MAXCOL 4
```
