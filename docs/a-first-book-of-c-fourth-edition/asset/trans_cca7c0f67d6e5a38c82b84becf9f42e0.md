

+   4. **(Program)** 编写一个程序，将以下数字存储在名为 `miles` 的数组中：15、22、16、18、27、23 和 20。让你的程序将 `miles` 中存储的数据复制到另一个名为 `dist` 的数组中，然后显示 `dist` 数组中的值。你的程序在复制和显示数组元素时应使用指针表示法。

+   5. **(Program)** 编写一个 C++ 程序，将以下字母存储在名为 `message` 的数组中：`This is a test.` 让你的程序将 `message` 中存储的数据复制到另一个名为 `mess2` 的数组中，然后显示 `mess2` 数组中的字母。

+   6. **(Program)** 编写一个程序，声明三个一维数组，分别命名为 `miles`、`gallons` 和 `mpg`。每个数组应能够容纳 10 个元素。在 `miles` 数组中存储数字 240.5、300.0、189.6、310.6、280.7、216.9、199.4、160.3、177.4 和 192.3。在 `gallons` 数组中存储数字 10.3、15.6、8.7、14、16.3、15.7、14.9、10.7、8.3 和 8.4。`mpg` 数组的每个元素应计算为 `miles` 数组的对应元素除以 `gallons` 数组的等效元素；例如，`mpg[0] = miles[0] / gallons[0]`。使用指针计算和显示 `mpg` 数组的元素。

## 8.4 传递地址

在第 6.3 节中，你看到了将地址传递给函数的一种方法：使用引用参数。向函数传递引用是地址的隐式使用，因为引用确实为函数提供了地址。不幸的是，实际的调用语句并不能揭示正在传递的内容——它可能是地址或值。例如，函数调用 `swap(num1,num2);` 并不能揭示 `num1` 或 `num2` 是引用（地址）还是值。只有通过查看变量 num1 和 num2 的声明，或检查 `swap()` 的函数头，才能确定 num1 和 num2 的数据类型。如果它们被定义为引用变量，则会传递地址；否则，会传递变量中存储的值。

与使用引用隐式传递地址不同，地址也可以通过指针显式传递。要显式地将地址传递给函数，只需在传递的变量前加上地址运算符 `&` 即可。例如，此函数调用

```
swap(&firstnum, &secnum);
```

将变量 `firstnum` 和 `secnum` 的地址传递给 `swap()`，如图 8.19 所示。此函数调用还清楚地表明地址正在被传递给函数。

## 程序 8.11

```
```cpp
#include <iostream>
using namespace std;

void swap(double *, double *);   // function prototype
int main()
{
   double firstnum = 20.5, secnum = 6.25;

   swap(&firstnum, &secnum);    // call swap
   return 0;
}

// this function illustrates passing pointer arguments
void swap(double *nm1Addr, double *nm2Addr)
{
   cout << "The number whose address is in nm1Addr is "
        << *nm1Addr << endl;
   cout << "The number whose address is in nm2Addr is "
        << *nm2Addr << endl;
   return;
}
```
```

在回顾程序 8.11 时，请注意两点。首先，`swap()` 的函数原型

`void swap(double *, double *)`

声明 `swap()` 不直接返回值，其参数是两个指向双精度值的指针。当函数被调用时，需要传递两个地址，每个地址都是双精度值的地址。

其次，在 `swap()` 中使用了间接运算符来访问 `firstnum` 和 `secnum` 中存储的值。`swap()` 函数不知道这些变量名，但它确实有 `firstnum` 的地址存储在 `nm1Addr` 中，`secnum` 的地址存储在 `nm2Addr` 中。第一个 cout 语句中的表达式 `*nm1Addr` 的意思是“地址在 nm1Addr 中的变量”。当然，它就是 firstnum 变量。类似地，第二个 cout 语句将 secnum 中存储的值获取为“地址在 nm2Addr 中的变量”。正如输出所示，指针已成功用于允许 `swap()` 访问 `main()` 中的变量。图 8.20 说明了将地址存储在参数中。

## 数组和指针

![](img/202cface8244f523c2641baa2e00d7dd_391_0.png)

