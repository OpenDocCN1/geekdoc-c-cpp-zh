

## 2.5.1 string 类型

可以定义用于存储字符串的变量。

```cpp
string name = "Harry";
```

string 类型是 C++ 标准的一部分。要使用它，只需包含头文件 `<string>`：

```cpp
#include <string>
```

我们要区分字符串变量（例如上面定义的变量 name）和字符串字面量（用引号括起来的字符序列，例如 "Harry"）。存储在字符串变量中的字符串可以改变。字符串字面量表示一个特定的字符串，就像数字字面量（例如 2）表示一个特定的数字一样。

与数值变量不同，即使不提供初始值，字符串变量也保证会被初始化。默认情况下，字符串变量会被设为空字符串：即不包含任何字符的字符串。空字符串字面量写作 `""`。下面的定义

```cpp
string response;
```

与下面的定义效果相同：

```cpp
string response = "";
```

## 2.5.2 字符串拼接

> 使用 + 运算符拼接字符串，也就是将字符串连接起来，得到一个更长的字符串。

给定两个字符串，例如 "Harry" 和 "Morgan"，你可以将它们拼接成一个长字符串。结果由第一个字符串中的所有字符，后接第二个字符串中的所有字符组成。在 C++ 中，可以使用 + 运算符拼接两个字符串。例如：

```cpp
string fname = "Harry";
string lname = "Morgan";
string name = fname + lname;
```

结果字符串为：

```cpp
"HarryMorgan"
```

如果你想在名和姓之间加一个空格，该怎么办？很简单：

```cpp
string name = fname + " " + lname;
```

这条语句拼接了三个字符串：fname、字符串字面量 " " 和 lname。结果为：

```cpp
"Harry Morgan"
```

## 2.5.3 字符串输入

你可以从控制台读取一个字符串：

```cpp
cout << "Please enter your name: ";
string name;
cin >> name;
```

如果省略长度，就会获取从给定位置到字符串末尾的所有字符。例如，`greeting.substr(7)` 是字符串 `"world!"`（包括感叹号）。

下面这个简单程序将上述概念付诸实践。程序会询问你的名字以及另一半的名字，然后打印出你们的姓名首字母。操作 `first.substr(0, 1)` 会从 `first` 的开头取出一个字符，组成一个字符串。程序对第二个名字也进行同样的操作。接着，它将得到的两个单字符字符串与字符串字面量 `"&"` 拼接，得到一个长度为 3 的字符串，也就是首字母字符串。（见图 4。）

![](img/23fb3582e93ebc95909e1de029c3d388_86_0.png)

![](img/23fb3582e93ebc95909e1de029c3d388_86_1.png)

**图 4** 构建姓名首字母字符串

*姓名首字母由每个名字的第一个字母组成。*

### ch02/initials.cpp

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

**表 8 字符串操作**

| 语句 | 结果 | 说明 |
|---|---|---|
| `string str = "C";`<br>`str = str + "+";` | `str` 被设为 `"C+"` | 对字符串使用时，`+` 表示拼接。 |
| `string str = "C" + "+";` | **错误** | **错误：**不能拼接两个字符串字面量。 |
| `cout << "Enter name: ";`<br>`cin >> name;`<br>（用户输入：Harry Morgan） | name 包含 "Harry" | `>>` 运算符会将下一个单词放入字符串变量中。 |
| `cout << "Enter name: ";`<br>`cin >> name >> last_name;`<br>（用户输入：Harry Morgan） | name 包含 "Harry"，last_name 包含 "Morgan" | 使用多个 `>>` 运算符可以读取多个单词。 |
| `string greeting = "H & S";`<br>`int n = greeting.length();` | n 被设为 5 | 空格也算作一个字符。 |
| `string str = "Sally";`<br>`string str2 = str.substr(1, 3);` | str2 被设为 "all" | 提取从位置 1 开始、长度为 3 的子串。（初始位置为 0。） |
| `string str = "Sally";`<br>`string str2 = str.substr(1);` | str2 被设为 "ally" | 如果省略长度，则会包含从指定位置到字符串末尾的所有字符。 |
| `string a = str.substr(0, 1);` | a 被设为 str 的首字母 | 提取从位置 0 开始、长度为 1 的子串。 |
| `string b = str.substr(str.length() - 1);` | b 被设为 str 的最后一个字母 | 最后一个字母的位置是 `str.length() - 1`。无需指定长度。 |

