
```cpp
void hello2() {
    const char str[] = "Hello world!";
    std::cout << str << std::endl;
}
```

```cpp
void hello3() {
    std::cout << "Hello world!" << std::endl;
}
```

```cpp
void hello4() {
    const char *str = "Hello world!";
    std::cout << str << std::endl;
}
```

在第一个函数中，我们将字符串声明为数组并用底层的方法进行初始化。注意结尾的 `'\0'` 终止符，它表示字符串的结束。第二个函数有类似的数组定义，但这次我们使用字符串字面量来初始化数组。在 C++ 中，字符串字面量只是带有隐式 `'\0'` 终止符的 `const char`。第三个函数直接使用字符串字面量并给它一个名称。一旦翻译成机器语言指令，它与前两个函数是相同的。

第四个函数有点不同，因为它不仅创建了一个（匿名）数组，还创建了一个名为 `str` 的指针变量，用于存储数组第一个项的地址。尽管如此，该函数的语义与之前的函数相同，优化型编译器会消除多余的 `str` 变量。

接受 C++ 字符串作为参数的函数通常接受 `char *` 或 `const char *`。这里有一个演示其使用的短程序：

```cpp
#include <ctype>
#include <iostream>
void makeUppercase(char *str) {
    for (int i = 0; str[i] != '\0'; ++i) {
        str[i] = std::toupper(str[i]);
    }
}
```

```cpp
void writeLine(const char *str)
{
    std::cout << str << std::endl;
}
int main(int argc, char *argv[])
{
    for (int i = 1; i < argc; ++i) {
        makeUppercase(argv[i]);
        newLine(argv[i]);
    }
    return 0;
}
```

在 C++ 中，`char` 类型通常持有一个 8 位值。这意味着我们可以很容易在 `char` 中存储 ASCII、ISO 8859-1 (Latin-1) 以及其他 8 位编码字符串，但如果不转换为多字节序列，我们就无法存储任意的 Unicode。Qt 提供了强大的 `QString` 类，它将 Unicode 字符串存储为 16 位 `QChar` 序列，并在内部使用隐式数据共享（写时复制）优化。第 11 章和第 18 章将更详细介绍 `QString`。

# 枚举 (Enumerations)

C++ 拥有枚举功能，用于声明一组命名常量，类似于 C# 和新版本 Java 提供的功能。假设我们想在程序中存储星期几：

```cpp
enum DayOfWeek {
    Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday
};
```

通常，我们将此声明放在头文件中，甚至可以放在类内部。上述声明在冗余性上等同于以下常量定义：

```cpp
const int Sunday = 0;
const int Monday = 1;
const int Tuesday = 2;
const int Wednesday = 3;
const int Thursday = 4;
const int Friday = 5;
const int Saturday = 6;
```

通过使用枚举结构，我们可以稍后声明 `DayOfWeek` 类型的变量或参数，编译器将确保只有来自 `DayOfWeek` 枚举中的值会被赋值给它。例如：

```
DayOfWeek day = Sunday;
```

如果我们不在乎类型安全，也可以这样写：

```
int day = Sunday;
```

注意，要引用 `DayOfWeek` 枚举中的 `Sunday` 常量，我们只需写 `Sunday`，而不是 `DayOfWeek::Sunday`。

默认情况下，编译器从 0 开始为枚举的常量分配连续的整数值。如果我们愿意，可以指定其他值：

```cpp
enum DayOfWeek {
  Sunday = 0,
  Monday = 1,
  Tuesday = 2,
  Wednesday = 3,
  Thursday = 4,
  Friday = 5,
  Saturday = 6
};
```

如果我们没有指定枚举项的值，该项将取前一个项的值加 1。枚举有时用于声明整数常量，在这种情况下我们通常省略枚举名称：

```cpp
enum {
  FirstPort = 1024,
  MaxPorts = 32767
};
```

枚举的另一个用法是表示选项集。考虑一个对话框的例子，带有四个复选框控制搜索算法（通配符、大小敏感、反向、循环）。我们可以用常量为 2 的幂的枚举来表示这些：

```cpp
enum FindAction {
  NoOptions = 0x00000000,
  WildcardSyntax = 0x00000001,
  CaseSensitive = 0x00000002,
  SearchBackward = 0x00000004,
  WrapAround = 0x00000008
};
```

每个选项通常被称为“标志 (flag)”。我们可以使用位运算符 `|=` 来组合这些标志：

```cpp
int options = NoOptions;
if (wildcardSyntaxCheckbox->isChecked())
  options |= WildcardSyntax;
if (caseSensitiveCheckbox->isChecked())
  options |= CaseSensitive;
if (searchBackwardCheckbox->isChecked())
  options |= SearchBackward;
if (wrapAroundCheckbox->isChecked())
  options |= WrapAround;
```
