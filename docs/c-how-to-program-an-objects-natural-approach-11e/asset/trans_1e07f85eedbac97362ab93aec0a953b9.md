

### 检查点

- 1. *(代码)* 编写一条 using 指令，使你可以使用 `cin` 和 `cout` 而无需 `std::` 限定。
  
  **答案：** `using namespace std;`

- 2. *(代码)* 假设 `number1` 为 12，`number2` 为 23。以下代码会输出什么？

  ```cpp
  if (number1 > number2) {
      cout << number1 << " > " << number2 << "\n";
  }
  ```

  **答案：** 该语句不会输出任何内容，因为条件为假，所以语句体将被跳过。

- 3. *(代码)* 假设 `number1` 为 23，`number2` 为 23。以下代码会输出什么？[编写并运行一个简短程序，看看这段代码实际做了什么。]

  ```cpp
  if (number1 != number2); {
      cout << number1 << " != " << number2 << "\n";
  }
  ```

  **答案：** 这段代码会错误地输出 23 != 23，因为一个分号被错误地放在了 if 语句条件之后。

## 2.8 对象自然案例研究：创建和使用标准库类 string 的对象

在整本书中，我们强调使用 C++ 标准库和 C++ 开源社区中的各种库中宝贵的既有类。你将专注于了解有哪些库可供使用，为你的应用选择合适的库，从现有库类创建对象，并让这些对象发挥其能力。所谓“对象自然”（Objects Natural），我们的意思是，即使在你于第 9 章学习创建自己的自定义类之前，你也能够方便地创建功能强大的对象并使用它们进行编程。

你已经使用过 C++ 对象——具体来说，`cout` 和 `cin` 对象分别封装了输出和输入的机制。这些对象是在幕后使用 `<iostream>` 头文件中的类为你创建的。在本节中，你将创建并操作 C++ 标准库 `string`<sup>3</sup> 类的对象。

### 测试驱动 string 类

类不能自行执行。一个 `Person` 对象可以通过告诉 `Car` 对象做什么（加速、减速、左转、右转等）来“驾驶”它，而无需了解汽车内部机制如何工作。类似地，`main` 函数可以通过调用 `string` 对象的成员函数来“驱动”它，而无需了解该类是如何实现的。在这个意义上，下面程序中的 `main` 被称为驱动程序。图 2.6 的 `main` 函数测试驱动了几个 `string` 对象。

```cpp
// fig02_06.cpp
// Standard library string class test program.
#include <iostream>
#include <string>
using namespace std;

int main() {
   string s1{"happy"};
   string s2{"birthday"};
   string s3; // creates an empty string

   // display the strings and show their lengths
   cout << "s1: \"" << s1 << "\", length: " << s1.length()
      << "\ns2: \"" << s2 << "\", length: " << s2.length()
      << "\ns3: \"" << s3 << "\", length: " << s3.length();

   // compare strings with == and !=
   cout << "\n\nThe results of comparing s2 and s1:" << boolalpha
      << "\ns2 == s1: " << (s2 == s1)
      << "\ns2 != s1: " << (s2 != s1);

   // test string member function empty
   cout << "\n\nTesting s3.empty():\n";

   if (s3.empty()) {
      cout << "s3 is empty; assigning to s3;\n";
      s3 = s1 + s2; // assign s3 the result of concatenating s1 and s2
      cout << "s3: \"" << s3 << "\"\n";
   }

   // testing new C++20 string member functions
   cout << "\n\ns1 starts with \"ha\": " << s1.starts_with("ha") << "\n";
   cout << "s2 starts with \"ha\": " << s2.starts_with("ha") << "\n";
   cout << "s1 ends with \"ay\": " << s1.ends_with("ay") << "\n";
   cout << "s2 ends with \"ay\": " << s2.ends_with("ay") << "\n";
}
```

```text
s1: "happy", length: 5
s2: "birthday", length: 9
s3: "", length: 0

The results of comparing s2 and s1:
s2 == s1: false
s2 != s1: true

Testing s3.empty():
s3 is empty; assigning to s3;
s3: "happy birthday"

s1 starts with "ha": true
s2 starts with "ha": false
s1 ends with "ay": false
s2 ends with "ay": true
```

**图 2.6** | 标准库 string 类测试程序。

### 实例化对象

通常，除非你创建了某个类的对象⁴——也称为实例化对象——否则不能调用该类的成员函数。第 8–10 行创建了三个 `string` 对象：

- `s1` 用字符串字面量 `"happy"` 的副本初始化；
- `s2` 用字符串字面量 `"birthday"` 的副本初始化；
- `s3` 默认初始化为空字符串（即 `""`）。

当我们像之前那样声明 `int` 变量时，编译器知道 `int` 是什么——它是 C++ 内置的基本类型。然而，在第 8–10 行中，编译器不会预先知道 `string` 是什么类型——它是来自 C++ 标准库的类类型。

