

int searchArray(int x[], int n)
{
int lcv; //LOOP CONTROL VARIABLE USED TO ACCESS ARRAY ELEMENTS
int index = NOTFOUNDERROR; //VALUE TO RETURN WHICH INDICATES LOCATION OR NOT FOUND
for(lcv = 0; lcv < ARRAYSIZE; lcv++)
{
if(x[lcv] == n)
{
index = lcv;
lcv = ARRAYSIZE;
}
}
return(index);
}

上面定义的用户搜索函数将搜索数组的每个元素，直到发生以下事件之一：

- 找到目标值，循环终止，并返回索引值。
- 到达数组末尾，循环终止，并返回“未找到”值。

int getTarget(void)
{
int target;
do
{
printf("Please enter the target value: ");
scanf("%d", &target);
if(target < 0)
printf("Please enter a valid target value >= 0!\n");
}while(target < 0);
return(target);
}

这种搜索称为**顺序搜索**，因为为了查找所需元素或确定该元素不存在，数组中的每个元素都可能按顺序被引用。

**顺序搜索**算法的优点是什么？

- 它有效！它很简单。

使用顺序搜索算法会有哪些问题？

| 问题 | 答案 |
|---|---|
| 如果我们有一个非常大的数据集，而我们要查找的值不存在怎么办？ | 搜索每个元素并做出此判定需要很长时间。 |
| 如果数组中可能存在多个目标值的实例怎么办？ | 在未排序的数组中，现在必须搜索整个数组才能找到目标的每个实例。 |

## 二分查找

- 可以通过使用一种称为**二分查找**的替代搜索算法来缩短完成搜索所需的时间（包括平均时间和最坏情况时间）。二分查找要求**数组中的数据已排序**。

| 问题 | 答案 |
|---|---|
| 排序数据是否有代价？ | 有，但如果我们频繁搜索数据，支付排序并保持数据处于排序状态的代价是值得的。 |
| 搜索时是否应该始终使用二分查找？ | 不，仅在数据集很大且频繁搜索时才使用。 |

## 二分查找中的新整数变量

- **first** – 此整数将表示在数组中可能找到目标值的最低索引值。
- **last** – 此整数将表示在数组中可能找到目标值的最高索引值。
- **mid** – **first** 和 **last** 变量的平均值将确定在数组中将与目标值进行下一次比较的位置。**mid** 在二分查找过程的每次迭代开始时都会更新。
- **first** 和 **last** 变量何时以及如何更新？当 **mid** 处的值小于目标值时，将 **first** 设置为 **mid** 的值加一。当 **mid** 处的值大于目标值时，将 **last** 设置为 **mid** 的值减一。

## 二分查找示例

假设我们有如下数组，请注意它是已排序的，并且在整个算法过程中都将保持排序状态。搜索算法绝不应更改其搜索的数据！目标值 = 25。

| 3 | 5 | 6 | 10 | 12 | 15 | 17 | 18 | 21 | 22 | 25 | 27 | 30 | 31 | 33 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |

将二分查找应用于上述示例的优点是什么？

- 只需要四次比较即可找到目标值（在上述示例中）。顺序搜索将需要 11 次比较。
- 重点：在目标值与中点处的元素进行每次比较时，我们大约排除一半（因此得名二分）的剩余索引值作为可能找到目标值的位置。

当查找数组中不存在的值时，二分查找与顺序搜索相比如何？

- 顺序搜索需要搜索数组中的每个元素，以确定该值不存在。

让我们看下面的示例，了解二分查找如何处理不存在的值！目标值 = 14。

| 3 | 5 | 6 | 10 | 12 | 15 | 17 | 18 | 21 | 22 | 25 | 27 | 30 | 31 | 33 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |

## **搜索程序 #2** - 要求用户输入目标值，并返回该值在数组中的位置。如果该值不存在，请通知用户。

#define NOTFOUNDERROR -1
#define ARRAYSIZE 15

int binarySearch(int[], int);
int getTarget(void);       //SAME FUNCTION USED IN SEQUENTIAL SEARCH PROGRAM

int main(void)
{
    int array[ARRAYSIZE] = {3, 5, 6, 10, 12, 15, 17, 18, 21, 22, 25, 27, 30, 31, 33};
    int target;            //VALUE WE ARE SEEKING
    int index;             //INDEX VALUE AT WHICH TARGET IS FOUND

    target = getTarget();
    index = binarySearch(array, target);

    if(index == NOTFOUNDERROR)
    {
        printf("Your value %d does not in the array!\n", target);
    }
    else
    {
        printf("Your value %d was found at index %d of the array.\n", target, index);
    }

    return(0);
}

int binarySearch(int x[], int n)
{
 int first = 0; //SMALLEST INDEX VALUE WE ARE CONSIDERING
 int last = ARRAYSIZE - 1; //LARGEST INDEX VALUE WE ARE CONSIDERING
 int mid; //MID POINT INDEX THAT WE ARE CONSIDERING
 int index = NOTFOUNDERROR; //VALUE TO RETURN WHICH INDICATES LOCATION OR NOT FOUND

do
{
 mid = (first + last) / 2;

 if(n > x[mid]) //TARGET GREATER THAN VALUE AT MID -> UPDATE FIRST
 {
 first = mid + 1;
 }
 else if(n < x[mid]) //TARGET LESS THAN VALUE AT MID -> UPDATE LAST
 {
 last = mid - 1;
 }
 else //TARGET HAS BEEN LOCATED IN THE ARRAY
 {
 index = mid;
 last = first - 1; //WHAT DOES THIS DO? WOULD first = last + 1 ALSO WORK?
 }
}while(first <= last);

 return(index);
}

用户定义的搜索函数将搜索数组，直到 `first` 大于 `last`，这将出于以下原因之一发生：

- 找到目标值。
- 数组中不再有可作为搜索候选的元素。

## 多维数组

目前为止我们看到的数组都是一维数组。每个一维数组都是一行索引列值。在考虑可能显著增加内存使用的多维结构之前，必须掌握一维数组的逻辑。

使用多维数组，我们可以添加第二个维度（多行，每行有自己的列）、第三个维度（平面、行和列），以及根据需要添加更多维度。您的唯一限制可能是内存，但很少有问题需要超过三个维度的数组。

无论数组有多少个维度，为数组选择的名称都将继续表示内存中其分配空间开始的位置。我们将看到，当函数将多维数组作为参数时，这需要传递额外信息。

## 声明和定义多维数组

多维数组（与一维数组一样）必须在使用前声明和定义。声明和定义告诉编译器数组每个维度的名称、数据类型和大小或范围。

| 数据类型 | 标识符 | 维度范围 |
|---|---|---|
| int | table | [4][4]; |

## 二维数组：

- 每个维度都是从零开始的。
- 每行和每列的交点表示存储定义类型值的容量。
- 总容量是每个维度范围的乘积。

## 三维数组：

## 四维数组：

问题：计算二维数组中每一行的平均值：

#define ROWS 5
#define COLS 4

void printTable(int[][COLS], float[]);
void calcAvgs(int[][COLS], float[]);

int main(void)
{
    float avgs[ROWS];
    int table[ROWS][COLS] =
    {
        {1, 2, 3, 4},
        {2, 3, 4, 5},
        {3, 4, 5, 6},
        {4, 5, 6, 7},
        {5, 6, 7, 8}
    };

    calcAvgs(table, avgs);
    printTable(table, avgs);

    return (0);
}

