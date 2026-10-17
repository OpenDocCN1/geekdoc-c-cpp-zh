
```cpp
    return 0;
}

// 使用 iostream。

void getNumbers(int &input1, int &input2) {

    using namespace std;

    cout << "Enter integers: ";

    cin >> input1

    >> input2;

}

void swapValues(int &variable1, int &variable2) {

    int temp;

    temp = variable1;

    variable1 = variable2;

    variable2 = temp;

}

// 使用 iostream。

void showResults(int output1, int output2) {

    using namespace std;

    cout << "In reverse order the numbers are: "

    << output1 << " " << output2 << endl;

}
```

### 示例对话

| 输入两个整数：5 10 |
| 数字的倒序排列为：10 5 |

## 第 5 章 / 适用于所有子任务的函数

变量 `firstNum` 和 `secondNum` 的值通过此函数调用设置。之后，接下来的函数调用反转了变量 `firstNum` 和 `secondNum` 中的值：

```cpp
swapValues(firstNum, secondNum);
```

在接下来的章节中，我们将更详细地描述引用传递机制，并解释显示 5.4 中使用的特定函数。

## 详细了解引用传递

在大多数情况下，引用传递机制的作用方式就像是将作为函数参数的变量名字面上直接替换为引用传递的形式参数。然而，这个过程比这要微妙得多。在某些情况下，这种微妙性非常重要，我们需要检查这种引用传递替换过程的更多细节。

编译器为每个变量分配一个内存位置。例如，编译显示 5.4 中的程序时，变量 `firstNum` 可能会被分配到位置 1010，而变量 `secondNum` 可能会被分配到 1012。为了本示例，请假设这些变量存储在这些内存位置上。换句话说，在执行以下行之后

```cpp
int firstNum = 0, secondNum = 0;
```

值 0 被存储在内存位置 1010 和 1012 中。下图中箭头指向变量所引用的内存位置。

| 内存位置 | 值 | |
|---|---|---|
| ... | | |
| 1008 | | |
| 1010 | 0 | firstNum |
| 1012 | 0 | secondNum |
| 1014 | | |

接下来，考虑显示 5.4 中的以下函数声明：

```cpp
void getNumbers(int& input1, int& input2);
```

引用传递的形式参数 `input1` 和 `input2` 是函数调用中使用的实际参数的占位符。

## 5.2 引用传递参数

## 引用传递

要使形式参数变为引用，请在其类型名称后添加连接符 `&`。那么在对函数的调用时，对应的参数应该是一个变量，而不是常量或其他表达式。当函数被调用时，对应的变量参数（而不是它的值）将替换形式参数。在函数体中对形式参数所做的任何更改都将在函数调用时应用到参数变量上。替换机制的准确细节在本章的正文中给出。

函数声明中引用传递参数的示例：

```cpp
void getData(int firstIn, double& secondIn);
```

现在考虑来自同一显示内容的如下函数：`getNumbers(firstNum, secondNum);`

当函数执行时，函数并没有获得存储在 `firstNum` 和 `secondNum` 中的值。相反，它获得的是与每个名称关联的内存位置。在这个示例中，这些位置是

- 1010
- 1012

这些按顺序分配给参数变量 `firstNum` 和 `secondNum` 的位置。正是这些内存位置与形式参数相关联。第一个内存位置与第一个形式参数关联，第二个内存位置与第二个形式参数关联，依此类推。在我们的示例中，`input1` 是第一个参数，所以它获得了与 `firstNum` 相同的内存位置。

| 内存位置 | 值 | |
|---|---|---|
| ... | | |
| 1008 | | |
| 1010 | 0 | firstNum |
| 1012 | 0 | secondNum |
| 1014 | | |

## 第 5 章 / 适用于所有子任务的函数

当函数退出时，变量 `input1` 和 `input2` 离开了作用范围并丢失了。这意味着我们不能再通过这些变量检索数据 1010 和 1012。

看起来引用传递机制在此调用中工作原理细节似乎在显示 5.5 中描述了。然而，如果内存位置 1010 处的变量是 `firstNumber`，为什么我们坚持说“内存位置 1010 处的变量”而不是简单地说 `firstNum` 呢？如果参数和形式参数包含某些名称上的巧合，就需要这种额外的细节级别。例如，你想修改显示 5.4 中的程序，使其使用带有同名参数的函数 `getNumbers`，并且假设你想做一些不那么明显的操作。

