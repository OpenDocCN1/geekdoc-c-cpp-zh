

`int *p = numbers;`

```cpp
cout << "Address of the first element is " << p << endl;
```

这行代码的输出是：

第一个元素的地址是 0059F710

要使用指针访问存储在数组第一个元素地址中的值，请运行以下代码行：

```cpp
cout << "The value in the address is " << *p << endl;
```

代码的输出是：

该地址中的值为 1。

要移动到数组的下一个元素，必须增大 p 的值。

```cpp
p++;
```

现在它将指向数组的第二个元素：

```cpp
cout << "Address of the second element is " << p << endl;
```

```cpp
cout << "The value in the address is " << *p << endl;
```

输出是：

我的电脑上 numbers 数组第二个元素的地址是 0059F714

第二个元素的地址中的值为 5。

例如，如果用户输入字符串‘Concatenation’，那么应用程序将输出

‘ConcatenationnoitanetacnoC’

以下头文件必须包含在 main.cpp 文件中：

```cpp
#include "stdafx.h"
#include <stdio.h>
#include <cctype>
#include <iostream>
#include <cstring>
```

字符串函数 `strcpy_s()`、`strcat_s()` 和 `strlen()` 需要 `<cstring>` 头文件。`toupper()` 函数需要 `<cctype>` 头文件。

我想解释一下我是如何按相反顺序将字符从原始字符串复制到临时字符串的。

首先，我使用 `strlen()` 函数获取原始字符串的长度。

```cpp
length = strlen(aWord);
```

然后在循环中，我将原始字符串的最后一个字符复制到临时字符串的第一个位置，依此类推。

让我们检查循环中的代码。

```cpp
for (i = 0; i < length; i++)
    temp[i] = aWord[length - (i + 1)];
```

如果用户输入单词‘Concatenation’，那么单词长度将是 13。字符串中第一个字符的索引是 0，那么字符串最后一个字符的索引将是 12。这意味着最后一个字符的索引是 length - 1。

我在循环中放置的一行代码是

```cpp
temp[i] = aWord[length - (i + 1)];
```

当 i = 0 时，temp[i] 将引用 temp 字符串的第一个字符。

同时（当 i = 0 时），`aWord[length - (i + 1)]` 将引用 `aWord[13 - (0 + 1)]` 字符，也就是 `aWord[12]`，即‘Concatenation’字符串的最后一个字符。

当 i = 1 时，temp[1] 将引用 temp 字符串的第二个字符，而 `aWord[13 - (1 + 1)]` 将引用‘Concatenation’字符串的倒数第二个字符。

通过这种方式，我们可以按相反顺序复制所有字符。

当我们将所有字符从原始字符串复制到 temp 字符串后，需要在 temp 字符串末尾添加空字符（null），因为 C++ 中的字符串必须以空字符结尾。

代码行 `temp[length] = '\0';` 可以完成这项工作。

完整代码包含在 [visual_studio_2017.zip](visual_studio_2017.zip) 中。

```cpp
#include "stdafx.h"
#include <stdio.h>
#include <cctype>
#include <cstring>
#include <iostream>

int main()
{
    char more = 'Y';

    char prompt1[] = "\nEnter a word not more than 20 characters and press enter.\n";

    char prompt3[] = "\nDo you want to continue? Y/N\n";

    char aWord[20];

    char aCopy[40];

    int length = 0;
    char temp[20];
    int i;

    while (toupper(more) == 'Y')
    {
        std::cout << prompt1;
        std::cin >> aWord;
        std::cout << "aWord=" << aWord << std::endl;
        strcpy_s(aCopy, aWord);
        std::cout << "aCopy=" << aCopy << std::endl;
        length = strlen(aWord);
        std::cout << "length=" << length << std::endl;

        // fill temp[] array with the word characters in opposite order.
        for (i = 0; i < length; i++)
            temp[i] = aWord[length - (i + 1)];
        temp[length] = '\0';
        std::cout << "Temp=" << temp << std::endl;
        strcat_s(aCopy, temp);
        std::cout << "aCopy after concatenation of temp=" << aCopy << std::endl;

        std::cout << prompt3;
        std::cin >> more;
    }

    return 0;
}
```

输出：

