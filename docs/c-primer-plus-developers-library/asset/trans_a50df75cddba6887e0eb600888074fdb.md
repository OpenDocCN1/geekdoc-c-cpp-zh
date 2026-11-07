
```cpp
...;
```

和

```cpp
for (n = lim; n > 0; n--)
    ...;
```

彼此不同吗？

从逻辑上讲，在这两种情况下，使用前缀形式还是后缀形式都没有区别。表达式的值没有被使用，因此唯一的影响是副作用。这里使用这些运算符的表达式是完整表达式，所以递增 x 和递减 n 的副作用保证在程序继续执行下一步之前完成；前缀形式和后缀形式会导致相同的最终结果。

然而，尽管前缀形式和后缀形式之间的选择对程序行为没有影响，但这种选择可能会对执行速度产生微小影响。对于内置类型和现代编译器来说，这似乎不是问题。但 C++ 允许你为类定义这些运算符。在这种情况下，用户定义的前缀函数通过递增一个值然后返回它来工作。但后缀版本的工作方式是先暂存该值的一个副本，递增该值，然后返回暂存的副本。因此，对于类来说，前缀版本比后缀版本效率稍高一些。

简而言之，对于内置类型，使用哪种形式很可能没有区别。对于具有用户定义递增和递减运算符的用户定义类型，前缀形式更高效。

## 递增/递减运算符与指针

递增运算符不仅可以用于基本变量，也可以用于指针。回想一下，对指针使用递增运算符会使其值增加它所指向类型所占的字节数。递增和递减指针也遵循同样的规则：

```cpp
double arr[5] = {21.1, 32.8, 23.4, 45.2, 37.4};
double *pt = arr;  // pt points to arr[0], i.e. to 21.1
++pt;              // pt points to arr[1], i.e. to 32.8
```

你还可以将这些运算符与 * 运算符结合使用，来改变指针所指向的量。将 * 和 ++ 同时应用于指针会引出问题：什么被解引用，什么被递增。这些操作由运算符的位置和优先级决定。前缀递增、前缀递减和解引用运算符都具有相同的优先级，并从右到左结合。后缀递增和后缀递减运算符具有相同的优先级，且高于前缀优先级。这两个运算符从左到右结合。

前缀运算符的从右到左结合规则意味着 *++pt 表示先对 pt 应用 ++（因为 ++ 位于 * 的右侧），然后对 pt 的新值应用 *：

```cpp
double x = *++pt;  // increment pointer, take the value; i.e., arr[2], or 23.4
```

另一方面，`++*pt` 表示先取得 `pt` 所指向的值，然后递增该值：

```cpp
++*pt;      // increment the pointed to value; i.e., change 23.4 to 24.4
```

这里，`pt` 仍然指向 `arr[2]`。

接下来，考虑这种组合：

```cpp
(*pt)++;     // increment pointed-to value
```

括号表明首先解引用指针，得到 `24.4`。然后 `++` 运算符将该值递增为 `25.4`；`pt` 仍然指向 `arr[2]`。

最后，考虑这种组合：

```cpp
x = *pt++;     // dereference original location, then increment pointer
```

后缀 `++` 运算符具有更高的优先级，这意味着 `++` 运算符作用于 `pt`，而不是作用于 `*pt`，因此指针被递增。但使用后缀运算符这一事实意味着被解引用的地址是原来的地址 `&arr[2]`，而不是新地址。因此，`*pt++` 的值是 `arr[2]`，即 `25.4`，但语句完成后 `pt` 的值是 `arr[3]` 的地址。

> **注意**
> 
> 递增和递减指针遵循指针算术规则。因此，如果 `pt` 指向数组的第一个成员，`++pt` 会改变 `pt`，使其指向第二个成员。

## 组合赋值运算符

程序清单 5.5 使用以下表达式更新循环计数器：

```cpp
i = i + by;
```

C++ 有一个组合加法和赋值运算符，可以更简洁地完成相同结果：

```cpp
i += by;
```

