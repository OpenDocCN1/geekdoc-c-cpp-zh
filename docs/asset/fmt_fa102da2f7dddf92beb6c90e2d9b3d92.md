
Team LiB

# 表列表

# 第 2 章：内存和数据类型

- 表 2-1：十进制 1 到 5 的二进制等值
- 表 2-2：整数数据类型、大小和范围
- 表 2-3：浮点数数据类型、大小和范围
- 表 2-4：浮点值的科学计数法和 E 符号表示
- 表 2-5：常用字符的 ASCII 值
- 表 2-6：常用转义序列

# 第 4 章：算术运算符

- 表 4-1：算术运算符
- 表 4-2：算术运算符与赋值运算符的结合
- 表 4-3：算术运算符的优先级
- 表 4-4：优先级演示
- 表 4-5：算术运算符的结合性

## 第 5 章：决策：if 和 switch 语句

- 表 5-1：关系运算符
- 表 5-2：关系表达式及其值
- 表 5-3：关系运算符的优先级
- 表 5-4：选定的 ANSI/ASCII 值

## 第 6 章：嵌套 if 语句和逻辑运算符

- 表 6-1：逻辑运算符
- 表 6-2：逻辑与运算符 (And)
- 表 6-3：逻辑或运算符 (Or)
- 表 6-4：逻辑非运算符 (Not)
- Table 6-5：逻辑与关系运算符的优先级

## 第 12 章：字符、C 字符串和 C++ 字符串类函数

- 表 12-1：检查字符值的函数
- 表 12-2：字符串比较的结果

## 第 13 章：持久化数据：文件输入与输出

- 表 13-1：文件模式标记

![](img/59a3417a6d5906fae6d8000d4c2cff76_362_0.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_362_1.png)

`cin.get(ch);`

![](img/59a3417a6d5906fae6d8000d4c2cff76_363_0.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_364_0.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_365_0.png)

`cin.get(ch);`

值：
`ch`

`\n`

赋值给 `ch` 之前的输入缓冲区

值：
`'n'`
`ch`

输入缓冲区为空

`cin.get(ch);`

调用 `cin.ignore()` 时输入缓冲区为空，因此等待字符以移除

`\n`

第二次按回车键

调用 `cin.ignore()` 移除了输入缓冲区中的换行符

`cin >> courseNum;`

![](img/59a3417a6d5906fae6d8000d4c2cff76_367_0.png)

| 8 | 0 | 2 | '\n' |

![](img/59a3417a6d5906fae6d8000d4c2cff76_367_1.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_367_2.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_367_3.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_367_4.png)

`cin.getline(name, 80);`

![](img/59a3417a6d5906fae6d8000d4c2cff76_367_5.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_367_6.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_367_7.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_367_8.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_367_9.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_368_0.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_369_0.png)

`int testScore[3];`

| 索引 | 偏移量 | 地址 |
| --- | --- | --- |
| 0 | 0 | 101 |
| 1 | 4 | 105 |
| 2 | 8 | 109 |

假设整数类型为 4 字节

```cpp
int main()
{
    sum = addNumbers(firstNum, secondNum);
}
int addNumbers(int x, int y)
{
    return x + y;
}
```
`x+y` 的值赋值给 `sum`
`firstNum` 和 `secondNum` 的值拷贝到 `x` 和 `y`

![](img/59a3417a6d5906fae6d8000d4c2cff76_371_0.png)

```cpp
int main()
{
  ...
  printMessage(str);
  return 0;
}
void printMessage (string s)
{
  cout << "You inputted" << s;
}
```
![](img/59a3417a6d5906fae6d8000d4c2cff76_372_0.png)

```cpp
void printMessage(void) {
    cout << "Hello World";
}
int main() {
    printMessage();
    return 0;
}
```
1. `main` 开始
2. 调用 `printMessage`
3. `printMessage` 执行
4. `main` 结束

img/59a3417a6d5906fae6d8000d4c2cff76_374.png
img/59a3417a6d5906fae6d8000d4c2cff76_375.png
1. 提示
grade 'A'
2. 输入
grade 'B'
3. 显示
grade 'C'
4. 显示
grade 低 60

img/59a3417a6d5906fae6d8000d4c2cff76_377_0.png
img/59a3417a6d5906fae6d8000d4c2cff76_378_0.png
img/59a3417a6d5906fae6d8000d4c2cff76_379_0.png
img/59a3417a6d5906fae6d8000d4c2cff76_379_1.png
img/59a3417a6d5906fae6d8000d4c2cff76_379_2.png
img/59a3417a6d5906fae6d8000d4c2cff76_379_3.png
img/59a3417a6d5906fae6d8000d4c2cff76_379_4.png
img/59a3417a6d5906fae6d8000d4c2cff76_379_5.png
img/59a3417a6d5906fae6d8000d4c2cff76_379_6.png
img/59a3417a6d5906fae6d8000d4c2cff76_379_7.png
img/59a3417a6d5906fae6d8000d4c2cff76_379_8.png
img/59a3417a6d5906fae6d8000d4c2cff76_379_9.png

终端 - 用于程序的开始和结束
显示 - 用于 `cout` 语句
输入 - 用于 `cin`
数据 - 用于赋值
过程 - 用于计算

![](img/59a3417a6d5906fae6d8000d4c2cff76_380_0.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_380_1.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_380_2.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_380_3.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_380_4.png)

# 打开解决方案

查看位置：

HelloWorld

- 调试
- 文件夹设置
- HelloWorld.sln

历史

我的项目

桌面

收藏夹

我的网络位置

文件名：

打开

文件类型：

解决方案文件 (*.sln)

取消

# 添加新建项 - HelloWorld

类别：

模板：

- Visual C++