![](img/ecb1bfa35f80f656f92811abb43b3df7_223_0.png)

图 字符串操作。

## 列表

让我们想象一个谜题。你有一排盒子。每个盒子里都有一张写有一个字母的卡片。你必须找出字母的顺序，使这些字母组成一个单词。

![](img/ecb1bfa35f80f656f92811abb43b3df7_223_1.png)

图 一个链表

在上图中，你可以看到每个盒子都有一个数字。你可能会猜到这些数字是解开谜题的关键。第一个盒子里有一个字母 T，正面有数字 5。取出写有字母 T 的卡片并放在一边。数字 5 可能指向下一个字母。数一数盒子。第五个盒子里有字母‘E’。取出写有‘E’字母的卡片，放在 T 旁边。你会得到“TE”。写有字母‘E’的盒子侧面有数字 2。因此，从第 2 个盒子中取出卡片，放在“TE”旁边。你会得到“TEC”。

写有字母‘C’的盒子有数字 10，所以从第 10 个盒子中取出卡片。你会得到“TECH”。写有字母‘H’的盒子有数字 4，所以从第 4 个盒子中取出卡片。你得到了“TECHN”。继续按照数字操作，你就会得到完整的单词：TECHNOLOGY。

这就是链表的工作方式。它由节点组成。每个节点至少有一个保存数据（文本、数字或对象）的变量，以及一个保存下一个节点地址的变量（指针）。这个系统会像你在谜题中那样遍历节点列表。最后一个节点的指针具有空值，或者它可能指向第一个节点。这时我们就有了一个闭合链表。

### 添加节点

如果要将新节点添加到链表末尾，必须创建一个新节点。然后将最后一个节点的指针指向新节点的地址，并将新节点的指针赋值为空。

![](img/ecb1bfa35f80f656f92811abb43b3df7_224_0.png)

图 在链表末尾添加节点。

如果要将新节点添加到链表开头，必须创建一个新节点。将新节点的指针指向第一个节点，就这样。

![](img/ecb1bfa35f80f656f92811abb43b3df7_224_1.png)

图 在链表头部添加节点。

如果需要在链表中间添加节点，必须创建一个新节点，然后断开链：将（断点之前的）节点重定向到新节点，并将新节点的指针指向下一个节点（断点之后的那个节点）。

![](img/ecb1bfa35f80f656f92811abb43b3df7_224_2.png)

图 在链表中间添加节点。

### 删除节点

要删除具有某个键的节点，需要沿着链表遍历，直到找到该键。然后将该键节点赋值给临时节点。接着将键节点之前的节点指向键节点之后的节点。参见图 60。结果，临时键节点与链表隔离。现在你可以删除该临时节点。

![](img/ecb1bfa35f80f656f92811abb43b3df7_225_0.png)

图 删除节点。

下面是 Node 类的代码。为简单起见，我创建了一个保存整数和指向下一个节点的节点指针的节点。两个类成员变量都声明为 private。不使用全局变量是良好的编程实践，因为私有成员无法从类外部看到。我们仍然需要设置和读取这些私有成员变量。公共函数 set 和 get 可以完成这项工作。

## 第3章：二叉树

二叉树是所有基本数据结构中最有用的一种，也是迄今为止最有趣的。它们是递归和指针如何用于完成一些非常有用事情的完美示例。

创建事物列表的最佳技术之一是链表，但在链表中查找元素可能需要一段时间。而且，如果你有大量非结构化数据，数组也不会有太大帮助。你可以尝试对数组排序，但即便如此，向其中插入项仍然很困难。如果你有一个希望保持有序的数组，插入新元素将需要进行大量搬移！而尽可能快地在列表中查找内容非常重要，尤其是在以下场景中：

- 你正在开发一款 MMORPG 游戏，玩家需要能够快速登录——这涉及快速查找玩家
- 你正在开发处理信用卡的软件，每小时需要处理数百万笔交易——信用卡余额需要被非常快速地查找
- 你正在使用低功耗设备（如平板电脑或智能手机），并向用户显示通讯录。你不会希望用户因为数据结构缓慢而一直等待。

本节将讨论克服这些问题及更多问题所需的工具。

解决方案的思路是能够将元素存储在类似链表的结构中，利用指针来帮助组织内存，但在

