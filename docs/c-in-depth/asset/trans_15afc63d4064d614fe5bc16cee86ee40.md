
## 9.18 使用指针数组表示的字符串排序程序

```c
#include<stdio.h>
#define N 5
main()
{
    char *arrp[N]={ "white","red","green","yellow","blue" };
    int i,j;
    char *temp;
    printf("Before sorting : \n");
    for(i=0;i<N;i++)
        printf("%s\t",arrp[i]);
    printf("\n");
    for(i=0;i<N;i++)
        for(j=i+1;j<N;j++)
            if(strcmp(arrp[i],arrp[j])>0)
            {
                temp=arrp[i];
                arrp[i]=arrp[j];
                arrp[j]=temp;
            }
    printf("After sorting :\n");
    for(i=0;i<N;i++)
        printf("%s\t",arrp[i]);
    printf("\n");
}
```

输出：

排序前 -
    white  red  green  yellow  blue
排序后 -
    blue  green  red  white  yellow

![](img/a76c706396af8b310f291a5313a27079_285_0.png)

这里排序高效，因为交换的只是指针。

## 9.7 sprintf()

### 声明：

```
int sprintf (char *str, const char *controlstring [, argument1, argument2, .........]);
```

此函数与 printf() 函数相同，只是它不会将格式化输出发送到屏幕，而是将格式化输出存储到字符串中。因此借助此函数我们可以将任何数据类型变量转换为字符串。末尾会自动追加空字符。此函数返回输出到字符串的字符数，不包括空字符。程序员有责任使字符串的大小足够大以存储所有参数，从而避免溢出。

在下面的程序中，我们使用 sprintf 将整数和浮点值转换为字符串。

```c
/*P9.19 Program to convert integer and float values to strings using sprintf() function*/
#include<stdio.h>
main()
{
    char str1[10];
    char str2[10];
    int x=1348;
    float y=234.56;
    sprintf(str1,"%d",x);
    sprintf(str2,"%.2f",y);
    printf("str1 = %s,str2 = %s\n",str1,str2);
}
```

### 输出：

str1 = 1348, str2 = 234.56

```c
/*P9.20 Program to understand the use of sprintf() function*/
#include<stdio.h>
main()
{
    char str[30];
    char name[10]="Suresh";
    int m1=89,m2=78,m3=80;
    float per=(m1+m2+m3)/3.0;
    char gr='A';
    sprintf(str,"Result - %s %d %d %d %f %c\n",name,m1,m2,m3,per,gr);
    printf("The string is :\n");
    puts(str);
}
```

### 输出：

字符串为-
Result - Suresh 89 78 80 82.333336 A

## 9.8 sscanf()

```
int sscanf (const char *str, const char *controlstring [, address1, address2, ………]);
```

此函数与 scanf( ) 函数相同，只是数据是从字符串中读取而不是从标准输入读取。我们可以从字符串中读取格式化文本并将其转换为不同数据类型的变量。在下面的程序中，我们有两个字符串，使用 sscanf( ) 将其转换为整数和浮点值。

```c
/*P9.21 Program to convert strings to integer and float values*/
#include<stdio.h>
main()
{
    char str1[10]="1348";
    char str2[10]="234.56";
    int x;
    float y;
    sscanf(str1,"%d",&x);
    sscanf(str2,"%f",&y);
    printf("Value of x = %d, Value of y = %.2f\n",x,y);
}
```

输出：
Value of x = 1348, Value of y = 234.56

```c
/*P9.22 Program to understand the use of sscanf( ) function*/
#include<stdio.h>
main()
{
    struct{
        char name[10];
        int age;
        float sal;
    }emp;
    char str[30]="Anita 23 8000.0";
    sscanf(str,"%s%d%f",&emp.name,&emp.age,&emp.sal);
    printf("Name    : %s\n",emp.name);
    printf("Age     : %d\n",emp.age);
    printf("Salary  : %.2f\n",emp.sal);
}
```

输出：
Name    : Anita
Age     : 23
Salary  : 8000.00

sscanf( ) 可用于验证输入数据。我们知道如何对数据进行简单的有效性检查，例如是否在指定范围内，但如果用户在需要整数的地方开始输入字符串怎么办。这种类型的错误很难检测和纠正。这里我们可以使用 sscanf( ) 来检查是否输入了有效整数值。为此，我们将输入取为字符串而不是整数变量，然后检查该字符串的每个字符，如果字符串中任何字符不是数字、‘+’ 或 ‘-’，则我们可以打印输入不是有效整数的消息。如果输入字符串中的所有字符都是有效的，则我们可以使用 sscanf() 将该字符串转换为整数变量，然后在程序中使用该整数变量。

