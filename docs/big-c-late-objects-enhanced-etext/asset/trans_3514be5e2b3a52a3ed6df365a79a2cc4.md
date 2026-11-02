
空字符串是不包含任何字符的字符串。空字符串字面量写作 `""`。定义

```cpp
string response;
```

与

```cpp
string response = "";
```

的效果相同。

## 2.5.2 字符串拼接

使用 `+` 运算符拼接字符串；也就是说，将它们放在一起以生成一个更长的字符串。

给定两个字符串，例如 `"Harry"` 和 `"Morgan"`，你可以将它们拼接成一个长字符串。结果由第一个字符串中的所有字符后跟第二个字符串中的所有字符组成。在 C++ 中，你使用 `+` 运算符来拼接两个字符串。例如，

```cpp
string fname = "Harry";
string lname = "Morgan";
string name = fname + lname;
```

得到字符串

`"HarryMorgan"`

如果你希望名字和姓氏之间用空格分隔呢？没问题：

```cpp
string name = fname + " " + lname;
```

这条语句拼接了三个字符串：`fname`、字符串字面量 `" "` 和 `lname`。结果是

`"Harry Morgan"`

## 2.5.3 字符串输入

你可以从控制台读取一个字符串：

```cpp
cout << "Please enter your name: ";
string name;
cin >> name;
```

当使用 `>>` 运算符读取字符串时，只有一个单词会被放入字符串变量中。例如，假设用户输入

Harry Morgan

## 2.5.4 字符串函数

`length` 成员函数返回字符串中的字符数。

字符串中字符的数量称为字符串的长度。例如，`"Harry"` 的长度是 5。你可以使用 `length` 函数计算字符串的长度。与 `sqrt` 或 `pow` 函数不同，`length` 函数使用点表示法调用。

## 大语言模型简介

大语言模型（LLM）是一类在海量文本语料库上训练的深度学习模型。它们能够理解和生成类似人类的文本，执行翻译、摘要和问答等任务。

- **规模**：LLM 通常拥有数十亿甚至数万亿个参数。
- **预训练**：模型在多样化的互联网规模数据上进行训练。
- **微调**：模型可以通过监督学习或强化学习来适配特定任务。
- **上下文学习**：LLM 可以在不更新权重的情况下执行新任务。

2017 年推出的 Transformer 架构是大多数现代 LLM 的基础。著名的例子包括 GPT、BERT、T5 和 LLaMA。

![](img/d61019b035dd82beb581604273c0ee6b_92_0.png)

> “语言是思想的服装。” —— 塞缪尔·约翰逊

```python
from transformers import AutoModelForCausalLM, AutoTokenizer

model = AutoModelForCausalLM.from_pretrained("gpt2")
tokenizer = AutoTokenizer.from_pretrained("gpt2")
```

| 模型 | 参数 | 年份 |
|-------|--------|------|
| GPT-2 | 1.5B   | 2019 |
| T5    | 11B    | 2020 |
| GPT-3 | 175B   | 2020 |
| PaLM  | 540B   | 2022 |

下面是一个简单的程序，将上述概念付诸实践。程序会询问你的名字和你另一半的名字，然后打印出你们的首字母。

操作 `first.substr(0, 1)` 会生成一个由单个字符组成的字符串，该字符取自 `first` 的开头。程序对 `second` 也执行相同操作。然后将得到的单字符字符串与字符串字面量 `"&"` 拼接，得到一个长度为 3 的字符串，即首字母缩写字符串。（参见图 4。）

```text
first = R o d o l f o
0 1 2 3 4 5 6

second = S a l l y
0 1 2 3 4

initials = R & S
0 1 2
```

![](img/d61019b035dd82beb581604273c0ee6b_93_0.png)

© Rich Legg/iStockphoto.

*缩写由每个名字的首字母构成。*

### 图4 构建首字母缩写字符串

### sec05/initials.cpp

```cpp
#include <iostream>
#include <string>

using namespace std;

int main()
{
    cout << "Enter your first name: ";
    string first;
    cin >> first;
    cout << "Enter your significant other's first name: ";
    string second;
    cin >> second;
    string initials = first.substr(0, 1)
        + "&" + second.substr(0, 1);
    cout << initials << endl;
    return 0;
}
```

### 程序运行

```text
Enter your first name: Rodolfo
Enter your significant other's first name: Sally
R&S
```

