

# 文件输入介绍

## 示例 2.11 读取文本文件的程序

```cpp
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

int main ()
{
    string firstName, lastName;
    int score;
    fstream inputStream;

    inputStream.open("player.txt");

    inputStream >> score;
    inputStream >> firstName >> lastName;

    cout << "Name " << firstName << " " << lastName << endl;
    cout << "Score: " << score << endl;
    inputStream.close();

    return 0;
}
```

### 示例对话
| 姓名 | 分数 |
| :--- | :--- |
| Gordon Freeman | 100 |

你可能想知道程序是否读取了文件中的所有内容。实现此点的方法是使用流提取运算符：如果读取成功则返回 `true`，失败则返回 `false`。因此，如果我们尝试读取文件末尾之后的内容，它将返回 `false`，我们可以忽略结果。这看起来可能有点奇怪，因为在同一行中，我们既执行了读取操作，又检查了布尔结果。示例 2.12 使用 `while` 循环将 `player.txt` 中的每行数据作为字符串读取并输出。

## 示例 2.12 使用循环读取文本文件（ 2 部分中的第 1 部分）

```cpp
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

int main () {
    string text;
    fstream inputStream;
    inputStream.open("player.txt");

    while (inputStream >> text) {
        // 处理每个单词
    }
    inputStream.close();
    return 0;
}
```

## 示例 2.12 使用循环读取文本文件（ 2 部分中的第 2 部分）
（逻辑延续）

# 第 2 章 控制流

### 自测练习

38. 下面代码本应输出文件中的每个单词，但它无法工作。哪里出了问题？
```cpp
bool moreToRead = true;
while (moreToRead) {
  string text;
  moreToRead = inputStream >> text;
}
```

39. 考虑一个高分文件。第一行是一个整数，存储文件中记录的数量。记录在玩家姓名和玩家分数之间交替。以下是一个名为 `scores.txt` 的示例文件，包含三条记录：
```
Gordon 500
Mario 550
Ivan 385
```
编写代码读取并在同一行输出玩家的姓名和分数。

40. 修改你对自测练习 39 的解决方案，仅输出分数最高玩家的姓名和分数。

## 章总结

- 布尔表达式的求值方式与算术表达式相似。
- C++ 分支语句包括 `if-else` 语句和 `switch` 语句。
- `switch` 语句是一种多分支语句。你可以通过嵌套 `if-else` 语句来形成多分支语句。
- `switch` 语句是实现程序菜单的良好方法。
- C++ 循环语句有 `while`、`do-while` 和 `for` 语句。
- `do-while` 语句至少会执行一次循环体。`while` 语句和 `for` 语句可能会执行零次循环体。
- `for` 循环可以用于实现重复 n 次循环体的指令。
- 循环可以使用 `break` 语句提前结束。循环体的单次可以使用 `continue` 语句提前结束。最好少用 `break` 语句。最好完全避免使用 `continue` 语句，尽管程序员偶尔会使用。
- 输入流可以用于读取文件，其方式与 `cin` 读取键盘类似。

## 自测练习答案

1. a. true。
b. true. 注意表达式 a 和 b 的含义完全相同。因为 `<` 运算符的优先级高于 `&&`，所以不需要括号。然而，括号确实使其更容易读。大多数人认为表达式 a 比表达式 b 更容易。
c. true。

true.
false. 因为第一个子表达式 `count == 1` 为 `false`，你不需要评估第二个子表达式就知道整个表达式为 `false`。因此，x 和 y 的值如何无关。这就是短路求值。
true. 因为第一个子表达式 `count < 10` 为 `true`，你不需要评估第二个子表达式就知道整个表达式为 `true`。因此，x 和 y 的值如何无关。这就是短路求值。
false. 注意表达式 g 包含了子表达式 a。该表达式按照我们对 f 描述的方式进行短路求值。整个表达式 g 等价于：
```
!(true || (x < y)) && true
```
这等价于 `!(true && true)`，进而等价于 `!(true)`，最后等价于最终值 `false`。这个表达式在评估时会产生错误，因为第一个子表达式 `limit/count > 7` 涉及除以零。
true. 因为第一个子表达式 `limit < 20` 为 `true`，你不需要评估第二个子表达式就知道整个表达式为 `true`。因此，第二个子表达式：
```
(limit/count) > 7
```
不会被评估，因此涉及除以零的问题从未被察觉。

