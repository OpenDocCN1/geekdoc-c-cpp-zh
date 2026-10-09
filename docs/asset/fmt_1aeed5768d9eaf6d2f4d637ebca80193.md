
```cpp
#include <iostream> // 程序将在屏幕上显示一些文本
using namespace std; // 将使用标准标识符 cout 和 endl

int main() {
    // 不同的前景颜色
    cout << "\e[31m RED" << endl;
    cout << "\e[32m GREEN" << endl;
    cout << "\e[33m YELLOW" << endl;
    cout << "\e[34m BLUE" << endl;
    cout << "\e[35m MAGENTA" << endl;
    cout << "\e[0m DEFAULT (USUAL) TEXT" << endl;

    // 不同的背景颜色
    cout << "\e[41m White on red" << endl;
    cout << "\e[42m White on green" << endl;

    // 正常与加粗
    cout << "\e[0m Normal text." << endl;
    cout << "\e[1m BOLD TEXT - super chunky!" << endl;

    // 重置所有为正常
    cout << "\e[0m Back to things again." << endl;

    return 0;
}
```

遗憾的是，黄色的转义代码在 Pi 上通常看起来像棕色。可以使用更长的转义序列获得更亮的黄色，允许更宽的颜色范围：

```cpp
cout << "\e[38;52m BRIGHT YELLOW!" << endl;
```

参见附录中的“控制屏幕颜色的转义序列”章节以获取更多代码。

第 4 章：键盘输入与屏幕输出 | 99

## 使用 `sleep()` 逐个显示屏幕输出

下面的程序使用 `sleep()` 逐个显示不同行文本的颜色。`\e` 字符告诉屏幕它正要使用一组特殊的代码序列来改变任何后续文本的外观。

例如：

```cpp
cout << "\e[31m TOMATO" << endl;
```

上述行将使用红色文本在屏幕上显示 TOMATO 单词，而不是终端的默认颜色。这是因为该字面量值开头包含一个转义序列。

`\e` 标记新转义序列的开始。`[` 符号告诉显示器改变颜色。代码 `31m` 代表前景颜色红色，它将用于在屏幕上显示的后续每一行。

- 示例 4.13 - `display_colours.cpp`

```cpp
#include <iostream> // 程序将在屏幕上显示一些文本
using namespace std; // 将使用标准标识符 cout 和 endl

int main() {
    // 不同的前景颜色
    cout << "\e[31m RED" << endl;
    cout << "\e[32m GREEN" << endl;
    cout << "\e[33m YELLOW" << endl;
    cout << "\e[34m BLUE" << endl;
    cout << "\e[35m MAGENTA" << endl;
    cout << "\e[0m DEFAULT (USUAL) TEXT" << endl;

    // 不同的背景颜色
    cout << "\e[41m White on red" << endl;
    cout << "\e[42m White on green" << endl;

    // 正常与加粗
    cout << "\e[0m Normal text." << endl;
    cout << "\e[1m BOLD TEXT - super chunky!" << endl;

    // 重置所有为正常
    cout << "\e[0m Back to things again." << endl;

    return 0;
}
```

`\t` 字符会创建一个水平间隙，在屏幕上显示任何后续字符之前，向右移动。（记住："tab"一词是"tabulated"的缩写，意思是“制成表格”。）

## 示例 4.10 - `tab_char.cpp`

```cpp
#include <iostream>      // 程序将在屏幕上显示一些文本
#include <unistd.h>       // 使用 sleep() 函数暂停 1 秒

using namespace std;      // 将使用标准标识符 cout 和 endl

int main()
{
    cout << "3..." << flush;
    sleep(1);

    cout << "\t2..." << flush;
    sleep(1);

    cout << "\t1..." << flush;
    sleep(1);

    cout << "\tGO!" << endl;

    return 0;
}
```

## 垂直制表符字符

`\v` 垂直制表符会将光标垂直向下移动一行，但在屏幕上显示任何后续字符之前，会保持在当前的水平位置：

## 示例 4.11 - `vertical_tab.cpp`

```cpp
#include <iostream>      // 程序将在屏幕上显示一些文本
using namespace std;      // 将使用标准标识符 cout 和 endl

int main()
{
    cout << "\H\vE\vL\vP\vV!" << endl;

    return 0;
}
```

你可以在显示每个字母后看到使用垂直制表符的效果：

![](img/0c86cf81300257fe2415e40f8fb03508_100_0.png)

第 4 章：键盘输入与屏幕输出 | 99

## 使用 `\` 反斜杠字符显示字面量字符

这里是一个在显示多个字面量文本值时使用 `\\` 双反斜杠字符的示例：

## 示例 4.12 – `slash_char.cpp`

```cpp
#include <iostream> // 程序将在屏幕上显示一些文本
using namespace std; // 将使用标准标识符 cout 和 endl
int main() {
	cout << " " << endl; // 显示 3 行空行

	cout << "/\\" << endl;
	cout << "\|\"" << endl;
	cout << "\\._/" << endl;
	cout << "\\" << endl;

	cout << endl << endl << endl; // 再显示 3 行空行

	return 0;
}
```

当你运行程序时，你应该能看到这张图片：

![](img/0c86cf81300257fe2415e40f8fb03508_101_0.png)

为了生成小牛的图片，两行代码使用了 `\\` 双反斜杠来在屏幕上显示单个的 `\` 反斜杠字符：

```cpp
cout << "/\\"" << endl;
cout << "\\.\\/" << endl;
```

这就像是在说：

> “这里有一个要显示的特殊字符，它是一个反斜杠。”

注意，单独的一个反斜杠本身不会这样显示，相反，它将指示预期将有一个后续的特殊字符。你不会在屏幕上看到显示的反斜杠符号。

## 显示不同颜色文本的转义序列

下面的程序使用 `\escape-sequences` 改变不同行文本的颜色。`\e` 字符告诉屏幕它正要使用一组特殊的代码序列来改变任何后续文本的外观。

例如：

```cpp
cout << "\e[31m TOMATO" << endl;
```

上述行将使用红色文本在屏幕上显示 TOMATO 单词，而不是终端的默认颜色。这是因为该字面量值开头包含一个转义序列。

`\e` 标记新转义序列的开始。`[` 符号告诉显示器改变颜色。代码 `31m` 代表前景颜色红色，它将用于在屏幕上显示的后续每一行。

- 示例 4.13 - `display_colours.cpp`

```cpp
#include <iostream> // 程序将在屏幕上显示一些文本
using namespace std; // 将使用标准标识符 cout 和 endl

int main() {
    // 不同的前景颜色
    cout << "\e[31m RED" << endl;
    cout << "\e[32m GREEN" << endl;
    cout << "\e[33m YELLOW" << endl;
    cout << "\e[34m BLUE" << endl;
    cout << "\e[35m MAGENTA" << endl;
    cout << "\e[0m DEFAULT (USUAL) TEXT" << endl;

    // 不同的背景颜色
    cout << "\e[41m White on red" << endl;
    cout << "\e[42m White on green" << endl;

    // 正常与加粗
    cout << "\e[0m Normal text." << endl;
    cout << "\e[1m BOLD TEXT - super chunky!" << endl;

    // 重置所有为正常
    cout << "\e[0m Back to things again." << endl;

    return 0;
}
```

遗憾的是，黄色的转义代码在 Pi 上通常看起来像棕色。可以使用更长的转义序列获得更亮的黄色，允许更宽的颜色范围：

```cpp
cout << "\e[38;52m BRIGHT YELLOW!" << endl;
```

参见附录中的“控制屏幕颜色的转义序列”章节以获取更多代码。
