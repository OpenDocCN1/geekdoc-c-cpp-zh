
这是描述选择语句的方式：`switch`关键字后面跟着括号测试表达式。接下来，在选择语句体（大括号）中有`case`分句。每个`case`分句包含一个与测试表达式进行比较的控制值。分句包含了在匹配时要执行的指令。通常情况下，每个`case`分句都以`break`指令结束。选择语句还可以包含`default`分句（`switch`语句的最后部分）。当没有`case`分句的控制值与测试表达式匹配时，执行`default`分句。

程序位于 2.6。其组织方式如下：

- 我们使用循环语句打印输入数字的提示（范围在 1 到 3 之间）。
- 用户输入的值通过`switch`语句进行测试。
- 根据输入的值，程序打印该数字的名称。

现在让我们考虑代码。

### 列表 2.6. switch 语句

```cpp
#include <iostream>
using namespace std;
int main() {
  // 整数变量：
  int num,k;
  // 循环语句：
  for(k=1;k<=5;k++) {
    cout<<"Enter a number from 1 to 3: ";
    // 获取变量的值：
    cin>>num;
    // 选择语句：
    switch(num){
        case 1:
            cout<<"This is one"<<endl;
            break;
        case 2:
            cout<<"This is two"<<endl;
            break;
        case 3:
            cout<<"This is three"<<endl;
            break;
        default:
            cout<<"I don't know this number"<<endl;
    }
  }
  return 0;
}
```

程序的可能输出如下所示（在此处及下方，用户输入的值已加粗标记）：

| 程序的输出（在列表 2.6 中） |

```
Enter a number from 1 to 3: **2**
This is two
Enter a number from 1 to 3: **-2**
```

# 第 2 章 控制语句

| 我不知道这个数字 |

| 输入一个 1 到 3 之间的数字: 1 |

| 这是一个 |

| 输入一个 1 到 3 之间的数字: 3 |

| 这是三个 |

| 输入一个 1 到 3 之间的数字: 5 |

| 我不知道这个数字 |

循环语句执行了 5 次迭代。在循环语句中，为了打印输入数字的提示，我们使用`cout << "Enter a number from 1 to 3: ";`。用户输入一个数字，该数字被保存在变量`num`中。这是通过语句`cin >> num`实现的。之后是选择语句。它包含了三个控制值为 1、2 和 3 的 case 区域（case sections）和一个默认部分（default section）。每个 case 区域都以`break`指令结束。被测试的表达式是变量`num`的值。如果变量`num`的值等于 1，则执行语句`cout << "This is one" << endl`。如果变量`num`的值等于 2，则执行语句`cout << "This is two" << endl`。变量`num`的值为 3 则意味着执行语句`cout << "This is three" << endl`。

## 注意事项

选择语句的执行方式如下：首先计算被测试表达式的值，然后将该值与 case 区域中的控制值进行比较。此过程一直持续到找到第一个匹配项。如果找到匹配，则执行相应 case 区域中的指令。语句将一直执行到选择语句的结束，或者遇到`break`指令。因此，如果我们希望语句只在单个 case 区域内执行，那么该 case 区域必须以`break`指令结束。

## 控制语句

默认部分包含语句`cout << "I don't know this number" << endl`。只有在测试 case 区域中的控制值时没有发现任何匹配项时，该部分才会“起作用”。

列表 2.7 展示了使用`switch`语句的另一个示例。这个程序与上一个相似，但它有一些特殊之处。特别是，我们生成了随机数，并且选择语句包含了空的 case 区域。

## 理论

为了生成随机数，我们使用`rand()`函数。在程序包含`<cstdlib>`头文件后，可以使用该函数。`rand()`返回一个从 0 到某个上限（该上限足够大）的均匀分布非负整数。如果我们想获取一个范围在`a`到`b`之间的随机数，在这些表达式中，运算符`%`返回整数除法的余数。如果`rand()`是一个随机数，那么表达式`rand() % (b-a+1)`给出了随机数除以数字`b-a+1`的整数除法余数。即从 0 到`b-a`的数字。因此，表达式`a+rand() % (b-a+1)`给出一个在`a`到`b`范围内的（随机）数字。这就是我们需要的。

