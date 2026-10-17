
`fr++`;

`scanf("%d",&num)`;

if (`num==0`) return 0;

`queue[fr]=num`;

`re=fr`;

do{
    ++`re`;
    if (`re>cur`) break;
    `scanf("%d",&num)`;
    if (`num==0`) break;
    `queue[re]=num`;
}while(`re<cur`)

return 0;
}

void `insert()`
{
    if(`re<cur`)
    {
        puts("Queue is full");
        exit(0);
    }
    puts("Enter a number to be inserted: ");
    `scanf("%d",&num)`;
    `queue[re]=num`;
}

void `del()`
{
    if(`fr==re`)
    {
        puts("The queue is empty"); exit(0);
        `fr++`;
    }
    `num=queue[fr]`;
    if(`fr==n`)
    {
        `fr=1`;
        `re=1`;
    }
}

void `show()`
{
    for(`m=fr`;`m<=re`;++`m`)
```
printf(" %d ",queue[m]);
getch();
}
```

输出
1] Create
2] Insert
3] Delete
4] Show
5] End
Enter Your choice:
4
2 3 0

### 解释：

我们已经在上一个程序中熟悉了 `create`、`insert` 和 `delete` 操作。在这个程序中，为不同的任务（如创建、插入和删除操作）定义了单独的函数。现在我们将逐一讨论。

在 `create` 函数中，用户必须输入要进入队列的元素数量。用户还需要输入。如果插入了 0，控制将从函数退出。0 被视为一个元素，它是它是为了退出函数而进入的。如果元素小于容量，剩余部分将保持为空。如果有空间，则使用 `insert()` 函数插入元素。如果队列已经填满，此操作将不起作用。`delete()` 函数用于删除元素。显示时使用 `show()` 函数。你可能已经注意到 `main()` 函数被递归调用，以便使用户选择操作。

## 5.6 动态实现（指针）

动态实现是使用指针实现的。通过在连续的内存位置上应用递增操作，可以访问内存并在该位置上存储元素。因此，元素序列可以连续存储直到任意数量的元素。程序员必须保留存储第一个元素的指针的起始地址。以此类，可以查看或修改这些数字。这里有一个简单的示例。

示例 5.7 编写一个程序使用指针实现队列。

```c
# include <stdio.h>
#include <conio.h>
#include <process.h>
void main()
{
    int *q;
    int rear=0;
    clrscr();
while(1)
{
    printf("Enter element: ");
    scanf("%d",&q);
    q++;
    rear++;
    if(rear==7)
    {
        printf("\n Queue is full\n");
        break;
    }
}
```
```c
q=q-rear;
printf("\n Elements of Queue are: ");
rear=0;
while(rear<7)
{
    printf("\n Element: %d rear=%d", *(q+rear),rear);
    rear++;
}
```

输出
Enter element: 4
Enter element: 2
Enter element: 3
Enter element: 4
Enter element: 7
Enter element: 8
Enter element: 9
Queue is full
Elements of Queue are:
Element: 4 rear=0
Element: 2 rear=1
Element: 3 rear=2
Element: 4 rear=3
Element: 7 rear=4
Element: 8 rear=5

解释：

在此程序中，使用了指针。通过对连续位置执行递增操作，可以访问内存并在该位置上存储元素。因此，元素序列可以连续存储直到任意数量的元素。程序员必须保留存储第一个元素的指针的起始地址。以此类推，可以查看或修改这些数字。这里有一个简单的示例。

## 5.7 插入和删除操作

在此程序中，使用了指针。通过对连续位置执行递增操作，可以访问内存并在该位置上存储元素。因此，元素序列可以连续存储直到任意数量的元素。程序员必须保留存储第一个元素的指针的起始地址。以此类推，可以查看或修改这些数字。这里有一个简单的示例。

示例 5.8 编写一个程序执行队列的不同操作，如插入、删除和显示元素。

# 队列

队列操作
1: 创建
2: 插入
3: 删除
4: 显示
5: 退出
输入您的选项：
4
1 2 4 5

# 解析：

在程序程序中，在 `main()` 之前声明了所需的变量和函数原型。用户可以执行不同的操作，且输入的元素将存储在队列中。使用 `while` 循环会要求用户输入选项。用户输入的选项将传递给 `switch()` 分支语句，在其中执行相应的 `case` 语句。 实际上，`case` 语句会调用函数并开始操作。

