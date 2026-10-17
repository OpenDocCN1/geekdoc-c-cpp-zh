
![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_100_0.png)

// 程序 0.5

// 无限读取值并向 vector 添加元素

```cpp
#include <iostream>
#include <vector>
using namespace std;
int main() {
    vector <int> ages;
    int age;
    cout << "输入某人的年龄。输入负数以停止： ";
    cin >> age;
    while (age >= 0) {
        ages.push_back(age);
        cout << "输入另一个年龄。输入负数以停止： ";
        cin >> age;
    }
}
```

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_100_1.png)

# // 测验

- 1. 执行以下每个操作的命令是什么？

对于接下来的2 个问题，请将这些与你在上一节课程等效练习中获得的解决方案进行比较。

- 3. 假设你有一组产品评分，你想找出哪些产品的评分高于平均值。编写一个程序，读取 ID 和评分，直到读到 ID 为 0。

- a. 创建两个并行 `vector`。
- b. 使用整型 `vector` 存储 ID。
- c. 创建一个浮点型 `vector`。
- d. 使用 `push_back` 命令向 `vector` 末尾添加元素。
- e. 使用 `size()` 方法获取 `vector` 的大小。

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc)

# // 测验答案

- 1. 执行以下每个操作的命令是什么？

    - a. `vector<int> v;`
    - b. `vector<int> v;`
    - c. `vector<float> v;`
    - d. `v.push_back(value);`
    - e. `v.size();`

- 3. 假设你有一组产品评分，你想找出哪些产品的评分高于平均值。编写一个程序，读取 ID 和评分，直到读到 ID 为 0。

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> ID;
    vector<float> rating;
    float sumofrings = 0.0;
    int i;
    cout << "输入产品 ID 和对应的评分，输入 ID 为 0 以停止" << endl;
    int id;
    float r;
    cin >> id >> r;
    while (id > 0) {
        ID.push_back(id); // 存储产品 ID
        rating.push_back(r); // 存储评分
        sumofrings += r; // 累加评分
        cin >> id >> r; // 读取下一个产品
    }
    int totalnumber = ID.size();
    float averaging = sumofrings / totalnumber;
    cout << "评分高于平均值的产品有：" << endl;
    for (i = 0; i < totalnumber; i++) {
        if (rating[i] > averaging) {
            cout << ID[i] << endl;
        }
    }
}
```

# 09 用于处理文本的 C++ 字符串

本节内容：

+   - 字符串变量与字面量
- 程序 9_1
- 程序 9_2
- 程序 9_3
- 程序 9_5
+   - 字符串操作
- 程序 9_6
- 程序 9_8
- 程序 9_8_a
+   - 字符类型变量
- 程序 9_9
- ASCII 格表

尽管计算机最初开发是为了主要处理数字，但很快人们发现，表示文本（包括字母和标点符号）同样重要。你已经在许多计数语句中使用过文本进行输出，并且已经见过将文本放在双引号中然后将该文本流到控制台的方法。这种文本——由字母、数字、标点符号、空格等连接在一起的集合——被称为字符串（`string`）。

## // 字符串变量与字面量

到目前为止，你一直在使用字符串字面量——某些类型的指定值。就像你可以使用变量来存储和操作布尔值一样，你也会希望有变量来让你存储和操作字符串。为了做到这一点，你使用了一种新的变量类型——字符串。字符串变量是你使用和操作文本数据的主要方式。

与 `int`、`float` 和 `bool` 不同，字符串不是内置的语言类型。要拥有字符串类型，你需要引入一个新的库，`string` 库。一旦完成引入，你就可以声明字符串变量，就像声明其他类型一样。

将字面量看作是变量的相反。变量可以是特定类型的任何值；而字面量是一个特定的值。

如果你有一个变量 `x` 和一行代码 `x = 5`，那么 `x` 是变量而 `5` 是字面量。如果你将 `3.14` 流向 `cout`，你正在流输出一个浮点值。或者，如果你将 `3.14` 赋值给浮点变量 `f`，那么你正在打印一个变量。

`string` 库是 C++ 标准库之一，因此你可以访问它，使用 `#include <string>`。`string` 中的所有内容都在命名空间中，因此在开头使用 `using namespace std;` 意味着你不需要显式列出命名空间。

最后，你通过 `cout` 输出字符串变量的值，就像你输出字符串字面量一样。

键！但你知道字符串可以包含空格，所以为什么你没有在这里字符串变量中存储完整姓名呢？

程序 9_1 是 `Hello: World` 的一个不同版本。因为你 `#include <string>`，你可以声明类型为 `string` 的变量。在这个示例中，你声明了一个类型为 `string` 的变量 `greeting`。当你赋值时，在这种情况下是字符串 `"Hello, World!"`。

