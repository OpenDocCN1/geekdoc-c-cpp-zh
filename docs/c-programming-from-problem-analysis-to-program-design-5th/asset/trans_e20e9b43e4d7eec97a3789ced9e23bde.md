

```cpp
void arrayAsParameter(int list[], int size)
{
    .
    .
    .

    list[2] = 28;        //第4行

    .
    .
    .
}
```

另外，假设你有如下对该函数的调用：

```cpp
arrayAsParameter(myList, 5);   //第5行
```

在这个语句中，`myList`的基地址被传递给了形参`list`。因此，`list`的基地址是1000。该函数的定义包含语句`list[2] = 28;`。该语句将28存储到`list[2]`中。为了访问`list[2]`，计算机按如下方式计算地址：1000 + 4 * 2 = 1008。于是，从地址1008开始，计算机访问接下来的四个字节并存储28。注意，实际上1008就是`myList[2]`的地址（参见图9-7）。因此，在执行第5行的语句期间，第4行的语句将值28存储到了`myList[2]`中。同时，在执行第5行的函数调用语句期间，`list[index]`和`myList[index]`指向相同的内存空间，其中0 <= index且index < 5。

> **注意**
>
> 如果C++允许按值传递数组，那么计算机就必须为形参的组件分配内存，并在函数调用时将实际数组的内容复制到对应的形参中。如果数组规模很大，这个过程会浪费内存以及复制数据所需的计算机时间。这就是为什么在C++中数组总是按引用传递的原因。

## 函数不能返回数组类型的值

C++不允许函数返回数组类型的值。请注意，前面描述的`sumArray`和`indexLargestElement`函数返回的是`int`类型的值。

### 示例9-7

下面的程序演示了在函数调用中数组如何作为实参传递。（请注意，该程序使用了示例9-6中编写的函数。）

```cpp
//数组作为函数的参数

#include <iostream>
using namespace std;

const int ARRAY_SIZE = 10;

void initializeArray(int x[],int sizeX);
void fillArray(int x[],int sizeX);
void printArray(const int x[],int sizeX);
int sumArray(const int x[],int sizeX);
int indexLargestElement(const int x[],int sizeX);
void copyArray(int list1[], int src, int list2[],
               int tar, int numOfElements);

int main()
{
    int listA[ARRAY_SIZE] = {0};    //声明数组listA
                                    //包含10个组件，并将
                                    //每个组件初始化为0。
    int listB[ARRAY_SIZE];          //声明数组listB
                                    //包含10个组件。

    cout << "Line 1: listA元素: ";      //第1行

        //使用函数printArray输出listA的元素
    printArray(listA, ARRAY_SIZE);           //第2行
    cout << endl;                            //第3行

        //使用函数initializeArray初始化listB
    initializeArray(listB, ARRAY_SIZE);      //第4行

    cout << "Line 5: listB元素: ";      //第5行

        //输出listB的元素
    printArray(listB, ARRAY_SIZE);           //第6行
    cout << endl << endl;                    //第7行

    cout << "Line 8: 输入 " << ARRAY_SIZE
         << " 个整数: ";                   //第8行

        //使用函数fillArray向listA输入数据
    fillArray(listA, ARRAY_SIZE);            //第9行
    cout << endl;                            //第10行

    cout << "Line 11: 填充listA后，"
         << "元素为:" << endl;     //第11行

        //输出listA的元素
    printArray(listA, ARRAY_SIZE);           //第12行
    cout << endl << endl;                    //第13行
```

## 声明数组的其他方式

假设一个班有20名学生，你需要记录他们的成绩。因为学生人数每学期都可能变化，与其在声明数组时指定大小，不如按如下方式声明数组：

```cpp
const int NO_OF_STUDENTS = 20;
int testScores[NO_OF_STUDENTS];
```

用于声明数组的其他形式如下：

```cpp
const int SIZE = 50;          //第1行
typedef double list[SIZE];    //第2行

list yourList;                //第3行
list myList;                  //第4行
```