为了生成随机数，必须向随机数生成器传递一个初始数值。这被称为随机数生成器的初始化。为了执行随机数生成器的初始化，我们使用`srand()`函数。它需要一个数值参数。传递给函数的数字本身没有特殊意义。重要的是`srand()`函数的参数决定了要生成的随机数序列。

我们在下面的程序中实现了这一想法。该程序执行了多次迭代，对于每次迭代，它都会生成一个 2 到 8 范围内的随机数。我们使用`switch`语句根据接收到的值打印消息：

- 对于数字 2、4 和 8，消息包含该数字，并且还说明该数字是 2 的幂（我们指的是 2 = 2^1, 4 = 2^2, 8 = 2^3）；
- 对于数字 3 和 6，消息包含该数字，并且还说明该数字可以被三整除无余数；
- 对于数字 5 和 7，消息包括该数字及其名称。

现在，让我们考虑下面的程序。

## 列表 2.7 使用 switch 语句

```cpp
#include <iostream>
using namespace std;
int main() {
    // 一个整数变量
    int num;
    // 初始化随机数生成器：
    srand(2);
    // 循环语句：
    for(int k=1; k<=10;k++) {
        // 从 2 到 8 的随机数：
        num=2+rand()%7;
        // 选择语句：
        switch(num) {
            case 3:
            case 6:
                cout<<num<<": can be divided by 3" << endl;
                break;
            case 2:
            case 4:
            case 8:
                cout<<num<<": is a power of 2" << endl;
                break;
            case 5:
                cout<<num<<": it is five" << endl;
                break;
            case 7:
                cout<<num<<": it is seven" << endl;
                break;
        }
    }
    return 0;
}
```

程序的输出可能如下（这里我们使用随机数），因此输出可能会发生变化：

## 程序的输出（在列表 2.7 中）

```
5: it is five
7: it is seven
8: is a power of 2
3: can be divided by 3
2: is a power of 2
```

生成随机数时，必须向随机数生成器传递一个初始数值。这被称为随机数生成器的初始化。

随机数2

为了生成随机数，我们使用`rand()`函数。在程序包含`<cstdlib>`头文件后，可以使用该函数。`rand()`返回一个从 0 到某个上限（该上限足够大）的均匀分布非负整数。如果我们想获取一个范围在`a`到`b`之间的随机数，在这些表达式中，运算符`%`返回整数除法的余数。如果`rand()`是一个随机数，那么表达式`rand() % (b-a+1)`给出了随机数除以数字`b-a+1`的整数除法余数。即从 0 到`b-a`的数字。因此，表达式`a+rand() % (b-a+1)`给出一个在`a`到`b`范围内的（随机）数字。这就是我们需要的。

为了生成随机数，必须向随机数生成器传递一个初始数值。这被称为随机数生成器的初始化。为了执行随机数生成器的初始化，我们使用`srand()`函数。它需要一个数值参数。传递给函数的数字本身没有特殊意义。重要的是`srand()`函数的参数决定了要生成的随机数序列。

我们在下面的程序中实现了这一想法。该程序执行了多次迭代，对于每次迭代，它都会生成一个 2 到 8 范围内的随机数。我们使用`switch`语句根据接收到的值打印消息：

- 对于数字 2、4 和 8，消息包含该数字，并且还说明该数字是 2 的幂（我们指的是 2 = 2^1, 4 = 2^2, 8 = 2^3）；
- 对于数字 3 和 6，消息包含该数字，并且还说明该数字可以被三整除无余数；
- 对于数字 5 和 7，消息包括该数字及其名称。

现在，让我们考虑下面的程序。

# 列表 2.7. 使用 switch 语句

```cpp

#include <iostream>

using namespace std;

int main() {

    // 一个整数变量

    int num;

    // 初始化随机数生成器：

    srand(2);

    // 循环语句：

    for(int k=1; k<=10;k++) {

        // 从 2 到 8 的随机数：

        num=2+rand()%7;

        // 选择语句：

        switch(num) {

            case 3:

            case 6:

                cout<<num<<": can be divided by 3" << endl;

                break;

            case 2:

            case 4:

            case 8:

                cout<<num<<": is a power of 2" << endl;

                break;

            case 5:

                cout<<num<<": it is five" << endl;

                break;

            case 7:

                cout<<num<<": it is seven" << endl;

                break;
```