当你运行程序时，你会看到输出 `Hello, World!`，就像你在原始版本中做的那样。

当你将输入流向字符串时，流将获取下一个单个项目并将该项目放入变量中。单个项目由空白符分隔——即空格、制表符和换行符。所以，当你输入 `John Keys` 时，流操作将其视为两个不同的字符串：一个是值为 `Keys` 的字符串。只有第一个字符串 `John` 被流入了变量。

你可以将输入流向字符串，就像你流向输出一样；也就是说，你可以使用 `cin` 从控制台获取输入并流入字符串变量。

程序 9_2 是一个简单的程序。你 `#include <string>` 库，并声明了一个类型为 `string` 的变量 `username`。

# // 程序 9_1

# // 程序 9_2

+   2 声明并打印字符串
+   2 一个问候程序
+   3 `#include <iostream>`
+   3 `#include <iostream>`
+   4 `#include <string>`
+   4 `#include <string>`
+   5 `using namespace std;`
+   5 `using namespace std;`
+   6
+   6
+   7 `int main()`
+   7 `int main()`
+   8
+   8
+   9 `string greeting;`
+   10 `string username;`
+   11 `greeting = "Hello, World!"`
+   11 `cout << "What's your name? ";`
+   12 `cout << endl;`
+   12 `cin >> username;`
+   13 `cout << "Howdy, " << username << "!" << endl;`

通过编写 `What's your name?` 提示用户输入，你可以获取用户的响应到字符串变量中。语法与使用其他变量一样：`cin >> username;`。你可以将字符串作为输出语句的一部分流出，以显示如何使用用户自己的姓名向用户返回 `Howdy`。

如果你运行这段代码并输入 `John`，你会得到消息 `Howdy, John!`——正如你所希望的。

另一方面，如果你输入全名 `John Keys`，你会得到相同的响应：`Howdy, John!`。你不会得到 `Howdy, Keys`。

这个程序的变体旨在处理名和姓。你声明了两个字符串变量：`firstname` 和 `lastname`。你还调整了提示以同时询问名和姓。

然后，你流入两个变量 `firstname` 和 `lastname`。这意味着输入的第一个字符串将进入第一个变量 `firstname`，而输入的下一个字符串将进入第二个变量 `lastname`。

输出语句也发生了变化。注意在流式输出中，你必须显式地在名姓之间输出一个空格；否则它们会在一起。

当你运行程序时，如果你输入名字 `John Keyser`，你会得到完整的问候 `Howdy, John Keyser!`。

```cpp
// 程序 9_3
// 一个处理名和姓的问候程序
#include <iostream>
#include <string>
using namespace std;

int main() {
    string firstname, lastname;
    cout << "What's your name? (Enter first and last name) ";
    cin >> firstname >> lastname;
    cout << "Howdy, " << firstname << " " << lastname << "!" << endl;
}
```

假设你想写一个询问用户姓名或喜好的程序，然后打印出回复。这告诉计算机用户的姓名，并在输出中显示。你可以使用 `cin` 流入数据，但如果你想读取一段较长的文本（例如带有空格和标点符号的句子），`string` 库中有一个名为 `getline` 的函数。

```cpp
// 程序 9_5
// 使用 getline
#include <iostream>
#include <string>
using namespace std;

int main() {
    string username;
    cout << "What is your name? ";
    getline(cin, username);
    cout << "Howdy, " << username << "!" << endl;
}
```

记得你可以通过在线参考 `cplus.com` 查找 `string`。

要使用 `getline`，你调用一个函数：`getline` 后面跟着两个参数：源 `cin` 和变量 `username`。让我们修改 `Hello, World!` 程序使用 `getline`。

在这段代码中，所有的命令与之前相同，除了输入命令。与其从 `cin` 流向 `username`，你而是使用了 `getline` 函数。`getline(cin, username);` 将读取整行输入。

| 练习 2 |
| a) 你如何声明一个名为 `food` 的字符串？ | b) 你如何给该变量赋值 `pizza`？ |
| c) 你如何从输入流入字符串？ |
| d) 你如何将整行读入 `string`？ |
| e) 你如何将该字符串流到输出？ |

如果你运行这个程序并输入 `John Keyser`，输出将包含完整的名字 `Howdy, John Keyser!`

 // 字符串操作

在程序 9_6 中，你有三个字符串——`s1`、`s2` 和 `s3`——并将 `Happy` 赋值给 `s1`，将 `Birthday` 赋值给 `s2`。

这意味着加法操作 `+` 对于两个字符串与对于两个数字不同。`+` 运算符被重载了，这意味着它有多个含义，取决于操作对象的类型。

在程序 9_8 中，你有一个字符串 `s`，将其初始化为 `Happy`。然后你有一行：`s += "Birthday";`。

