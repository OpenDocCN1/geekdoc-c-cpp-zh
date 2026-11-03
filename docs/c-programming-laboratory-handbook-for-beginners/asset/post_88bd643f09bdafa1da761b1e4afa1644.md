
## Prerequisites for Coding

### getchar function: getchar();

getchar function reads a single character from standard input. It takes no parameters and it returns the input character. In general, a reference to the getchar function is written as

```
variable = getchar();
```

For example,

```c
char c;
c = getchar();
```

The second line causes a single character to be entered from the standard input device and then assigned to c. If an end-of-file condition is encountered when reading a character with the getchar function, the value of the symbolic constant EOF will automatically be returned.

This function can also be used to read multi-character strings, by reading one character at a time within a multi-pass loop.

### putchar function: putchar(variable | constant);

The standard C function that prints or displays a single character by sending it to standard output is called putchar. This function takes one argument, which is the character to be displayed.

For example,

- 1. putchar ('N'); displays the character N.
- 2. char var = '*';
  putchar(var); Displays the character *.

## Algorithm

Start

- **Step 1:** Input a character.
- **Step 2:** If the entered character is non-blank, print it.
- **Step 3:** Otherwise print the first blank character and skip all the consecutive blanks.
- **Step 4:** Repeat steps 1 to 3 till the entered character is a new line character.

Stop

## Flowchart

![](img/dad8bddd927fabdab2417ecbf1eb24eb_60_0.png)

## Program

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

### Sample Outputs

- 1. Enter the text

  ```text
  Hello    World
  The output text is:
  Hello World
  ```

- 2. Enter the text

  ```text
  C    is    a    middle    level    language
  The output text is:
  C is a middle level language
  ```

## Outcomes

- Capable of using built-in standard string functions.
- Should be able to apply the logic to edit large volumes of text.
- Capable of writing C code for other forms of editing.

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

## Unsuccessful Binary Search Example

![](img/dad8bddd927fabdab2417ecbf1eb24eb_64_0.png)

### Algorithm

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

### Flowchart

![](img/dad8bddd927fabdab2417ecbf1eb24eb_65_0.png)

### Program

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

### Results

### Sample Output 1

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

### Sample Output 2

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

### Sample Output 3

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

### Outcomes

- Should be able to understand storing and retrieving of numbers in an array.
- Able to identify the applications that use binary search such as recursive programs, number guessing games, etc.

### Related Program

### Program 1

Write a program in C to input *N* integer numbers in ascending order into a single-dimensional array, and then to perform a binary search for a given key integer number and report success or failure in the form of a suitable message, *using recursive function.*

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

### Output

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

## Term-Work 7

### Problem Definition

Design, develop and execute a program in C to input *N* integer numbers into a single-dimensional array, sort them in ascending order using bubble sort technique and print both the given array and the sorted array with suitable headings.

### Objectives

- To accept an input of random set of numbers and store them in an array.
- To understand the logic of bubble sort technique and code it.

### Related Theory: Logic Used

Sorting method:

- Bubble sort, also known as sinking sort, is a simple sorting algorithm that works by repeatedly stepping through the list to be sorted, comparing each pair of adjacent items and swapping them if they are in the wrong order.
- The pass through the list is repeated until no swaps are needed, which indicates that the list is sorted.
- The algorithm gets its name from the way smaller elements “bubble” to the top of the list. It only uses comparisons to operate on elements, hence it is a comparison sort.

### Sort: Transforms an Unordered Collection to an Ordered One

| 1 | 2 | 3 | 4 | 5 | 6 |
| --- | --- | --- | --- | --- | --- |
| 77 | 42 | 35 | 12 | 101 | 5 |

![](img/dad8bddd927fabdab2417ecbf1eb24eb_71_0.png)

| 1 | 2 | 3 | 4 | 5 | 6 |
| --- | --- | --- | --- | --- | --- |
| 5 | 12 | 35 | 42 | 77 | 101 |
