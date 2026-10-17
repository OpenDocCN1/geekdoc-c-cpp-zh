
这主要由于编译器中的二进制转换，以及 IEEE 754 双精度占用 64 位数据，其中 52 位用于二进制格式中的有效数字。

## 科学

| | HYP | F-E | |

| MC | MR | M+ | MS | M- |

| x² | xʸ | sin | cos | tan |

| ✓ | 10⁶ | log | Exp | Mod |

| ↑ | CE | C | ÷ |

| π | 7 | 8 | 9 | × |

| n! | 4 | 5 | 6 | + |

| ± | 1 | 2 | 3 | - |

| ( ) | 0 | = |

```cpp
#include <iostream>
using namespace std;
double PI = 3.14159265358979238463;

int main() {
    cout.precision(22);
    cout << PI;
}
```

![](img/0b5e7d59f3578d974082f03180129000_108_0.png)

```cpp
#include <iostream>
using namespace std;
double PI = 3.14159265358979238463;

int main() {
    cout.precision(22);
    cout << PI;
}
```

```
3.14159265358979238463
Process returned (0) execution time: 0.047 s
Press any key to continue.
```

# 字符串

字符串是表示和持有字符序列的实例。例如，你可以在代码中设置一个通用的问候语 'Welcome' 并将其赋值为字符串，以便在程序的任何地方调用。

## 字符串理论

有多种方法可以创建字符字符串，这些方法在历史上都是继承自原始的 C 语言，并且仍然被 C++ 支持。

- 步骤 1 使用 `char` 函数创建字符串。打开一个新的 C++ 文件并从通常的头文件开始：

```cpp
#include <iostream>
using namespace std;

int main() {

}
```

![](img/0b5e7d59f3578d974082f03180129000_109_0.png)

- 步骤 3 构建并运行代码，屏幕上出现了 'Welcome'。虽然这样做完全可行，但它并不是字符串。字符串是一个类，它定义了可以表示为字符流的对象，并且不需要像数组那样终止。因此，代码可以表示为：

```cpp
#include <iostream>
using namespace std;

int main() {

    char greet[] = "Welcome";
    cout << greet << "\n";
}
```

![](img/0b5e7d59f3578d974082f03180129000_109_1.png)

- 步骤 2 很容易将字符串与数组混淆。这里有一个数组，可以用空字符终止：

```cpp
#include <iostream>
using namespace std;

int main() {

    char greet[8] = {'W', 'e', 'l', 'l', 'c', 'o', 'm', '\0'};
    cout << greet << "\n";

}

```

![](img/0b5e7d59f3578d974082f03180129000_109_2.png)

- 步骤 4 在 C++ 中也有字符串类型，其工作方式相同。再次使用问候语代码，你可以输入：

```cpp
#include <iostream>
using namespace std;

int main() {

    string greet = "Welcome";
    cout << greet << "\n";
}

```

![](img/0b5e7d59f3578d974082f03180129000_109_3.png)

## 字符串操作

步骤 5 你可以对 `string` 类型应用许多不同的操作。例如，要获取字符串的长度，你可以使用：

步骤 8 正如你预期的那样，你可以混合整数并存储与字符串相关的内容。在这里，我们创建了 `int length`，它存储了 `string.size()` 的结果并输出到屏幕：

```cpp
#include <iostream>
using namespace std;
int main() {
    string greet = "Welcome";
    cout << "the length of the string is: " << greet.size() << "\n";
}
```

```cpp
#include <iostream>
using namespace std;
int main() {
    int length;
    string greet1 = "Hello";
    string greet2 = " world!";
    string greet3 = greet1 + greet2;
    length = greet3.size();
    cout << "The length of the combined strings is: " << length << "\n";
}
```

步骤 6 你可以看到我们使用 `string::size()` 来输出长度，即字符串内容中字符的数量。自然地，如果你将字符串名称改为 `other greet`，那么你需要更改命令以反映这一点，这总是简单的操作。构建并运行代码查看结果：