在验证 `swap()` 可以访问 `main()` 的局部变量 `firstnum` 和 `secnum` 之后，你现在可以扩展 `swap()` 以交换这些变量中的值。`main()` 的变量 firstnum 和 secnum 中的值可以通过在 `swap()` 中使用第 6.3 节中描述的三步交换算法来互换：

+   1. 将 `firstnum` 的值存储在临时位置中。
+   2. 将 `secnum` 的值存储在 `firstnum` 中。
+   3. 将临时值存储在 `secnum` 中。

使用指针在 `swap()` 中，此算法采用以下形式：

+   1. 通过使用语句 `temp = *nm1Addr;` 将 `nm1Addr` 指向的变量的值存储在临时位置中（见图 8.21）。

![](img/202cface8244f523c2641baa2e00d7dd_391_1.png)

+   2. 使用语句 `*nm1Addr = *nm2Addr;` 将地址在 `nm2Addr` 中的变量的值存储在地址在 `nm1Addr` 中的变量中（见图 8.22）。

![](img/202cface8244f523c2641baa2e00d7dd_392_0.png)

# 图 8.22 间接更改 firstnum 的值

3. 通过使用语句 *nm2Addr = temp; 将临时位置中的值移入地址在 nm2Addr 中的变量（见图 8.23）。

![](img/202cface8244f523c2641baa2e00d7dd_392_1.png)

# 图 8.23 间接更改 secnum 的值

程序 8.12 包含了根据此描述编写的 `swap()` 的最终形式。程序 8.12 的一次示例运行产生了以下输出：

```
The value stored in firstnum is: 20.5
The value stored in secnum is: 6.25

The value stored in firstnum is now: 6.25
The value stored in secnum is now: 20.5
```

## 数组和指针

```
Program 8.12

```cpp
#include <iostream>
using namespace std;

void swap(double *, double *);   // function prototype
int main()
{
    double firstnum = 20.5, secnum = 6.25;

    cout << "The value stored in firstnum is: " << firstnum << endl;
    cout << "The value stored in secnum is: " << secnum << "\n\n";

    swap(&firstnum, &secnum);        // call swap

    cout << "The value stored in firstnum is now: "
         << firstnum << endl;
    cout << "The value stored in secnum is now: "
         << secnum << endl;
    return 0;
}

// this function swaps the values in its two arguments
void swap(double *nm1Addr, double *nm2Addr)
{
    double temp;

    temp = *nm1Addr;       // save firstnum's value
    *nm1Addr = *nm2Addr;   // move secnum's value into firstnum
    *nm2Addr = temp;       // change secnum's value
    return;
}
```
```

正如程序输出所示，`main()` 的变量中存储的值已在 `swap()` 中被修改，这要归功于使用了指针。为了确保你理解，可以将此版本的 `swap()` 与程序 6.10 中使用引用的版本进行比较。使用指针而不是引用的优点是函数调用指定正在使用地址，这是一个提示，表明函数很可能会更改调用函数的变量。使用引用的优点是记法更简单。一般来说，对于 `swap()` 这样的函数，使用指针和引用的记法简便性。传递数组给函数时，编译器会自动传递地址，这就决定了使用指针来存储地址。

## 传递数组

当数组传递给函数时，其地址是实际传递的唯一项目。“地址”是指用于存储数组的第一个位置的地址，如图 8.24 所示。因为为数组保留的第一个位置对应于数组的元素 0，所以“数组的地址”也是元素 0 的地址。

![](img/202cface8244f523c2641baa2e00d7dd_394_0.png)

图 8.24 数组的地址是为数组保留的第一个位置的地址

作为传递数组给函数的具体示例，请检查程序 8.13。在此程序中，nums 数组使用常规数组表示法传递给 findMax() 函数。

## 程序 8.13

```
#include <iostream>
using namespace std;

int findMax(int [], int);   // function prototype
int main()
{
    const int NUMPTS = 5;

    int nums[NUMPTS] = {2, 18, 1, 27, 16};

    cout << "\nThe maximum value is "
         << findMax(nums,NUMPTS) << endl;
    return 0;
}

// this function returns the maximum value in an array of ints
int findMax(int vals[], int numels)
{
    int i, max = vals[0];

    for (i = 1; i < numels; i++)
        if (max < vals[i])
            max = vals[i];
    return max;
}
```

