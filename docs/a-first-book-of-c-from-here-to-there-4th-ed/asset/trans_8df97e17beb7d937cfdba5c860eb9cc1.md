

# 信息要点

## 为字符串分配空间

尽管以下两种声明

```
char test[5] = "abcd";
char *test = "abcd";
```

都为字符 'a'、'b'、'c'、'd' 和 '\0' 创建了存储空间，但这两种声明之间以及向 test 赋值的方式上存在细微差别。数组声明（例如 `char test[5];`）会阻止后续使用赋值表达式（例如 `test = "efgh"`）向数组赋值。然而，使用 `strcpy()` 函数（如 `strcpy(test, "efgh")`）是有效的。对 `strcpy()` 的唯一限制是数组大小，在本例中为五个元素。当创建指针时，情况则相反。指针声明（例如 `char *test;`）阻止使用 `strcpy()` 来初始化指针所指向的内存位置，但允许赋值。例如，以下语句序列是有效的：

```
char *test;
test = "abcd";
test = "here is a longer string";
```

这种使用上的差异可以通过以下事实解释：编译器会自动为指针变量所指向的任何 C-字符串分配足够的新内存空间，但不会为字符数组这样做。数组的大小由定义语句固定。

形式上，任何产生可在赋值表达式左侧使用的值的表达式都被称为左值（lvalue）。（类似地，任何产生可在赋值语句右侧使用的值的表达式被称为右值（rvalue）。）因此，指针变量可以是左值，但数组名不能。

![](img/e9bf940282dfb289356f077151cc69dd_713_0.png)

图 15.7 seasons[] 指针中的地址

seasons 数组的初始化也可以合并到数组的定义中，如下所示：

```
char *seasons[4] = {"Winter",
    "Spring",
    "Summer",
    "Fall"};
```

此声明既创建了一个指针数组，又用适当的地址初始化了这些指针。在地址被分配给指针后，每个指针都可以用来访问其对应的字符串。程序 15.8 使用 seasons 数组通过 for 循环显示每个季节。

## 程序 15.8

```
#include <iostream>
using namespace std;
int main()
{
    const int NUMSEASONS = 4;
    int n;
    char *seasons[] = {"Winter",
        "Spring",
        "Summer",
        "Fall"};

    for( n = 0; n < NUMSEASONS; n++)
        cout << "\n\tThe season is " << seasons[n];

    return 0;
}
```

程序 15.8 的输出如下：

```
The season is Winter
The season is Spring
The season is Summer
The season is Fall
```

使用指针列表的优势在于，逻辑上的数据标题组可以被收集起来，并通过一个数组名进行访问。例如，一年中的月份可以分组到一个名为 months 的数组中，一周中的天数可以分组到一个名为 days 的数组中。类似标题的分组使程序员能够通过简单地指定标题在数组中的正确位置来访问和打印相应的标题。程序 15.9 使用 seasons 数组来识别并显示与用户输入的月份相对应的季节。

## 程序 15.9

```
#include <iostream>
using namespace std;
int main()
{
    int n;
    char *seasons[] = {"Winter",
                        "Spring",
                        "Summer",
                        "Fall"};

    cout << "\nEnter a month (use 1 for Jan., 2 for Feb., etc.): ";
    cin >> n;
    n = (n % 12) / 3;  // create the correct subscript
    cout << "The month entered is a " << seasons[n] << " month.";

    return 0;
}
```

除了表达式 `n = (n % 12) / 3` 之外，程序 15.9 相当直接。程序请求用户输入一个月份，并使用 cin 对象接受与月份对应的数字，以显示选定的月份。表达式 `n = (n % 12) / 3` 使用了一种常见的编程“技巧”来将一组数字缩放为更有用的集合。使用下标，seasons 数组的四个元素必须通过 0 到 3 的下标访问。因此，对应于数字 1 到 12 的月份，必须通过使用表达式 `n = (n % 12) / 3` 进行调整，以对应正确的季节下标。表达式 `n % 12` 将用户输入的月份调整到 0 到 11 的范围内，其中 0 对应十二月，1 对应一月，依此类推。除以 3 使结果数字范围在 0 到 3 之间，对应于可能的 seasons 元素。除以 3 的结果被赋给整数变量 n。月份 0、1 和 2 除以 3 后设置为 0；月份 3、4 和 5 设置为 1；月份 6、7 和 8 设置为 2；月份 9、10 和 11 设置为 3。这相当于以下赋值：

