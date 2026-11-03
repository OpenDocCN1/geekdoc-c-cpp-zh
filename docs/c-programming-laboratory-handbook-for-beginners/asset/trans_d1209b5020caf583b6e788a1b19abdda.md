
## 编程先决条件

### getchar 函数：getchar();

getchar 函数从标准输入读取单个字符。它不接受参数，并返回输入的字符。通常，对 getchar 函数的引用写法如下

```
variable = getchar();
```

例如，

```c
char c;
c = getchar();
```

第二行会从标准输入设备输入一个字符，然后将其赋给 c。如果使用 getchar 函数读取字符时遇到文件结束条件，将自动返回符号常量 EOF 的值。

该函数还可用于读取多字符字符串，方法是在多趟循环中一次读取一个字符。

### putchar 函数：putchar(variable | constant);

通过将单个字符发送到标准输出来打印或显示该字符的标准 C 函数称为 putchar。该函数接受一个参数，即要显示的字符。

例如，

- 1. putchar ('N'); 显示字符 N。
- 2. char var = '*';
  putchar(var); 显示字符 *。

## 算法

开始

- **步骤 1：** 输入一个字符。
- **步骤 2：** 如果输入的字符非空白，则打印它。
- **步骤 3：** 否则打印第一个空白字符，并跳过所有连续空白。
- **步骤 4：** 重复步骤 1 到 3，直到输入的字符为换行符。

停止

## 流程图

![](img/dad8bddd927fabdab2417ecbf1eb24eb_60_0.png)

## 程序

```c
#include<stdio.h>
#include<string.h>
void main()
{
    char c;
    printf("Enter the text\n");
    c=getchar();
    printf("The output text is\n");
    while(c!='\n')
    {
        if(c==' '||c=='\t')
        {
            c=' ';
            putchar(c);
        }
        while(c==' '||c=='\t')
        {
            c=getchar();
            putchar(c);
            c=getchar();
        }
    }
    printf("\n");
}
```

### 示例输出

- 1. 输入文本

  ```text
  Hello    World
  The output text is:
  Hello World
  ```

- 2. 输入文本

  ```text
  C    is    a    middle    level    language
  The output text is:
  C is a middle level language
  ```

## 成果

- 能够使用内置的标准字符串函数。
- 应能够应用该逻辑编辑大量文本。
- 能够编写用于其他编辑形式的 C 代码。

## 3.1.1 随机事件的概率

在初中，我们已经初步了解了随机事件的概念，并列举了在下列具体情境中的一些随机事件：

- 抛掷一枚硬币，结果出现正面;
- 篮球运动员投篮一次，结果命中;
- 从一副扑克牌中抽出一张牌，结果抽出的是红桃;

随机事件在一次试验中是否发生是不确定的，但在同一条件下进行大量重复试验时，随机事件的发生是否具有规律性呢？我们来做一个试验：

### 试验

把全班同学分成10个小组，每小组抛掷一枚硬币20次，记录“正面向上”的次数，然后统计"正面向上"的频数和频率，并填写下表：

| 投掷次数 | 出现正面的次数 | 出现正面的频率 |
| --- | --- | --- |
| 20 | | |
| 40 | | |
| 60 | | |
| 80 | | |
| 100 | | |
| 120 | | |
| 140 | | |
| 160 | | |
| 180 | | |
| 200 | | |

观察上表，你能发现什么规律？

历史上，有些数学家曾经做过成千上万次抛掷硬币的试验。

| 试验者 | 抛掷次数(n) | 出现正面的次数(m) | 出现正面的频率(m/n) |
| --- | --- | --- | --- |
| 棣莫弗 | 2048 | 1061 | 0.5181 |
| 布丰 | 4040 | 2048 | 0.5069 |
| 费勒 | 10000 | 4979 | 0.4979 |
| 皮尔逊 | 12000 | 6019 | 0.5016 |
| 皮尔逊 | 24000 | 12012 | 0.5005 |

在抛掷硬币的试验中，随着试验次数的增加，“正面向上”的频率稳定在0.5附近。

对于随机事件，从概率的定义可知：随机事件A的概率P(A)满足0≤P(A)≤1。当A是必然事件时，P(A)=1；当A是不可能事件时，P(A)=0。

一般地，在大量重复进行同一试验时，事件A发生的频率m/n总是接近于某个常数，在它附近摆动，这时就把这个常数叫做事件A的概率，记作P(A)。

## 不成功的二分查找示例

![](img/dad8bddd927fabdab2417ecbf1eb24eb_64_0.png)

### 算法

```text
Start
Step 1: Read the array size.
Step 2: Read the array elements.
Step 3: Read the key element to be searched.
Step 4: If the key element is equal to the middle element of the array,
            Print search is successful.
         Else if the element is greater than the middle element,
            Perform binary search in the second half of the array
         Else
            Perform binary search in the first half of the array.
Stop
```

### 流程图

![](img/dad8bddd927fabdab2417ecbf1eb24eb_65_0.png)