## 5.2 引用传递参数

## 显示 5.5 引用传递参数的行为（部分 1，共 2）

来自 5.4 的函数调用解剖
引用使用

- 0 假设编译器为 `firstNum` 和 `secondNum` 分配了以下地址：
`firstNum 1010`
`secondNum 1012`

（我们不知道分配了哪些地址，结果将取决于实际地址，但这将过程非常具体，从而更容易理解。）

- 1 在显示 5.4 的程序中，执行了以下函数调用：
`getNumbers(firstNum, secondNum);`

- 2 告诉函数使用变量 `firstNum` 的内存位置替换形式参数 `input1`，并使用 `secondNum` 的内存位置替换形式参数 `input2`。其效果相当于函数定义被重写为如下（这不符合 C++ 代码，但对我们来说意义清晰）：
`void getNumbers(int& <the variable at memory location 1010,`
`int& <the variable at memory location 1012>)`
`{`
`namespace std;`
`cout << "Enter integers: ";`
` >> <the variable at memory location 1010;`
`>> <the variable at memory location 1012>`
`}`

显示 5.4 函数调用解剖（续）

由于位置 1010 和 1012 处的变量是 `firstNum` 和 `secondNum`，其效果相当于函数定义被重写为如下：

```cpp
void getNumbers(int& firstNum, int& secondNum)
{
    namespace std;
    cout << "Enter integers: ";
    cin >> firstNum
    >> secondNum;
}
```

- 3 执行函数体。其效果相当于执行了以下内容：

（继续）

```cpp
{
  using namespace std;
  cout << "Enter two integers: ";
  cin >> firstNum;
  cin >> secondNum;
}
```

- 当执行 `cin` 语句时，变量 `firstNum` 和 `secondNum` 的值被设置为键盘输入的值。（如果对话如显示 5.4 所示，`firstNum` 的值设置为 5，`secondNum` 的值设置为 10。）

- 当函数结束时，变量 `firstNum` 和 `secondNum` 返回它们在函数体中由 `cin` 语句赋予的值。（如果对话如显示 5.4 所示，在函数调用结束时，`firstNum` 的值为 5，`secondNum` 的值为 10。）

...input2，以及要存储在名为 `input1` 变量中的第二个数字——也许因为第二个数字会被先处理，或者因为它是更重要的数字。现在，假设在程序主部分声明的变量 `input1` 和 `input2` 已经被分配了内存地址 1014 和 1016。函数的调用方式如下：

```cpp
int input1, input2;
getNumbers(input2, input1);
```

> 注意参数的顺序

在这种情况下，如果你说 "input1"，我们并不知道名为 `input1` 的变量是在程序主部分声明的，还是作为形式参数 `input1`。然而，如果在程序主部分声明的变量 `input1` 被分配了内存地址 1014，那么“内存地址 1014 处的变量”这个短语就是没有歧义的。让我们来看这种情况下替换机制的细节。

在此次调用中，对应形式参数 `input1` 的参数是变量 `input2`，而对应形式参数 `input2` 的参数是变量 `input1`。这可能会让人困惑，但对计算机来说完全没有问题，因为计算机从未真正执行过“用 `input2` 替换 `input1`”或“用 `input1` 替换 `input2`”。计算机仅仅处理内存地址。计算机用“内存地址 1016 处的变量”替换形式参数 `input1`，并用“内存地址 1014 处的变量”替换形式参数 `input2`。

## 5.2 引用传递参数

### 编程示例 swapValues 函数

在显示 5.4 中定义的 `swapValues` 函数交换两个变量中存储的值。该函数的描述由以下声明及附带的注释给出：

```cpp
void swapValues(int& variable1, int& variable2);
// 交换 variable1 和 variable2 的值。
```

为了查看该函数预期的工作方式，假设 `firstNum` 的值为 5，变量 `secondNum` 的值为 10，并考虑以下函数调用：

```cpp
swapValues(firstNum, secondNum);
```

此调用之后，`firstNum` 的值将变为 10，`secondNum` 的值将变为。

如显示 5.4 所示，函数 `swapValues` 的定义使用了局部变量 `temp`。这个局部变量是必不可少的。你可能会认为函数定义可以简化为以下形式：