步骤 9 使用 `string` 自带的可用操作，你可以操作字符串的内容。要从字符串中删除字符，你可以使用：

```cpp
#include <iostream>
using namespace std;
int main() {
    string str = "Here is a long sentence in a string";
    cout << str << "\n";
    str.erase(10,5);
    cout << str << "\n";
    str.erase(str.begin(0)+8);
    cout << str << "\n";
    str.erase(str.begin(0)+9, str.end()-9);
    cout << str << "\n";
}
```

步骤 7 `#include <iostream>`

using namespace std;

你可以将字符串相加，或者通过组合移除其他字符串来形成它们：

```cpp
#include <iostream>
using namespace std;
int main() {
    string greet1 = "Hello";
    string greet2 = " world!";
    string greet3 = greet1 + greet2;
    cout << greet3 << "\n";
}
```

```
The length of the string is: 7
Process returned 0x0 execution time : 0.44 s
Press any key to continue.
```

步骤 10 花点时间玩玩数字，这些是字符串中的字符位置。你可以判断是否正确，所以练习一下。看一眼截图中的结果：

```cpp
#include <iostream>
using namespace std;
int main() {
    string greet1 = "Hello";
    string greet2 = " world!";
    string greet3 = greet1 + greet2;
    cout << greet3 << "\n";
}
```

```
The length of the string is: 7
Process returned 0x0 execution time : 0.44 s
Press any key to continue.
```

# C++ 数学

编程本质上是数学性的，正如你预期的，C++ 为数学数学提供了许多内容。对于想要实现模型的人来说，C++ 可以非常复杂，也可以相对简单。

## C++ 数学基础

基础数学符号在 C++ 中的应用与大多数编程语言相同。然而，通过使用 C++ 数学库，你还可以计算平方根、幂。数学操作遵循学校里教的模式，即加法、除法和减法。你可以改变这些。现在创建一个新文件并输入：

```cpp
#include <iostream>
using namespace std;
int main() {
    float numbers = 100;
    numbers = numbers * 10; // 将 100 乘以 10
    cout << numbers << "\n";
    numbers = numbers - 10; // 从总数减去 10
    cout << numbers << "\n";
}
```

- 步骤 3 乘法和除法可以这样应用：

```cpp
#include <iostream>
using namespace std;
int main() {
    float numbers = 100;
    numbers = numbers * 10; // 将 100 乘以 10
    cout << numbers << "\n";
    numbers = numbers / 10; // 将 100 除以 10
    cout << numbers << "\n";
}
```

| | |

|---|---|

| Start | Maths.cpp |

| 1 | #include <iostream> |

| 2 | using namespace std; |

