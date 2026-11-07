
考虑以下语句：

```cpp
int list[10];
```

像下面这样的循环可能会使 list 的索引越界：

```cpp
for (int i = 0; i <= 10; i++)
    list[i] = 0;
```

当 i 变为 10 时，循环测试条件 i <= 10 求值为 true，循环体执行，从而将 0 存入 list[10]。从逻辑上讲，list[10] 并不存在。

> **注意** 在某些新编译器上，如果程序中的数组索引越界，程序可能会终止并显示错误消息。例如，参见程序 `Example_ArrayIndexOutOfBoundsA.cpp` 和 `Example_ArrayIndexOutOfBoundsB.cpp` 以及本书配套网站。

## 声明期间的数组初始化

像任何简单变量一样，数组可以在声明时初始化。例如，以下 C++ 语句声明了一个包含五个分量的数组 sales，并初始化这些分量。

```cpp
double sales[5] = {12.25, 32.50, 16.90, 23, 45.68};
```

这些值放在花括号之间并用逗号分隔——这里，sales[0] = 12.25，sales[1] = 32.50，sales[2] = 16.90，sales[3] = 23.00，sales[4] = 45.68。

在声明数组时进行初始化，不必指定数组的大小。大小由花括号中初始值的数量决定。但是，必须包含数组名后的方括号。因此，前一条语句等价于：

```cpp
double sales[] = {12.25, 32.50, 16.90, 23, 45.68};
```

尽管如果在声明期间初始化数组，则不必指定数组的大小，但这样做是一种良好实践。

## 声明期间数组的部分初始化

当同时声明并初始化数组时，不需要初始化数组的所有分量。此过程称为**声明期间数组的部分初始化**。但是，如果在声明期间部分初始化数组，则必须谨慎。以下示例有助于解释在声明并部分初始化数组时会发生什么。

语句：

```cpp
int list[10] = {0};
```

### 示例 8-5

考虑以下函数：

```cpp
void funcArrayAsParam(int listOne[], double listTwo[])
{
    .
    .
    .
}
```

函数 `funcArrayAsParam` 有两个形参：(1) `listOne`，一个类型为 `int` 的一维数组（即分量类型为 `int`）；(2) `listTwo`，一个类型为 `double` 的一维数组。在此声明中，两个数组的大小均未指定。

有时，数组中的元素数量可能小于数组的大小。例如，存储学生数据的数组中的元素数量可能随着学生退课或加课而增加或减少。在这种情况下，我们只想处理数组中保存实际数据的分量。要编写处理此类数组的函数，除了将数组声明为形参外，还要声明另一个形参来指定数组中的元素数量，如下面的函数所示：

```cpp
void initialize(int list[], int listSize)
{
    for (int count = 0; count < listSize; count++)
        list[count] = 0;
}
```

函数 `initialize` 的第一个参数是任意大小的 `int` 数组。调用函数 `initialize` 时，实际数组的大小作为函数 `initialize` 的第二个参数传入。

## 常量数组作为形参

回想一下，当形参是引用参数时，每当形参改变，实参也会改变。然而，尽管数组总是按引用传递，你仍然可以阻止函数更改实参。为此，在形参声明中使用保留字 `const`。考虑以下函数：

```cpp
void example(int x[], const int y[], int sizeX, int sizeY)
{
    .
    .
    .
}
```

这里，函数 `example` 可以修改数组 x，但不能修改数组 y。任何更改 y 的尝试都会导致编译时错误。如果不希望函数修改数组，则将数组声明为常量形参是一种良好的编程实践。

### 示例 8-6

此示例展示如何编写用于数组处理的函数，以及如何将数组声明为形参。

```cpp
//Function to initialize an int array to 0.
//The array to be initialized and its size are passed
//as parameters. The parameter listSize specifies the
//number of elements to be initialized.
void initializeArray(int list[], int listSize)
{
    for (int index = 0; index < listSize; index++)
        list[index] = 0;
}

//Function to read and store the data into an int array.
//The array to store the data and its size are passed as
//parameters. The parameter listSize specifies the number
//of elements to be read.
void fillArray(int list[], int listSize)
{
    for (int index = 0; index < listSize; index++)
        cin >> list[index];
}

//Function to print the elements of an int array.
//The array to be printed and the number of elements
//are passed as parameters. The parameter listSize
//specifies the number of elements to be printed.
void printArray(const int list[], int listSize)
{
    for (int index = 0; index < listSize; index++)
        cout << list[index] << " ";
}

//Function to find and return the sum of the
//elements of an int array. The parameter listSize
//specifies the number of elements to be added.
int sumArray(const int list[], int listSize)
{
    int sum = 0;

    for (int index = 0; index < listSize; index++)
        sum = sum + list[index];

    return sum;
}

//Function to find and return the index of the first
//largest element in an int array. The parameter listSize
//specifies the number of elements in the array
int indexLargestElement(const int list[], int listSize)
{
    int maxIndex = 0; //assume the first element is the largest

    for (int index = 1; index < listSize; index++)
        if (list[maxIndex] < list[index])
            maxIndex = index;

    return maxIndex;
}

//Function to copy some or all of the elements of one array
//into another array, starting at the position specified
//by src, the elements of list1 are copied into list2,
//starting at the position specified by tar. The parameter
//numOfElements specifies the number of elements of list1 to
//be copied into list2. Starting at the position specified
//by tar, list2 must have enough components to copy the
//elements of list1. The following call copies all of the
//elements of list1 into the corresponding positions in
//list2: copyArray(list1, 0, list2, 0, numOfElements);
void copyArray(int list1[], int src, int list2[],
               int tar, int numOfElements)
{
    for (int index = src; index < src + numOfElements; index++)
    {
        list2[tar] = list1[index];
        tar++;
    }
}
```

## 数组的基地址与计算机内存中的数组

数组的**基地址**是第一个数组分量的地址（即内存位置）。例如，如果 `list` 是一维数组，则 `list` 的基地址是分量 `list[0]` 的地址。

考虑以下语句：

```cpp
int myList[5];       //Line 1
```

此语句将 **myList** 声明为一个包含五个 **int** 类型分量的数组。这些分量是 **myList[0]**、**myList[1]**、**myList[2]**、**myList[3]** 和 **myList[4]**。计算机为这些分量分配五个内存空间，每个空间都足以存储一个 int 值。此外，这五个内存空间是连续的。

数组 **myList** 的基地址是分量 **myList[0]** 的地址。假设数组 **myList** 的基地址是 1000。那么，分量 **myList[0]** 的地址是 1000。通常，为 int 变量分配的内存为四个字节。回顾第 1 章，主存是单元的有序序列，每个单元都有唯一地址。通常，每个单元为一个字节。因此，要将值存储到从地址 1000 开始的 **myList[0]** 中，接下来的四个字节分配给 **myList[0]**。由此可知，**myList[1]** 的起始地址是 1004，**myList[2]** 的起始地址是 1008，依此类推（见图 8-7）。

![](img/b217c421655b51e7494cf3b89bb5432d_587_0.png)

**图 8-7** 数组 *myList* 及其分量的地址

现在 **myList** 是数组的名称。还有一个与标识符 **myList** 关联的内存空间，数组的基地址存储在该内存空间中。考虑以下语句：

```cpp
cout << myList << endl;        //Line 2
```

前面我们说过，此语句不会给出期望的结果。也就是说，此语句不会输出 **myList** 的*分量*的值。事实上，该语句