`create` 函数用于向队列中插入元素。在此函数中，用户必须输入要插入的元素个数，随后由用户输入这些数字。如果 `f`（队头）的值为 0，则执行 `if` 块。通过 `while` 循环反复输入元素并存储在队列中。在每次循环中，变量 `r` 都会加1。`insert()` 函数用于在队列的指定位置插入元素。变量 `j` 的值为 10，是队列能够容纳的最大数量。如果 `r`（队尾）的值大于 `j`，简单意思是队列已满，`return` 语句会挂函数执行。如果队列为空且在下一个可用位置，则存储新输入的元素。

在 `erase()` 函数中，首先比较 `r`（队尾）和 `f`（队头）的值，如果它们相同，则意味着队列为空。队头和队尾的值意味着队列没有元素。如果 `if` 和 `j`（最大数量）相同，则两个变量都被设置为 0。

`show()` 函数用于将元素作为输出。循环从 `front` 的值执行到 `rear` 的值。在 `erase()` 函数中，元素并没有被实际删除，而是增加了 `front`的位置。该函数用于显示元素。在 `front` 位置之前，元素物理上是存在的。我们也可以物理地删除它们，但那样我们需要将元素移动到数组的开头。

## 5.8 队列的类型

在过去的几周里，我们学习了简单队列并已经看到了它的缺点。当队尾指针到达队列（数组）末尾时，无法向队列中添加更多元素，即使数组的起始内存位置是空的。为了克服这一缺点，可以应用不同类型的队列。不同类型的队列有：

### 5.8.1 循环队列

简单队列或直线队列有我们已知的若干局限性，即使队列开头的内存位置可用，也无法如图 5.9 所示插入元素。我们可以通过使用循环队列来有效地利用直线队列的可用空间。

## 5.20 使用 C 语言的数据结构

| | 5 | 8 | 7 |
|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 |
| Front = 3 | | | rear = 5 | | |

图 5.9 带有空位的简单队列

在上面的讨论中，假设 `front` 没有移动到队列的开头。如图 5.10 所示，循环队列像一个轮子或完美的环。$c$ [4] 是为了实现循环队列而声明的数组。然而，在逻辑上元素以循环方式出现，但在计算机内存中，它们被存储在连续的内存位置。

![](img/c2f6b24e88575cdba9137937a75b3615_162_0.png)

图 5.10 循环队列

在循环队列中，第一个元素存储在最后一个元素之后。如果队列的最后一个位置被占用，则新元素将插入到实现数组（队列）的第一个内存位置。例如，$C[n]$，$C$ 是一个包含 $n$ 个元素的队列。在插入后，在最后一个内存位置 $[(n-1)th]$ 存储一个元素后，下一个元素将存储在第一个位置，如果...（注：此处原文不完整，已按现有内容翻译）

在上述程序中，假设插入的元素为 1,2,3,4,5 和 6，并考虑它们在数组中的位置从第 0 到第 5 个。队列状态为满。如果我们继续移除元素，元素将一个接一个移除。删除第 0 位置的元素后，该位置将保持为空。现在，如果插入一个元素（假设为 7），它将如图 5.13 所示存储在第 0 位置。

由于循环队列机制，如果最后一个位置被占用且起始位置为空，则元素将插入到空位置。如果我们继续移除元素，元素将按照 2,3,4,5,6 和 7 的顺序被移除。然而，7 存储在数组的第 0 位置，但它是最后被插入的元素。

![](img/c2f6b24e88575cdba9137937a75b3615_167_0.png)

图 5.13 循环队列（删除和插入后）

### 5.8.2 双端队列

到为止，我们学习了栈和队列。栈只有一个端，可以交替插入和删除元素。另一方面，双端队列有两个端：头部和尾部。头部用于移除元素，尾部用于插入元素。在这里，在双端队列中，插入和删除可以从两端执行，因此，它被称为双端队列，简称为 deque。它是一个元素的同构列表。deque 是栈和队列的通用表示，可以用作栈和队列。有多种方法实现链表，并可以使用数组来执行双端队列。数组的实现简单且直观。

考虑下面的图 5.14：

![](img/c2f6b24e88575cdba9137937a75b3615_167_1.png)

图 5.14 双端队列

在双端队列中，有必要固定在头部和尾部要执行的操作类型。双端队列可以分为两类：

## 5.26 使用 C 语言的数据结构

输入限制双端队列：在输入限制双端队列中，插入和删除操作在尾部执行，而头部只执行删除操作。图 5.15 表示了输入限制双端队列。

在输入限制双端队列中可以以下操作：

- 1. 在尾部插入元素。
- 2. 在头部和尾部删除元素。