```cpp
void swapValues(int variable1, int& variable2)
{
  variable1 = variable2;
  variable2 = variable1;
}
```

![](img/67be1289808bc3852827f7f3e32e9d82_296_0.png)

为了证明这种替代定义无法工作，请考虑在此定义和函数调用发生时：

```cpp
swapValues(firstNum, secondNum);
```

变量 `firstNum` 和 `secondNum` 被替换为形式参数 `variable1` 和 `variable2`，因此使用这个错误的函数定义，该调用等同于：

```cpp
firstNum = secondNum;
secondNum = firstNum;
```

这段代码没有产生预期的结果。`firstNum` 的值被设置为 `secondNum` 的值，这本是正确的，但随后 `secondNum` 的值被设置为 `firstNum` 的值（此时 `firstNum` 已经变成了 `secondNum` 的值），导致两个变量都变成了相同的值。

如显示 5.4 所示，函数 `swapValues` 的定义使用了局部变量 `temp`。这个局部变量是必不可少的。你可能会认为函数定义可以简化为以下形式：

```cpp
void swapValues(int variable1, int& variable2)
{
  variable1 = variable2;
  variable2 = variable1;
}
```

### 参数与实

参数和实的区别可能会让人困惑。然而，如果你记住以下几点，就能轻松地处理它们：

- 形式参数定义在函数头中，而参数是传递给函数的值。
- 当调用函数时，参数替换了形式参数。
- 在值传递（call-by-value）中，形式参数是参数的副本。
- 在引用传递（call-by-reference）中，形式参数是参数的别名，因此对参数的操作会影响原始变量。

### 混合参数列表

在同一个函数中混合值传递和引用传递是完全合法的。例如，第一个和最后一个参数是引用，而中间的是值传递：

```cpp
void goodStuff(int &par1, int par2, double &par3);
```

### 返回值

引用传递参数不仅限于 `void` 函数。你也可以在返回值的函数中使用它们。因此，带有引用传递参数的函数可以更改参数的值。

### 编程提示 使用何种类型的参数

显示 5.6 展示了编译器如何处理值传递和引用传递参数的区别。参数 `parValue` 和 `parRef` 在函数体内都被赋予了值。但由于它们是不同类型的参数，效果是不同的。

`parValue` 是值传递参数，因此是一个局部变量。当如下调用函数时：

```cpp
doStuff(n1, n2);
```

局部变量 `parValue` 初始化为 `n1` 的值。也就是说，`parValue` 初始化为 1，而函数忽略了 `n1`。从示例对话中可以看到，形式参数 `parValue`（作为一个局部变量）在函数体内被设置为 1，这个值被输出到屏幕上。然而，参数 `n1` 的值并没有改变。

### 显示 5.6 比较参数机制（1/2 部分）

```cpp
// 展示值传递参数与引用传递
// 参数的区别。
#include <iostream>
void doStuff(int parValue, int &parRef);
// parValue 是值传递形式参数，
// parRef 是引用传递形式参数。
int main() {
    using namespace std;
    int n1 = 1;
    int n2 = 2;
    doStuff(n1, n2);
    cout << "函数调用后 n1 = " << n1 << endl;
    cout << "函数调用后 n2 = " << n2 << endl;
    return 0;
}
void doStuff(int parValue, int &parRef) {
    using namespace std;
    parValue = 10;
    parRef = 20;
    cout << "parValue: " << parValue << endl;
    cout << "parRef: " << parRef << endl;
}
```

# 302 第 5 章 / 用于所有子任务函数

## 显示 5.6 比较参数机制（部分 2/2）

```cpp
parValue = 111;
cout << "parValue in function call = "
<< parValue << endl;
par2Ref = 222;
cout << "par2Ref in function call = "
<< par2Ref << endl;
```

### 示例对话

parValue in function call = 111
par2Ref in function call = 222
n1 after function call = 1
n2 after function call = 222

另一方面，par2Ref 是一个按引用传递的参数。当调用函数时，变量参数 n2（而不仅仅是它的值）被替换为形式参数 par2Ref。因此，当执行以下代码时：

```cpp
par2Ref = 222;
```

它等同于执行了以下代码：

```cpp
n2 = 222;
```