| 月份 | 季节 |
|---|---|
| 十二月、一月、二月 | 冬季 |
| 三月、四月、五月 | 春季 |
| 六月、七月、八月 | 夏季 |
| 九月、十月、十一月 | 秋季 |

以下是程序 15.9 的示例输出：

```
Enter a month (use 1 for Jan., 2 for Feb., etc.): 12
The month entered is a Winter month.
```

## 练习 15.3

- 1. （练习）编写两个声明语句，可用于替代声明 `char text[] = "Hooray!";`

- 2. （桌面检查）对于以下每段代码，确定 `*text`、`*(text + 3)` 和 `*(text + 7)` 的值：
  - a. `char *text;`
    `char message[] = "the check is in the mail";`
    `text = message;`
  - b. `char *text;`
    `char formal[] = {'T','h','i','s',' ','i','s',' ','a','n',' ',`
    `'i','n','v','i','t','a','t','i','o','n','\0'};`
    `text = &formal[0];`
  - c. `char *text;`
    `char more[] = "Happy Holidays";`
    `text = &more[4];`
  - d. `char *text, *second;`
    `char blip[] = "The good ship";`
    `second = blip;`
    `text = ++second;`

- 3. （调试）确定以下程序中的错误：

```
#include <iostream>
using namespace std;
int main()
{
    int i = 0;
    char message[] = {'H','e','l','l','o','\0'};
    for( ; i < 5; i++)
    {
        cout << *message;
        message++;
    }
    return 0;
}
```

- 4. （程序）a. 编写一个 C++ 函数，显示与用户输入的 1 到 7 之间数字对应的星期几。也就是说，响应输入 2 时，程序显示名称 Monday。在函数中使用指针数组。
  - b. 将练习 4a 中编写的函数包含在一个完整的可运行程序中。

5. （修改）修改练习 4a 中编写的函数，使其返回包含要显示的正确日期的字符串的地址。

6. （程序）编写一个函数，接受用户输入的 10 行文本，并将它们存储为 10 个 C-字符串。在函数中使用指针数组。

## 15.4 常见编程错误

当使用指向 C-字符串的指针时，经常会出现以下错误：

- 1. 使用指针“指向”不存在的数组元素。当然，这个错误与你在使用下标时已经见过的错误相同。C++ 编译器不对数组执行边界检查，因此程序员有责任确保指针中的地址是有效数据元素的地址。

- 2. 没有为要存储的 C-字符串提供足够的空间。此错误的一个简单变体是，当 C-字符串被定义为字符数组时，没有为字符串结尾的 NULL 字符提供空间，并且在初始化数组时没有包含 '\0' 字符。此错误的一个更复杂的变体是声明一个字符指针，例如 `char *p;`，然后尝试使用诸如 `strcpy(p, "Hello");` 的语句复制 C-字符串。由于没有为 C-字符串分配空间，C-字符串会覆盖 p 所指向的内存区域。

- 3. 误解术语。例如，如果 message 被定义为
  `char *message;`
  变量 message 有时被称为字符串。因此，你可能会看到诸如“将字符 Hooray for the Hoosiers 存储在名为 message 的字符串中”的措辞。严格来说，将 message 称为字符串或 C-字符串变量是不正确的。它是一个指针，包含 C-字符串中第一个字符的地址。然而，将字符指针称为 C-字符串的情况经常发生，你应该对此有所了解。

## 15.5 章节总结

- 1. C-字符串是以 NULL 字符 '\0' 结尾的字符数组。

- 2. C-字符串始终可以使用标准的数组处理技术进行处理。然而，输入和显示 C-字符串始终需要依赖标准库函数。

- 3. cin 对象以及 `cin.get()` 和 `cin.getline()` 函数可用于输入 C-字符串。cin 对象对于 C-字符串输入往往用途有限，因为它在遇到空白时会终止输入。

- 4. cout 对象可用于显示 C-字符串。

- 5. 代替下标，指针表示法和指针算术对于操作 C-字符串元素特别有用。