`+=` 运算符将其两个操作数的值相加，并将结果赋给左侧的操作数。这意味着左操作数必须是可以赋值的东西，例如变量、数组元素、结构成员，或通过解引用指针所标识的数据：

```cpp
int k = 5;
k += 3;                 // ok, k set to 8
int *pa = new int[10];   // pa points to pa[0]
pa[4] = 12;
pa[4] += 6;              // ok, pa[4] set to 18
*(pa + 4) += 7;          // ok, pa[4] set to 25
pa += 2;                 // ok, pa points to the former pa[2]
34 += 10;                 // quite wrong
```

每个算术运算符都有一个对应的赋值运算符，如表 5.1 所总结。每个运算符的工作方式类似于 `+=`。因此，例如，以下语句将 k 的当前值替换为增大 10 倍的值：

```cpp
k *= 10;
```

**表 5.1. 组合赋值运算符**

| 运算符 | 效果（L=左操作数，R=右操作数） |
|---|---|
| `+=` | 将 L + R 赋给 L |
| `-=` | 将 L - R 赋给 L |
| `*=` | 将 L * R 赋给 L |
| `/=` | 将 L / R 赋给 L |
| `%=` | 将 L % R 赋给 L |

## 复合语句，或块

编写 C++ `for` 语句的格式或语法对你来说可能显得限制较多，因为循环体必须是单条语句。如果你希望循环体包含多条语句，这会很别扭。幸运的是，C++ 提供了一个语法漏洞，你可以借此把任意多条语句塞进循环体。技巧是使用成对的花括号构造复合语句，或称块。块由成对的花括号及其包含的语句组成，并且出于语法目的，它算作单条语句。例如，程序清单 5.8 使用花括号将三条独立语句组合成一个块。这使循环体能够提示用户、读取输入并执行计算。该程序计算你所输入数字的累计和，这为使用 `+=` 运算符提供了自然的场合。

程序清单 5.8  **block.cpp**

```cpp
// block.cpp -- use a block statement
#include <iostream>
int main()
{
    using namespace std;
    cout << "The Amazing Accounto will sum and average ";
    cout << "five numbers for you.\n";
    cout << "Please enter five values:\n";
    double number;
    double sum = 0.0;
    for (int i = 1; i <= 5; i++)
    {
        // block starts here
        cout << "Value " << i << " is: ";
        cin >> number;
        sum += number;
    }                                  // block ends here
    cout << "Five exquisite choices indeed! ";
    cout << "They sum to " << sum << endl;
    cout << "and average to " << sum / 5 << ".\n";
    cout << "The Amazing Accounto bids you adieu!\n";
    return 0;
}
```

以下是程序清单 5.8 中程序的一次示例运行：

```
The Amazing Accounto will sum and average five numbers for you.
Please enter five values:
Value 1: 1942
Value 2: 1948
Value 3: 1957
Value 4: 1974
Value 5: 1980
Five exquisite choices indeed! They sum to 9801
and average to 1960.2.
The Amazing Accounto bids you adieu!
```

假设你保留缩进但省略花括号：

```cpp
for (int i = 1; i <= 5; i++)
    cout << "Value " << i << ": ";       // loop ends here
    cin >> number;                       // after the loop
    sum += number;
cout << "Five exquisite choices indeed! ";
```

编译器忽略缩进，因此只有第一条语句会位于循环中。这样，循环将打印五个提示，然后不再做其他事情。循环完成后，程序转到接下来的行，只读取并求和一个数字。

复合语句还有另一个有趣的特性。如果在块内定义一个新变量，该变量只在程序执行块内语句期间存在。当执行离开该块时，变量会被释放。这意味着该变量只在块内已知：

```cpp
#include <iostream>
int main()
{
    using namespace std;
    int x = 20;
    {
        int y = 100;          // block starts
        cout << x << endl;    // ok
        cout << y << endl;    // ok
    }                         // block ends
    cout << x << endl;        // ok
    cout << y << endl;        // invalid, won't compile
    return 0;
}
```