## 9.9 一些附加问题

### 问题 1

编写一个程序来测试一个词是否为回文。回文是指反转后保持不变的词。例如 – radar, madam

```c
/*P9.23 Program to test whether a word is palindrome or not*/
#include<stdio.h>
#include<string.h>
main()
{
    char str[10];
    int i=0,j,flag;
    printf("Enter the word : ");
    scanf("%s",str);
    j=strlen(str)-1;
    while(i<j)
    {
        if(str[i]==str[j])
            flag=1;
        else
        {
            flag=0;
            break;
        }
        i++;
        j--;
    }
    if(flag==1)
        printf("Word is palindrome\n" );
    else
        printf("Word is not palindrome\n" );
}
```

### 问题 2

编写一个程序将小写字符串转换为大写。

```c
/*P9.24*/
#include<stdio.h>
main()
{
    char str[10];
    int i=0;
    printf("Enter a string in lowercase : ");
    scanf("%s",str);
    while(str[i]!='\0')
    {
        str[i]=str[i]-32;
        i++;
    }
    printf("The uppercase string is : %s\n",str);
}
```

### 问题 3

编写一个程序输入任意字符串并按相反顺序打印它。

```c
/*9.25 Program to enter any string and print it in reverse order.*/
#include<stdio.h>
main()
{
char str[20];
int len;
printf("Enter any string : ");
scanf("%s",str);
len=strlen(str)-1;
while(len>=0)
{
printf("%c",str[len]);
len--;
}
printf("\n");
}
```

### 问题 4

编写一个程序接受任意一行并统计其中的单词数。

```c
/*9.26*/
#include<stdio.h>
main()
{
char line[100];
int count=0,i=0;
printf("Enter the line of text : ");
gets(line);
while(line[i]!='\0')
{
if(line[i]==32)
count++;
i++;
}
if(line[i]=='\0')
count++;
printf("The number of words in line = %d\n", count);
}
```

### 问题 5

编写一个程序输入两个最多包含 80 个字符的字符串。检查这两个字符串并从中删除所有共同字符。显示结果字符串。

```c
/*p9.27*/
#include<stdio.h>
main()
{
    char str1[80],str2[80],str3[80],str4[80];
    int i,j,k,flag;

    printf("Enter the first string : ");
    scanf("%s",str1);
    printf("Enter the second string : ");
    scanf("%s",str2);
    k=0;
    for(i=0;i<strlen(str1);i++)
    {
        flag=0;
        for(j=0;j<strlen(str2);j++)
        {
            if(str1[i]==str2[j])
            {
                flag=1;
                break;
            }
        }
        if(flag!=1)
        {
            str3[k]=str1[i];
            k++;
        }
    }
    str3[k]='\0';

    k=0;
    for(i=0;i<strlen(str2);i++)
    {
        flag=0;
        for(j=0;j<strlen(str1);j++)
        {
            if(str2[i]==str1[j])
            {
                flag=1;
                break;
            }
        }
        if(flag!=1)
        {
            str4[k]=str2[i];
            k++;
        }
    }
    str4[k]='\0';
}
printf("The first string is : %s\n",str3);
printf("The second string is : %s\n",str4);
```

### 问题 6

编写一个程序读取一个字符串并输出该字符串中每个字符的频率。

```c
* P9.28 *
#include<stdio.h>
main()
{
char str[10],ch;
int i,j,n,count;
printf("Enter a string : ");
scanf("%s",str);
n=strlen(str);
for(i=0;i<n;i++)
{
    ch=str[i];
    if(ch!=' ')
    {
        count=0;
        for(j=0;j<n;j++)
        {
            if(ch==str[j])
            {
                count++;
                str[j]=' ';
            }
        }
        printf("%c occurs %d times\n",ch,count );
    }
}
```

### 问题 7

编写一个程序输入一个四位数并以文字形式显示它。

```c
*P9.29*
#include<stdio.h>
main()
{
int n,num,d=0,dig[4];
char *ones[ ]={"","One","Two","Three","Four","Five","Six","Seven","Eight","Nine","Ten"};
char *el[ ]={"Ten","Eleven","Twelve","Thirteen","Fourteen","Fifteen","Sixteen","Seventeen","Eighteen","Nineteen"};
```