它们并不在其中。一些德国数据处理系统用德语字母替换很少使用的 ASCII 字符：`[\]{}|~` 被替换为 Ä Ö Ü ä ö ü。虽然大多数人没有这些字符也能凑合，但 C++ 程序员显然不能。其他编码方案利用了一个事实：一个字节可以编码 256 个不同的字符，其中只有 128 个由 ASCII 标准化。不幸的是，这类编码存在多种不兼容的标准，导致欧洲计算机用户相当恼火。

许多国家根本不使用罗马文字。俄语、希腊语、希伯来语、阿拉伯语和泰语字母（仅举几例）拥有完全不同的形状。更复杂的是，希伯来语和阿拉伯语是从右向左输入的。这些字母表每种都有 30 到 100 个字母，使用这些字母的国家已经为它们制定了编码标准。

在使用汉字脚本的语言中，情况更加剧烈：中文方言、日语和韩语。汉字不是字母文字，而是表意文字。一个字符代表一个想法或事物。大多数单词由一、二或三个这样的表意文字组成。（已知超过 50,000 个表意文字，其中约 20,000 个在使用中。）因此，需要用两个字节来编码它们。中国、台湾、日本和韩国对它们有不兼容的编码标准。（日语和韩语书写混合使用本土音节文字和汉字表意文字。）

字符编码之间的不一致一直是国际电子通信以及争夺全球市场的软件制造商的主要麻烦。从 1988 年开始，一个由硬件和软件制造商组成的联盟开发了一种统一的 21 位编码方案，称为 Unicode，它能够对世界上几乎所有书面语言的文本进行编码。大约 100,000 个字符已被赋予编码，其中包括超过 70,000 个中文、日文和韩文表意文字。甚至已经消亡的语言，如埃及象形文字，也被纳入 Unicode。

![](img/d61019b035dd82beb581604273c0ee6b_95_0.png)

希伯来语、阿拉伯语和英语

![](img/d61019b035dd82beb581604273c0ee6b_95_1.png)

汉字

## 章节总结

### 在 C++ 中编写变量定义。

- 变量是带有名称的存储位置。
- 定义变量时，通常需要指定初始值。
- 定义变量时，还需要指定其值的类型。
- 对于不能有小数部分的数字，使用 `int` 类型。
- 对于浮点数，使用 `double` 类型。
- 按照惯例，变量名应以小写字母开头。
- 赋值语句将新值存储到变量中，替换先前存储的值。
- 赋值运算符 `=` 并不表示数学上的相等。

![](img/d61019b035dd82beb581604273c0ee6b_95_2.png)

![](img/d61019b035dd82beb581604273c0ee6b_95_3.png)

- c. `s.substr(s.length() / 2, 1)`
- d. `s + t`
- e. `t + s`

### R2.8 找出以下程序中的至少五个编译时错误。

```cpp
#include iostream

int main();
{
cout << "Please enter two numbers:"
cin >> x, y;
cout << "The sum of << x << "and" << y
<< "is:" x + y << endl;
return;
}
```

### R2.9 找出以下程序中的至少四个运行时错误。

```cpp
#include <iostream>

using namespace std;

int main()
{
int total;
int x1;
cout << "Please enter a number: ";
cin >> x1;
total = total + x1;
cout << "Please enter another number: ";
int x2;
cin >> x2;
total = total + x1;
double average = total / 2;
cout << "The average of the two numbers is "
<< average << endl;
return 0;
}
```

### R2.10 解释 `2`、`2.0`、`"2"` 和 `"2.0"` 之间的区别。

### R2.11 解释以下每个程序片段计算什么。

- a.
  `int x = 2;`
  `int y = x + x;`
- b.
  `string s = "2";`
  `string t = s + s + s;`

### R2.12 为以下程序编写伪代码：读取一个单词，然后打印第一个字符、最后一个字符以及中间字符。例如，如果输入是 Harry，程序打印 H y arr。

### R2.13 为以下程序编写伪代码：读取一个姓名（例如 Harold James Morgan），然后打印由名字、中间名和姓氏的首字母组成的缩写（例如 HJM）。

### R2.14 为以下程序编写伪代码：计算一个数字的第一个和最后一个数字。例如，如果输入是 23456，程序应打印出 2 和 6。提示：`%`、`log10`。

