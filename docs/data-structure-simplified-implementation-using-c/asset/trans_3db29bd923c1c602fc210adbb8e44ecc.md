
可归类为以下类型：

- 非递归
- 递归

## 1.3.2 非递归

在非递归算法中，我们使用条件语句或循环语句来解决特定问题。这种方法被认为简单，并且被开发人员在编码中广泛使用。调试递归算法简单且需要较少的精力。

```
To find out the sum of n numbers
int sum_array (int x [])
{
int total=0;      //initialize the total to zero
while(x[i])
{
    total=total+x[i]; //add the element with total
    i++;  //go to the next element
}
return total;
}
```

与利用栈来存储/保存其各种状态的递归方法相比，非递归算法的开销更小。然而，有许多实例，使用非递归方法解决问题的复杂性很高，例如在树中遍历、汉诺塔、阶乘等。在这种情况下，应用递归方法会使程序员的生活变得简单。

## 1.3.3 递归方法

一个使用非递归方法解决的问题也可以借助递归方法来解决。在递归算法中，函数在其自身术语中定义。然而，函数包含一个约束，以防止无限地调用自身。例如，考虑一个将数组的所有元素相加的情况。

```
int sum (int x [], int n)// Array element sum, recursively
{
if (n==0)   // base condition
return 0;
return total=sum(x, n-1) +x[n];      //decreasing n
}
```

在上面的示例中，整个问题已在 sum 函数的术语中得到解决。每当我们编写递归方法时，必须包含两个条件，并且已在此提及：

- 基础条件（函数终止的条件）。
- 导致基础条件的后续调用

在上面的程序中，'if n==0' 是基础条件，而 sum(x, n-1) 是导致基础条件的调用。为了实现这一目标，使用表达式 'n-1' 对 'n' 的值进行递减。

## 1.4 复杂度分析

可以应用多种方法来解决一个问题。程序员根据自己的看法和理解来解决这些问题(s)。由于存在多种解决方案，选择能产生最佳性能的解决方案变得极具挑战性。

最优解决方案的选择受多种因素支配，例如，为解决一个问题所需的计算周期、内存空间需求、存储需求等。计算时间最少、内存空间最少的解决方案被认为是最佳解决方案。

根据时间和空间需求选择的算法称为渐近算法。在这种类型的算法中，我们根据最佳或最坏情况计算复杂度。分析是任何算法编写的主要组成部分之一。在最佳情况下，算法可以在几次迭代或甚至一次迭代中解决给定问题。然而，在最坏情况下，它可以在最后一步或倒数第二步解决所考虑的问题。

计算效率的另一种方法称为摊销方法。在摊销方法中，我们不根据最佳或最坏情况计算算法的效率，而是根据平均时间。然而，在渐近中，复杂度效率以以下方式确定：

- 所需的最大时间。
- 所需的最小时间。
- 所需的相等时间。

相应地，它们被归类为下界、上界、等界等。在本书中，我们考虑了大写字母 O，它代表上界。

### 1.4.1 Big-Oh

对于具有 'n' 个数字的函数，Big Oh 可以定义为 f (n) <=c*g (n) 对所有 n, n>=n0 成立；Big (Oh) 充当上界，这意味着它代表最大项的复杂度。然而，算法在实际中可能需要的時間比 Big (O) 所表示的更少。

掌握大写 'O' 复杂度是那些离开数学或记不住许多公式的学生的主要挑战。在大写 Oh 中，主要的复杂度结果是 O (1)、O (n)、O (n2)、O (2n)、O (log n)。本节以非常简单的术语枚举 Big Oh，并提供足够的示例以提供深刻的简单性。

### A. O(1)

Big O (1) 是 Big Oh 记号中其他复杂度中最简单的。O (1) 表示只需要一次比较。在各种场合下，人们观察到程序本身就是单条语句。因此，复杂度结果为 O (1)。在 O (1) 记号中，计算时间始终保持不变。因为该项目已在第一步本身被搜索。例如，考虑以下示例：

```
Problem: To find out the greater between two numbers

// Solution to find out the greater between two numbers
bool max_value (int a, int b) // function that accept two numbers
{

if (a> b)          // Compare the two numbers
return true;       // if first is greater return true
else
return false;     // otherwise return false
}
```