![](img/59a3417a6d5906fae6d8000d4c2cff76_386_0.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_386_1.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_386_2.png)
![](img/59a3417a6d5906fae6d8000d4c2cff76_386_3.png)
![](img/59a3417a6d5906fae6d8000d4c2ff76_386_4.png)
![](img/59a3417a6d5906fae6d8000d4c2ff76_386_5.png)
![](img/59a3417a6d5906fae6d8000d4c2ff76_386_6.png)
![](img/59a3417a6d5906fae6d8000d4c2ff76_386_7.png)
![](img/59a3417a6d5906fae6d8000d4c2ff76_386_8.png)

创建一个 C++ 源文件。

名称：

hello

位置：

`c:\Documents and Settings\Administrator\PCKLUB866\My Documents\Omh\D`

浏览...

打开

取消

帮助

# 数值

| 11111111 | 11111111 | | | | |
|---|---|---|---|---|---|
| <- 100 | 101 | 102 | 103 | 104 | 105 -> |

内存地址

# 数值

| | 00000000 | 00000000 | 11111111 | 11111111 | | |
|---|---|---|---|---|---|
| <- 100 | 101 | 102 | 103 | 104 | 105 -> |

内存地址

![](img/59a3417a6d5906fae6d8000d4c2ff76_389_0.png)

# 数值

| 00000100 | 10011000 | 01001010 | 00100100 | | | |
|---|---|---|---|---|---|---|
| <- 100 | 101 | 102 | 103 | 104 | 105 -> |

内存地址

# 新项目

项目类型：

- Visual Basic 项目
- Visual C# 项目
- Visual J# 项目
- Visual C++ 项目
  - .NET
  - ATL
  - MFC
  - Win32
  - 常

![](img/59a3417a6d5906fae6d8000d4c2ff76_391_0.png)

Win32 控制台项目
Win32 项目

Win32 项目的控制台应用程序类型。

名称：

HelloWorld

位置：

`C:\Documents and Settings\Administrator\PCKLUB866\My Documents\Demystified\C++\nCh1\Projects\HelloWorld`。

浏览...

项目将在 `C:\...\My Documents\OMH\Demystified\C++\nCh1\Projects\HelloWorld` 创建。

确定

取消

帮助

# Win32 应用程序向导 - HelloWorld

# 欢迎使用 Win32 应用程序向导

此向导生成一个 Win32 应用程序项目。项目可以是 Windows 应用程序、控制台应用程序、DLL 或静态库。

![](img/59a3417a6d5906fae6d8000d4c2ff76_392_0.png)

概述

应用程序设置

这些是当前项目设置：

- 控制台应用程序

从任何窗口点击“完成”以接受当前设置。

创建项目后，请查看项目的 readme.txt 文件以获取有关项目功能和生成文件的信息。

![](img/59a3417a6d5906fae6d8000d4c2ff76_392_1.png)

完成

取消

帮助

# Win32 应用程序向导 - HelloWorld

# 应用程序设置

指定您将用此项目构建的应用程序类型以及想要支持的选项或库。

| 概述 | 应用程序类型： | 为以下添加支持： |
|---|---|---|
| 应用程序设置 | ○ Windows 应用程序 | ☐ ATL |
| | ○ 控制台应用程序 | ☐ MFC |
| | ○ DLL | |
| | ○ 静态库 | |
| | 其它选项： | |
| | ☐ 空项目 | |
| | ☐ 导出符号 | |
| | ☐ 预编译头文件 | |

![](img/59a3417a6d5906fae6d8000d4c2ff76_393_0.png)

![](img/59a3417a6d5906fae6d8000d4c2ff76_394_0.png)

![](img/59a3417a6d5906fae6d8000d4c2ff76_395_0.png)

# 添加新建项 - HelloWorld

类别：

- Visual C++

模板：

| Windows 窗体 (.NET) | C++ 文件 (.cpp) | HTML 页面 (.htm) |
|---|---|---|
| 静态文件 (.rc) | 头文件 (.h) | Midl 文件 (.idl) |
| 资源文件 (.rc) | 响应文件 (.res) | 模块定义文件 (.def) |

创建一个 C++ 源文件。

名称：

hello

位置：

`c:\Documents and Settings\Administrator\PCKLUB866\My Documents\Omh\D`

浏览...

打开

取消

帮助

![](img/59a3417a6d5906fae6d8000d4c2ff76_398_0.png)

# HelloWorld - Microsoft Visual C++ [设计] - hello.cpp

文件 编辑 项目调试窗口帮助

hello.cpp

调试

解决方案 - HelloW...

- 解决方案 'HelloWorld' (1 个)
  - HelloWorld
    - 引用
    - 源文件
      - hello cpp
    - 头文件
    - 资源文件

准备 行 1 列 1 第 1

# HelloWorld - Microsoft Visual C++ [设计]

文件 编辑 项目调试工具窗口帮助

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    cout << "Hello World!";
    return 0;
}
```

- 解决方案 - HelloW...
- 解决方案 'HelloWorld' (1 个项目)
  - HelloWorld
    - 引用
    - 源文件
      - hello cpp
    - 头文件
    - 资源文件

# 任务列表 - 显示 1 个生成错误任务（已过滤）

| | 描述 | 文件 |
|---|---|---|
| 点击此处添加新任务 | | |
|  C2065: 'Cout'：未定义的 c:\...\hello.cpp | | |

- 任务列表 - 输出

# HelloWorld - Microsoft Visual C++ [设计] - hello.cpp

文件 编辑 项目调试工具窗口帮助

hello.cpp

```cpp
#include <iostream>
using namespace std;
int main(void)
{
    Cout << "Hello World!";
    return 0;
}
```

```
Hello World!按任意键继续
```
