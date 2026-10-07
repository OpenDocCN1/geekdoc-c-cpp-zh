
为了简单起见，程序 9.5 尝试在独立的且未尝试过的 `try` 块中打开输入输出文件。更通用地说，第二个文件是在嵌套的 `try` 块中打开的；如果在打开时发生异常，则不会尝试打开这个第二个文件。（信息点框解释了如何嵌套 `try` 块）。

在审查程序 9.5 时，请特别此语句：
`while ((ch = inFile.get()) != EOF)`
该语句从输入流中读取值，直到达到 `EOF` 值。只要返回值不等于 `EOF`，值就会写入对象流。表达式 `(ch = inFile.get())` 周围的括号是必要的，确保在与 `EOF` 值比较之前先将值赋值给变量 `ch`。如果没有括号，整个表达式 `ch = inFile.get() != EOF` 将产生操作优先级问题；关系表达式 `inFile.get() != EOF` 将先执行。由于这是一个关系表达式，其结果是根据 `get()` 方法检索的数据得出的布尔真或假值。将此备份赋值给字符变量 `ch` 是跨越赋值运算符的无效转换。

### 信息点

嵌套 Try 块

当涉及多个流时，在各自的 `try` 块中打开每个文件流可以隔离并精确识别是哪个文件导致了异常（如果发生异常的话）。`try` 块是可以嵌套的。例如，程序 9.5 已使用嵌套的 `try` 块重写。请注意，内部 `try` 块的 `catch` 块必须嵌套在与 `try` 块相同的作用范围内：

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib> // needed for exit()
#include <string>
using namespace std;
int main() {
    string fileOne = "info.txt"; // 将文件名放在前面
    string fileTwo = "info.bak";
    char ch;
    ifstream inFile;
    ofstream outFile;
    try { // 此块尝试打开输入文件
        inFile.open(fileOne.c_str());
        if (inFile.fail()) throw fileOne;
        try { // 此块尝试打开输出文件
            // 执行所有文件处理
            // 打开一个基础输出流
            outFile.open(fileTwo.c_str());
            if (outFile.fail()) throw fileTwo;
            while ((ch = inFile.get()) != EOF) {
                outFile.put(ch);
            }
            inFile.close();
            outFile.close();
        } // 结束内部 try 块
        catch (string out) { // 捕获内部 try 块
            cout << "The backup file " << out << " was not successfully opened." << endl;
            exit(1);
        }
    } // 结束外部 try 块
    return 0;
}
```

### 完成基础部分

#### 信息点
嵌套 try 块（续）
```cpp
{
    cout << "The input file " << in
      << " was not successfully opened." << endl
      << " No backup was made." << endl;
  exit(1);
}
cout << "A successful backup of " << fileOne
      << " named " << fileTwo << " was successfully made." << endl;
return 0;
```

1. （复习）列出导致输入异常的两种条件。
2. （复习）列出导致输出异常的两种条件。
3. （复习）如果以写入模式打开现有文件，会发生什么？
4. （修改）修改程序 9.3，使用你选择标识符代替字母。
5. （练习）输入并运行程序 9.4。
6. （调试）确定为什么字符串没有存储（提示：见 6a）。
7. （调试）如果嵌套的 `try` 块不相关，将无法编译。
b. 对字符串必须做哪些额外的更改？

# 练习 9.2

![](img/d5a225ca53b347501e86d72212077531_547_0.png)

## 528 完善基础

**表 9.2** `string` 类构造函数（需要包含头文件 string）

| 构造函数 | 描述 | 示例 |
|---|---|---|
| `string objectName = value` | 创建并初始化一个字符串对象为一个值，该值可以是字符串字面量、之前声明的对象，或包含字符串字面量和字符串对象的表达式 | `string str1 = "Good Morning";` `string str2 = str1;` `string str3 = str1 + str2;` |
| `string objectName(stringValue)` | 产生与前一项相同的初始化方式 | `string str("Hot");` `string str + + " Dog";` |
| `string objectName(str, n)` | 创建并初始化一个字符串对象，其内容为字符串对象 `str` 从索引 `n` 开始的子字符串 | `string str2(2, 5)` 如果 `str2` 包含 `Good Morning`，则 `str1` 变为字符串 `Morning` |
| `string objectName(str, n, p)` | 创建并初始化一个字符串对象，其内容为字符串对象 `str` 从索引 `n` 开始且包含 `p` 个字符的子字符串 | `string str2(2, 5, 2)` 如果 `str2` 包含 `Good Morning`，则 `str1` 变为字符串 `Mo` |
| `string objectName(n, char)` | 创建并初始化一个包含 `n` 个字符 `char` 的字符串对象 | `string str(5, '*')` 这 `str = *****` |
| `string objectName;` | 创建并初始化一个字符串对象表示空字符序列（等同于 `objectName = ""`，因此字符串长度为 0） | `string message;` |

程序 9.6 显示了 `string` 类提供的每个构造函数的示例。

## 第 9 章

### 程序 9.6

```cpp
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string str1; // 一个空字符串
    string str2("Good Morning");
    string str3 = "Hot Dog";
    string str4(str3);
    string str5(str4, 4);
    string str6 = "linear";
    string str7(str6, 3, 3);
    cout << "str1: " << str1 << endl;
    cout << "str2: " << str2 << endl;
    cout << "str3: " << str3 << endl;
    cout << "str4: " << str4 << endl;
    cout << "str5: " << str5 << endl;
    cout << "str6: " << str6 << endl;
    cout << "str7: " << str7 << endl;
    return 0;
}
```