![](img/c2f6b24e88575cdba9137937a75b3615_168_0.png)

因此，输入限制双端队列允许单端插入和两端删除。

## 示例 5.10 编写一个程序演示输入限制双端队列。

```c
#include <stdio.h>
#include <conio.h>
int ird[5];
void main()
{
int r=0
```
```c
{
  c=1;
  r--;
} else
  if(f<0) 
    printf("\n Deque is full ");
    getch();
    break;
    case 2: deleter(-r,f);break;
    case 3: deletef(r,++);
    break;
    case 4: show (); break;
    default: exit(0);
  }
}
}
```
```c
void show() {
  int j;
  printf("\n Elements of deque are: ");
  for(j=0;j<5;j++)
    printf(" %d ",ird[j]);
  getch();
n
}
```
```c
int insert(int h) {
  int k;
  printf("\n Enter an element (enter 0 to exit): ");
  scancf("%d",&k);
  ird[h]=k;
  return(k);
}
```
```c
void deleter(int m,int n) {
  if(m<=n)
    printf("\n Deque is empty ");
  else {
    printf("\n %d The element deleted: %d",m,ird[m]);
    ird[m]=0;
    getch();
  }
}
```
```c
void deletef(int f,int j) {
  if(f<j)
```
```c
printf("Deque is empty");
else{
    printf("\n %d The element deleted: %d",j,ird[j]);
    ird(f)=NULL;
}
getch();
```

OUTPUT:
(1) Insert from rear
(2) Delete from rear
(3) Delete from front
(4) Display
(0) Exit
Enter Your choice:- 1
Enter an element (enter 0 to exit): 2
Enter an element (enter 0 to exit): 3
Enter an element (enter 0 to exit): 5
Enter an element (enter 0 to exit): 8
Enter an element (enter 0 to exit): 6
Deque is full
(1) Insert
(2) Delete from rear
(3) Delete from front
(4) Display
(0) Exit
Enter Your choice:- 4
Elements of deque are: 2 3 5 8 6

## Explanation:

程序的输出没有完全显示。用户可以通过执行它看到结果。记住，在输入限制双端队列中，插入只能从尾部进行，并通过 `insert()` 函数执行。循环用于连续执行 `insert()` 函数。用户可以输入元素，当输入 0 时，循环终止。因此，执行了元素的插入。变量 `r` (尾部) 增加，其值不应超过数组的最大容量，即 5，且在 while 循环条件中是相同的。

我们可以选择移除元素。我们可以从两端移除元素。如果我们选择第二个选项，则从尾部移除元素。变量 `r` (尾部) 递减，队列的 `rh` 元素被擦除。此选项有一个副作用。删除操作产生的空位置可以使用插入操作来填充。然而，如果我们选择选项 3，情况就不同。在这种情况下，元素从头部删除，在队列开头创建了空空间。如果我们想在该位置插入元素，则将使用插入选项。

输出限制双端队列允许单端插入和两端删除。如图所示 ![](img/c2f6b24e88575cdba9137937a75b3615_168_0.png)

输入限制双端队列

在输入限制双端队列中可以以下操作：

- 1. 在尾部插入元素。
- 2. 在头部和尾部删除元素。

因此，输入限制双端队列允许单端插入和两端删除。

示例 5.10 编写一个程序演示输入限制双端队列。

```c
#include <stdio.h>
#include <conio.h>
int ird[5];
void main()
{
int r=0
```
```c
{
  c=1;
  r--;
} else
  if(f<0) 
    printf("\n Deque is full ");
    getch();
    break;
    case 2: deleter(-r,f);break;
    case 3: deletef(r,++);
    break;
    case 4: show (); break;
    default: exit(0);
  }
}
}
```
```c
void show() {
  int j;
  printf("\n Elements of deque are: ");
  for(j=0;j<5;j++)
    printf(" %d ",ird[j]);
  getch();
n
}
```
```c
int insert(int h) {
  int k;
  printf("\n Enter an element (enter 0 to exit): ");
  scancf("%d",&k);
  ird[h]=k;
  return(k);
}
```
```c
void deleter(int m,int n) {
  if(m<=n)
    printf("\n Deque is empty ");
  else {
    printf("\n %d The element deleted: %d",m,ird[m]);
    ird[m]=0;
    getch();
  }
}
```
```c
void deletef(int f,int j) {
  if(f<j)
```
```c
printf("Deque is empty");
else{
    printf("\n %d The element deleted: %d",j,ird[j]);
    ird(f)=NULL;
}
getch();