![](img/23fb3582e93ebc95909e1de029c3d388_87_0.png)

### 自我检测

- 25. 字符串 `"C++ Program"` 的长度是多少？
- 26. 考虑以下字符串变量：`string str = "C++ Program";` 请给出一个 `substr` 成员函数调用，使其返回子串 `"gram"`。
- 27. 使用字符串拼接，将自我检测 26 中的字符串变量 `str` 转换为 `"C++ Programming"`。
- 28. 以下语句序列会打印什么？`string str = "Harry";` `cout << str.substr(0, 1) + str.substr(str.length() - 1);`
- 29. 给出一条输入语句，用于读取形如 “John Q. Public” 的姓名。

**动手练习** 现在可以尝试本章末尾的这些练习：R2.6、R2.9、P2.12、P2.19。

![](img/23fb3582e93ebc95909e1de029c3d388_88_0.png)

## 趣闻 2.2 国际字母与 Unicode

英语字母表相当简单：大写和小写的 a 到 z。其他欧洲语言则有重音符号和特殊字符。例如，德语有三个所谓的变音字母 ä、ö、ü，以及一个双 s 字符 ß。这些并非可有可无的装饰；如果不使用这些字符，根本无法写出一页德语文字，而德语键盘上也有对应的按键。

![](img/23fb3582e93ebc95909e1de029c3d388_88_1.png)

*德语键盘布局*

这给计算机用户和设计人员带来了一个问题。美国标准字符编码（称为 ASCII，即美国信息交换标准代码）规定了 128 个编码：52 个大小写字母、10 个数字、32 个标点符号，以及 34 个控制字符（例如空格、换行符，以及另外 32 个用于控制打印机和其他设备的字符）。变音字母和双 s 字符并不在其中。一些德国数据处理系统会用德语字母替换不常用的 ASCII 字符：[\]{|}~ 被替换为 ÄÖÜäöüß。大多数人或许可以不用这些字符，但 C++ 程序员肯定不行。其他编码方案则利用一个字节可以编码 256 种不同字符这一事实，而 ASCII 只标准化了其中的 128 种。遗憾的是，这类编码存在多种互不兼容的标准，给欧洲计算机用户带来了一些麻烦。

许多国家根本不使用罗马字母。举例来说，俄语、希腊语、希伯来语、阿拉伯语和泰语字母都有完全不同的形状。更复杂的是，希伯来语和阿拉伯语是从右向左书写的。这些字母体系各有 30 至 100 个字母，使用它们的国家也都制定了相应的编码标准。

![](img/23fb3582e93ebc95909e1de029c3d388_88_2.png)

*希伯来语、阿拉伯语和英语*

使用汉字的语言所面临的情况要复杂得多，包括各种汉语方言、日语和韩语。汉字不是字母文字，而是表意文字。一个字符代表一种概念或事物。大多数词语由一个、两个或三个这样的表意字符组成。（已知的表意文字超过 50,000 个，其中约 20,000 个正在使用。）因此，编码它们需要两个字节。中国大陆、台湾、日本和韩国各自采用了互不兼容的编码标准。（日语和韩语书写中混合使用本民族的音节文字和汉字。）

字符编码之间的不一致，长期以来一直是国际电子通信和争夺全球市场的软件制造商面临的一大麻烦。从 1988 年开始，一批硬件和软件制造商组成的联盟开发了一种统一的 21 位编码方案，称为 Unicode，能够为世界上几乎所有书写语言的文本编码。约 100,000 个字符已被分配编码，其中包括 70,000 多个中日韩表意文字。人们甚至计划为古埃及象形文字等已消亡的语言添加编码。

![](img/23fb3582e93ebc95909e1de029c3d388_88_3.png)

*汉字*