### 程序

```c
#include<stdio.h>
#include<process.h>
void main()
{
  int n,i,a[10],key,low,high,mid;
  printf("\n Enter the no. of elements:");
  scanf("%d",&n);
  printf("\n Enter %d elements in ascending order",n);
  for(i=0 ; i<n ; i++)
    scanf("%d",&a[i]);
  printf("\n Enter the key element to search: ");
  scanf("%d",&key);
  low=0;
  high=n-1;
  while(low<=high)
  {
    mid=(low+high)/2;
    if(key==a[mid])
    {
      printf("\nSearch Successful");
      exit(0);
    }
    else if(key>a[mid])
      low=mid+1;
    else
      high=mid-1;
  }
  printf("\n Unsuccessful Search");
}
```

### 结果

### 示例输出 1

```text
Enter the no. of elements: 5
Enter 5 elements in ascending order
2
3
4
5
6
Enter the key element to search: 5
Search Successful
```

### 示例输出 2

```text
Enter the no. of elements: 8
Enter 8 elements in ascending order
1
12
23
34
56
63
64
88
Enter the key element to search: 66
Unsuccessful Search
```

### 示例输出 3

```text
Enter the no. of elements: 6
Enter 6 elements in ascending order
11234
12234
23441
23453
26090
3000
Enter the key element to search: 26090
Search Successful
```

### 成果

- 应能够理解数组中数字的存储和检索。
- 能够识别使用二分查找的应用，例如递归程序、猜数字游戏等。

### 相关程序

### 程序 1

编写一个 C 程序，按升序将 *N* 个整数输入一维数组，然后对给定的关键字整数执行二分查找，并以合适的消息形式报告成功或失败，*使用递归函数。*

```c
#include <stdio.h>
#define MAX_LEN 10

/* Recursive function*/
int bsearch_recursive(int l[],int arrayStart,int arrayEnd,int a)
{
    int m,pos;
    if(arrayStart<=arrayEnd)
    {
        m=(arrayStart+arrayEnd)/2;
        if (l[m]==a)
            return m;
        else if (a<l[m])
            return bsearch_recursive(l,arrayStart,m-1,a);
        else
            return bsearch_recursive(l,m+1,arrayEnd,a);
    }
    return -1;
}

void read_list(int l[],int n)
{
    int i;
    printf("\nEnter the elements:\n");
    for(i=0;i<n;i++)
        scanf("%d",&l[i]);
}

void print_list(int l[],int n)
{
    int i;
    for(i=0;i<n;i++)
        printf("%d\t",l[i]);
}
/*main function*/

void main()
{
    int l[MAX_LEN], num, ele,f,ll,a;
    int ch,pos;
    printf("\n Binary Search using Recursion method");
    printf("\n=============================================");
    printf("\nEnter the number of elements: ");
    scanf("%d",&num);
    read_list(l,num);
    printf("\nElements present in the list are:\n\n");
    print_list(l,num);
    printf("\n\nEnter the element you want to search:\n\n");
    scanf("%d",&ele);
    pos=bsearch_recursive(l,0,num,ele);
    if(pos==-1)
    {
        printf("Element is not found");
    }
    else
    {
        printf("Element is found at %d position",pos);
    }
}
```

### 输出

```text
1.
Binary Search using Recursion method
=============================================
Enter the number of elements: 5
Elements present in the list are:
1
2
3
4
5
Enter the element you want to search: 5
Element is found at 4 position

2.
Binary Search using Recursion method
=============================================
Enter the number of elements: 8
Elements present in the list are:
10
20
30
40
50
60
70
80
Enter the element you want to search: 100
Element is not found
```

## 学期作业 7

### 问题定义

设计、开发并执行一个 C 程序，将 *N* 个整数输入一维数组，使用冒泡排序技术按升序对它们排序，并在合适的标题下打印给定数组和排序后的数组。

### 目标

- 接受一组随机数字的输入并将其存储在数组中。
- 理解冒泡排序技术的逻辑并编写代码。

### 相关理论：所用逻辑

排序方法：

- 冒泡排序，也称为沉底排序，是一种简单的排序算法，其工作方式是反复遍历待排序列表，比较每对相邻项，如果顺序错误则交换它们。
- 重复遍历列表，直到不需要交换为止，这表明列表已排序。
- 该算法因较小元素“冒泡”到列表顶部的方式而得名。它仅使用比较来操作元素，因此是一种比较排序。

### 排序：将无序集合转换为有序集合

| 1 | 2 | 3 | 4 | 5 | 6 |
| --- | --- | --- | --- | --- | --- |
| 77 | 42 | 35 | 12 | 101 | 5 |

![](img/dad8bddd927fabdab2417ecbf1eb24eb_71_0.png)

| 1 | 2 | 3 | 4 | 5 | 6 |
| --- | --- | --- | --- | --- | --- |
| 5 | 12 | 35 | 42 | 77 | 101 |