第2行的语句定义了一个数据类型`list`，它是包含50个`double`类型组件的数组。第3行和第4行的语句声明了两个变量`yourList`和`myList`。两者都是包含50个`double`类型组件的数组。当然，这些语句等价于：

```cpp
double yourList[50];
double myList[50];
```

## 在数组中搜索特定项

在列表中搜索给定项是对列表执行的最常见操作之一。我们描述的搜索算法称为**顺序搜索**或**线性搜索**。顾名思义，你从第一个数组元素开始依次搜索数组。你将`searchItem`与数组（列表）中的元素进行比较，并继续搜索，直到找到该项或列表中不再有数据可与`searchItem`比较为止。

考虑图9-8中显示的七个元素的列表。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_547_0.png)

图9-8 七个元素的列表

假设你想确定27是否在列表中。顺序搜索的工作方式如下：首先，你将27与`list[0]`比较，即将27与35比较。因为`list[0] ≠ 27`，接着将27与`list[1]`比较，即与列表中的第二项12比较。因为`list[1] ≠ 27`，你将27与列表中的下一个元素比较，即将27与`list[2]`比较。因为`list[2] = 27`，搜索停止。这次搜索成功。

现在让我们搜索10。和之前一样，搜索从列表的第一个元素开始，即从`list[0]`开始。按前述方式进行，我们看到这次搜索项10与列表中的每一项都进行了比较。最终，列表中不再有数据可与搜索项比较。这是一次不成功的搜索。

因此可以得出，一旦你在列表中找到与搜索项相等的元素，就必须停止搜索并报告成功。（在这种情况下，通常还需要报告搜索项在列表中找到的位置。）否则，在搜索项与列表中每个元素都不成功比配后，你必须停止搜索并报告失败。

假设包含列表元素的数组名为`list`。前面的讨论转化为以下顺序搜索算法：

```
found被设为false;
loc = 0;

while (loc < listLength and not found)
    if (list[loc]等于searchItem)
        found被设为true
    else
        将loc加1

if (found)
    返回loc;
else
    返回-1;
```

以下函数对列表执行顺序搜索。具体来说，为了便于说明，我们假设列表元素为`int`类型。

```cpp
int seqSearch(const int list[], int listLength, int searchItem)
{
    int loc;
    bool found = false;

    loc = 0;

    while (loc < listLength && !found)
        if (list[loc] == searchItem)
            found = true;
        else
            loc++;

    if (found)
        return loc;
    else
        return -1;
}
```

如果函数`seqSearch`返回的值大于或等于0，则搜索成功；否则，搜索不成功。

从这个代码中可以看出，你首先将`searchItem`与列表中的第一个元素进行比较来开始搜索。如果`searchItem`等于列表中的第一个元素，则退出循环；否则，`loc`加1以指向列表中的下一个元素。然后你将`searchItem`与列表中的下一个元素进行比较，依此类推。

### 示例9-8

```cpp
// 该程序演示了如何在程序中
// 使用顺序搜索。

#include <iostream>                                      //第1行

using namespace std;                                     //第2行

const int ARRAY_SIZE = 10;                               //第3行

int seqSearch(const int list[], int listLength,
              int searchItem);                           //第4行

int main()                                               //第5行
{
    int intList[ARRAY_SIZE];                              //第7行
    int number;                                           //第8行

    cout << "第9行: 输入" << ARRAY_SIZE
         << "个整数。" << endl;                        //第9行

    for (int index = 0; index < ARRAY_SIZE; index++)      //第10行
        cin >> intList[index];                            //第11行

    cout << endl;                                         //第12行

    cout << "第13行: 输入要搜索的"
         << "数字: ";                                //第13行
    cin >> number;                                        //第14行
    cout << endl;                                         //第15行

    int pos = seqSearch(intList, ARRAY_SIZE, number);     //第16行

    if (pos != -1)                                        //第17行
        cout << "第18行: " << number
             << " 在位置" << pos
             << "处找到" << endl;                                     //第18行
    else                                               //第19行
        cout << "第20行: " << number
             << " 不在列表中。" << endl;           //第20行

    return 0;                                             //第21行
}                                                        //第22行

//将前面给出的函数seqSearch的定义
//放在这里。
```