如果封装得当，类可以被其他程序员重用。这是使用像 C++ 这样支持面向对象编程的语言最重要的好处之一。这类语言拥有丰富的、功能强大的预建类库。例如，你可以通过包含适当的头文件——在本例中是 `<string>` 头文件（第 4 行）——在任何程序中重用 C++ 标准库中的类。名称 `string` 和名称 `cout` 一样，属于命名空间 `std`。

### string 成员函数 length

第 13–15 行输出每个字符串及其长度。`string` 类的 `length` 成员函数返回特定 `string` 对象中存储的字符数。在第 13 行中，表达式

```cpp
s1.length()
```

通过调用对象的 `length` 成员函数返回 `s1` 的长度。要为特定对象调用此成员函数，你需要指定对象名（`s1`），后跟点运算符（`.`），再跟成员函数名（`length`）和一组圆括号。空括号表示 `length` 无需额外信息即可执行其任务。很快你将看到，某些成员函数需要称之为实参的额外信息来执行任务。

从 `main` 的角度来看，当调用 `length` 成员函数时：

- 1. 程序将执行从调用处（`main` 中的第 13 行）转移到成员函数 `length`。由于 `length` 是通过 `s1` 对象调用的，`length` “知道”要操作哪个对象的数据。
- 2. 接着，成员函数 `length` 执行其任务——也就是，将 `s1` 的长度返回到第 13 行调用处。`main` 函数不知道 `length` 如何执行其任务，就像汽车驾驶员不知道发动机、变速箱、转向机构和刹车是如何实现的一样。
- 3. `cout` 对象显示成员函数 `length` 返回的字符数，然后程序继续执行，显示字符串 `s2` 和 `s3` 及其长度。

⁴ 在第 9.20 节中你将看到，可以不创建类的对象就调用类的静态成员函数。

### 使用相等运算符比较 string 对象

与数字一样，字符串之间也可以相互比较。第 18–20 行使用相等运算符将 `s2` 与 `s1` 进行比较——字符串比较是区分大小写的。⁵

通常，当你输出条件的值时，C++ 对于 false 显示 0，对于 true 显示 1。来自 `<iostream>` 头文件的流操纵符 `boolalpha`（第 18 行）告诉输出流更自然地以单词 `false` 或 `true` 显示条件值。

### string 成员函数 empty

第 25 行调用 string 成员函数 `empty`，如果字符串为空——即字符串长度为 0——则返回 `true`，否则 `empty` 返回 `false`。对象 `s3` “默认”初始化为空字符串，所以它确实是空的，`if` 语句体将执行。

### string 连接与赋值

第 27 行使用 `+` 运算符“相加”字符串 `s1` 和 `s2`，将产生的新值赋给 `s3`——这称为字符串连接。赋值后，`s3` 包含 `s1` 的字符后跟 `s2` 的字符——“happy birthday”。第 28 行输出 `s3`，以证明赋值操作正确完成。

### C++20 string 成员函数 `starts_with` 和 `ends_with`

第 32–35 行演示了 C++20 的 string 成员函数 `starts_with` 和 `ends_with`，它们分别在该字符串以指定子字符串开头或结尾时返回 `true`；否则返回 `false`。第 32 和 33 行显示 `s1` 以 `"ha"` 开头，但 `s2` 不是。第 34 和 35 行显示 `s1` 不以 `"ay"` 结尾，但 `s2` 以 `"ay"` 结尾。

![](img/7b5e2088e71c7f78681d4ddbcf104c06_144_0.png)

### 检查点

- 1. *(代码)* 假设 string 对象 `name` 存在并已初始化。编写一个 string 成员函数调用，如果 `name` 以 `"Je"` 开头，则返回 `true`。
  
  **答案：** `name.starts_with("Je")`

- 2. *(代码)* 假设 string 对象 `name` 存在并已初始化。编写一个 string 成员函数调用，如果 `name` 以 `"on"` 结尾，则返回 `true`。
  
  **答案：** `name.ends_with("on")`

## 2.9 小结

在本章中，我们介绍了许多重要的 C++ 特性，包括在屏幕上显示数据、从键盘输入数据以及声明基本类型的变量。你学习了使用输出流对象 `cout` 和输入流对象 `cin` 来构建简单的交互式程序。我们声明并初始化变量，使用算术运算符执行计算。我们讨论了 C++ 应用运算符的顺序（即运算符优先级规则），以及运算符的分组方式（也称为运算符的结合性）。你看到了 C++ 的 `if` 语句如何让程序进行决策。我们引入了相等运算符和关系运算符，并用它们在 `if` 语句中形成条件。

⁵ 在第 8 章中，你将看到字符串使用每个字符串中字符的数值进行“字典序”比较。