然后你有 `s3 = s1 + s2;`。换句话说，你正在合并两个字符串以得到第三个字符串。

当你运行时，你会得到一个拼接字符串 `HappyBirthday`，中间没有空格。`Birthday` 被附加到了原始字符串 `Happy` 上。基本上，你获取了字符串的值并在右侧执行了 `+` 操作，将结果放回原始变量。但字符串的 `+` 定义为拼接，所以两个字符串被拼接在一起，结果放在 `s` 中。

如果你运行这个程序，输出 `s3` 会给你一个字符串 `HappyBirthday`，单词之间没有空格。基本上，`s3` 是由第一个字符串 `Happy` 和紧接其字符串 `Birthday` 形成的。这被称为拼接。你拼接了字符串 `s1` 和 `s2` 来形成 `s3`。

运算符重载是定义不同类型行为的常用做法。

> `+` 并不总是意味着加法。

各种运算符的含义取决于它们所操作的对象类型。

在之前程序的另一个变体中，不是字符串 `Happy` 和 `Birthday`，而是给 `s1` 赋值字符串 `"3"`，给 `s2` 赋值字符串 `"4"`。

```cpp
// 程序 9_6
// 相加字符串
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s1, s2, s3;
    s1 = "Happy";
    s2 = "Birthday";
    s3 = s1 + s2;
    cout << s3 << endl;
}
```

当你把两个相加时，输出是 3。为什么？

| 10 | `s1 = "3";` |
| 11 | `s2 = "4";` |
| 12 | `s3 = s1 + s2;` |

```cpp
// 程序 9_8
// 添加字符串
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s = "Happy";
    s += "Birthday";
    cout << s << endl;
}
```

记住 `s1` 和 `s2` 是字符串。赋值给 `s1` 的 `3` 不是数字 3；它是一个内部只有一个单个字符数字 `3` 的字符串。同样，当你加上赋值的 `4` 时，你得到拼接，所以相加 `s1` 和 `s2` 的结果是拼接它们的字符串。结果并不是真正的数字 34；它是字符串 "34"。

所以，当变量是一个字符串时，`+=` 操作与追加（append）相同，因为你只是将新字符串附加到现有字符串的末尾。

这基本上是一个编译器错误，告诉你你不允许将两个字符串字面量相加。

在相加字符串时你会遇到一些意想不到的副作用。在程序 9_8a 中，你有一个字符串，并尝试将 `s` 赋值为两个字符串字面量 Happy Birthday 之和。但出乎意的是，你得到了：

对于通用用途，不允许相加字符串字面量。你可以相加字符串变量，甚至可以将字符串变量和字符串字面量相加。但你不能将两个字符串字面量相加。

```cpp
// Program 9_8_a
// ERROR - cannot add string literals
#include <iostream>
using namespace std;
int main() {
 s = "Happy" + "Birthday";
cout << s << endl;
}
```

## // char 类型变量

字符串本质上是由字符数组或字符向量（`vector`）组成的。字符可以是字母、数字、标点符号或空格等，每个字符都有自己的内置类型。

在 C 语言中，字符串本质上是一个数组。在 C++ 中，虽然底层仍然是数组，但你可以使用许多类似向量选项的字符串。

你不需要 `#include` 任何库即可访问它。该类型是 `char`。

程序 9_9 是一个使用 `char` 类型变量的简单程序。注意，你不需要 `#include` 任何特殊库来使用 `char`；你只需要 `iostream` 就可以输出到控制台。

```cpp
// Program 9_9
// char type
#include <iostream>
using namespace std;
int main() {
char testchar;
testchar = 'a';
cout << testchar << endl;
}
```

在 C 和 C++ 中，字符被单引号（'）括起来，里面只能有一个字符。字符串使用双引号（""）。

注意：单引号和双引号应该是基础的标准引号。如果你使用文字处理软件来编写代码，它经常会“帮助”你将这些更改为弯引号——这些并不是一回事，并且会导致你的程序出错。

你通过编写 `testchar;` 声明了一个类型为 `char` 的变量 `testchar`；你可以给 `testchar` 赋值——在这种情况下赋值为 `a`。当 `testchar` 流向输出时，`a` 会打印到屏幕上。

## # ASCII 表

| DEC | CHAR | DEC | CHAR | DEC | CHAR | DEC | CHAR |
|---|---|---|---|---|---|---|---|
| 0 | NUL (null) | 32 | SPACE | 64 | @ | 96 | ` |
| 1 | SOH (start of heading) | 33 | ! | 65 | A | 97 | a |
| 2 | STX (start of text) | 34 | " | 66 | B | 98 | b |
| 3 | ETX (end of text) | 35 | # | 67 | C | 99 | c |