| 3 | int main() { |

| 4 | |

| 5 | float numbers = 100; |

| 6 | numbers = numbers * 10; // 将 100 乘以 10 |

| 7 | cout << numbers << "\n"; |

| 8 | numbers = numbers / 10; // 将 100 除以 10 |

| 9 | cout << numbers << "\n"; |

| 10 | |

| 11 | |

| 12 | |

| 13 | |

| 14 | |

| 15 | |

简单的，它可以正确地更新数学变量。注意我们使用了 `float` 来处理变量。如果你想使用整数，则需要更改 `float` 或 `double`，取决于精度。运行代码查看结果。

```
C:\Users\david\C++\Maths.exe
100
Process returned 0x execution time : 0.43 s
Press any key to continue.
```

- 步骤 4 再次，简单的代码并查看结果。并不是特别有趣，它进入了 C++ 数学。在这里使用了 `float`，所以你可以玩转代码并进行乘除、加减法。

```
C:\Users\david\C++\Maths.exe
100
Process returned 0x0 execution time : 0.50 s
Press any key to continue.
```

## C++ 数学库

步骤 5 当你调用 C++ 数学库时，会出现有趣的数学内容。这个头文件中包含了许多数学函数以及操作。从余弦到正切，你可以调用头文件获取 Pi 的值：

步骤 8 计算数字的幂可以这样做：

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {

}
```

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    float number = 12;
    cout << number << " to the power of 2 is " << pow(number, 2) << "\n";
    cout << number << " to the power of 3 is " << pow(number, 3) << "\n";
    cout << number << " to the power of 8 is " << pow(number, 8) << "\n";
}
```

```
x "Maths.cpp"
Files
1 #include <iostream>
2 #include <cmath>
3 using namespace std;
4
5 int main() {
6
7
8
9
10
```

![](img/0b5e7d59f3578d974082f03180129000_112_0.png)

步骤 6 从生成一个数字的平方根开始：

```cpp
#include <iostream>
#include <cmath>
using namespace std;
```

步骤 9 我们创建了一个 `float` 变量（power），值为 12，现在使用变量计算幂和平方根。例如，第一行的相同值：

```cpp
int main() {
    float number = 134;
    cout << "The square root of " << number << " is: " << sqrt(number) << "\n";
}
```

![](img/0b5e7d59f3578d974082f03180129000_112_1.png)

```cpp
x "Maths.cpp"
Files
1 #include <iostream>
2 #include <cmath>
3 using namespace std;
4
5 int main() {
6 float number = 134;
7 cout << "The square root of " << number << " is: " << sqrt(number) << "\n";
8 }
9
10
```

步骤 10 PI 的值存储在 `cmath` 库中。可以使用 `M_PI` 函数调用。输入 `cout << M_PI;` 你就会得到 3.14159；或者你可以使用：

步骤 7 这里我们创建了一个 `float` 数字，并使用 `sqrt(number)` 函数显示 134 的平方根。构建并运行你的代码，答案是 11.5758。

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    double area, radius = 1.5;
    area = M_PI * radius * radius;
    cout << area << "\n";
}
```

# C++ 输入/输出

![](img/0b5e7d59f3578d974082f03180129000_113_0.png)

当你编写的代码要求用户输入内容，然后使用这些输入来产生用户可见的结果时，会有一种成就感。即使只是简单地询问某人的名字，并显示一条个性化的欢迎消息，这也是一个巨大的飞跃。

接下来的页面将涵盖用户交互、字符字面量、定义常量以及文件输入/输出。所有这些都将帮助你更好地理解 C++ 程序是如何运行的。

| 页码 | 主题 |

| :--- | :--- |

| 116 | 用户交互 |

| 118 | 字符字面量 |

| 120 | 定义常量 |

| 122 | 文件输入/输出 |

![](img/0b5e7d59f3578d974082f03180129000_114_0.png)

# 用户交互

没有什么没有什么比创建一个能对你做出响应的程序更令人满足的。基础的用户交互是任何语言中最常被教授的方面，通过它，你可以做比简单打招呼多多的事情。

## 你好，DAVE

在之前的代码中你已经使用了 `cout`（标准输出流）。现在，你将使用 `cin`（标准输入流）来提示用户响应。

- 步骤 1：任何你想让用户输入到系统内存中的内容，都可以可以被检索和使用。因此，任何输入必须首先声明为一个变量，以便准备好供用户使用。从创建一个带有头文件的 C++ 文件开始。

- 步骤 2：变量的数据类型也与你想要从用户处获得的输入类型匹配。例如，为了询问用户的年龄，你会像这样使用整数：

```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    cout << "What is your age: ";
    cin >> age;
    cout << "You are " << age << " years old.";
}
```

- 步骤 3：`cin` 命令的工作方式与 `cout` 命令相反。第一行 `cout` 使用尖括号所示将"What is your age?"输出到屏幕。`cin` 使用指向相反的尖括号，表示输入。输入被放入整数 `age` 中，并在第二个 `cout` 命令中调用。构建并运行代码。

```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    cout << "What is your age: ";
    cin >> age;
    cout << "You are " << age << " years old.";
}
```

- 步骤 4：如果你在提问，你需要将输入存储为字符串；为了询问用户名字，你会执行：