在上面的示例中，只需要一次比较，因此整体性能将保持不变，与任何其他因素无关。所以该算法的复杂度是 O (1)。相应地，复杂度不依赖于元素的数量。

### B. O(n)

O (n) 也称为线性复杂度。在 O (n) 中，我们从第一个元素开始，然后是第二个元素，继续直到达到最后一个元素。到达最后一个元素时，可能会发生要搜索的项目未找到。然而，也可能发生要搜索的项目在第 nᵗʰ 元素之前就已找到，但我们仍将其视为第 nᵗʰ。因此，复杂度表示为 O (n)。以下示例已对此进行了描述。

```
// Program to search a number from a list of numbers
// number is to be searched, n is size //of number
bool search (int arr [], int number, int n)
{

bool found=false;

for (int i=0; i<n; i++)
        {
            if (arr[i] ==number)
            {
found=true;
break;
}      // end of if
}      // end of for
return found;
}      // end of function
```

在上面的示例中，要搜索的元素可能在第一个位置，在这种情况下复杂度将为 O (1)。然而在大多数情况下它将在第二个位置、第三个位置或可能在第 nᵗʰ 位置。然而，我们仍将其复杂度视为 O (n)。

### C. O(n²)

O (n²) 类型的复杂度称为二次复杂度。O (n²) 是由于算法中涉及的嵌套循环而产生的。因此，对于外部循环的第 1ˢᵗ 次迭代，内部循环执行 'n' 次。以下示例已对此进行了描述。

```
Problem: Write a program to sort the series of numbers using Bubble sort

Solution: Bubble sort method to sort the given array

void array (int arr [], int n)
{
int i, j;
for (i=0; i<n; i++)       // start of outer loop
{
    for (j=1; j<n-i; j++)   // inner loop
    {
        if (arr [j+1] > arr[j]) // comparing the elements
        {
                         // swapping if the adjacent is larger
temp=arr [j+1];
arr [j+1] =arr[j];
arr[j] =temp;
        }      // end of if
    }      //end of inner for loop
}      // end of outer for loop
}
```

上面的示例表明，对于外部循环的一次迭代，内部循环执行 'n-i' 次。因此，总迭代次数可以计算为：

n [n-1+n-2+n-3+………..3+2+1].

=n (n+1)/2

=n² [我们认为 'n' 的值很高（这里的高表示 'n' 的值至少为五位数，即 10000），在这种情况下，'n' 的值相对于 n² 可以忽略不计]。

从上面的示例可以明显看出，随着嵌套的增加，'n' 的幂也会增加。考虑一个有三个嵌套循环的情况，相应地该算法的复杂度将为 O (n³)。如果使用四个嵌套循环，则将为 O (n⁴)。

### D. O(2ⁿ)

O (2ⁿ) 类型的复杂度被称为多项式，并且如果连续项是前一项的两倍，则会产生。考虑此处给出的示例：

| 所需步骤数 | 2 | 4 | 8 | 16 | 32 | 64 | 128 | 256 | 512 |

在上面的示例中，我们可以观察到连续项是前一项的两倍。因此，这样的序列的复杂度也将为 2(2ⁿ⁻¹ -1)，即 O (2ⁿ)，考虑到 'n' 的值足够大。

### E. O(log n)

对数类型的复杂度是由于将给定序列分成两半而产生的。随后，从两半中我们只选择一半。所选择的一半进一步分为左右两半。此过程一直持续到将序列分割的目标未完成为止。这种方法也称为分而治之方法。

考虑二分查找，我们遵循上述方法。要解决二分查找，首先我们将通过将数组中下界和上界（最后一个）元素的索引相加来计算 mid。随后，将得到的结果除以 2。这里要搜索的数字与已计算的 mid 元素进行比较。在比较过程中，我们可能会遇到以下可能性。

- 要搜索的项目位于列表的中间位置。
- 中间元素小于要搜索的数字。
- 中间元素大于要搜索的数字。

如果要搜索的数字大于中间元素，在这种情况下我们遵循右半部分，否则我们遵循序列的左半部分。此过程一直持续到数字未找到或序列未耗尽为止。二分查找的算法如下所述：

```
Program: Write an algorithm to search the element from the series by using the binary search techniques.
bool bsearch (b [], n, low, upper) // 'n' is the number to be searched
{
bool found=false;
