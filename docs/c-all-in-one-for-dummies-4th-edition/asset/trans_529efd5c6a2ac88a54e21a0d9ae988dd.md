

### 清单6-10：编写一个函数的两个版本

```cpp
#include <iostream>

using namespace std;

void Combine(string first, string second)
{
    cout << first << " " << second << endl;
}

void Combine(int first, int second)
{
    int sum = first + second;
    cout << first << " " << second << " " << sum << endl;
}

int main()
{
    Combine("David","Letterman");
    Combine(15,20);
    return 0;
}
```

你会看到每个函数都在 `main()` 中被调用。编译器根据你提供的参数来决定调用哪个函数。例如，看到这个调用时：

```cpp
Combine("David","Letterman");
```

你会看到两个字符串。因此，编译器知道要使用第一个版本，它接受两个字符串。现在看看第二个函数调用：

```cpp
Combine(15,20);
```

这个调用接受两个整数，因此编译器知道要使用函数的第二个版本。

![](img/128ab511de4e7360e167e3b15cdd5dd0_181_0.png)

> **记住**
>
> 重载函数时，参数必须不同（或者必须按不同顺序出现）。例如，函数可以接受相同类型的信息，但使用不同数量的参数。当然，前面的例子表明，参数也可以因类型不同而不同。你也可以使用不同的返回类型，但函数之间的差异不能仅限于返回类型，而且改变参数名也不算数。编译器会将 `Combine(string A, string B)` 和 `Combine(string First, string Second)` 视为同一个函数。

## 调用所有字符串函数

要想充分发挥字符串的作用，你需要使用一些专门针对字符串的特殊函数。不过，使用这些函数与本章目前使用的其他函数略有不同。你不能直接调用函数，而是先输入保存字符串的变量名，然后输入一个句点（或*点号*），再输入函数名以及任何参数。

![](img/128ab511de4e7360e167e3b15cdd5dd0_182_0.png)

你之所以用不同的方式编写字符串函数，是因为你利用了某些面向对象的编程特性。第2册第1章详细描述了这些类型的函数（称为*方法*）是如何工作的。接下来的几节将介绍一些常见的函数，并告诉你如何使用它们。

### 在字符串中插入字符串

你可以使用的一个函数是 `insert()`。如果你想向另一个字符串中插入更多字符，就可以使用这个函数。例如，如果你有字符串 "Something interesting and bizarre"，并且将字符串 "seriously "（末尾带一个空格）从索引10开始插入其中间，你会得到字符串 "Something seriously interesting and bizarre"。

![](img/128ab511de4e7360e167e3b15cdd5dd0_182_1.png)

处理字符串时，第一个字符是第0个索引，第二个字符是第1个索引，依此类推。下面几行代码使用 `insert()` 函数在索引10处执行插入，尽管你实际上是在第11个字符处进行插入：

```cpp
string words = "Something interesting and bizarre";
words.insert(10, "seriously ");
```

第一行代码只是创建了一个名为 words 的字符串，并用短语 "Something interesting and bizarre" 将其填满。第二行执行插入操作。注意调用函数的奇怪方式：你先指定变量名 words，然后是一个点，然后是函数名 insert。接下来，像往常一样在括号中加上参数。对于这个函数，第一个参数是要插入字符串的索引，第二个参数是你要插入的实际字符串。当这两行代码运行后，名为 words 的字符串变量将包含 "Something seriously interesting and bizarre"。

### 删除字符串的一部分

你还可以使用一个类似的函数 `erase()` 来删除字符串的一部分。下面这行代码从索引19开始删除 words 字符串中的16个字符：

```cpp
words.erase(19,16);
```

因此，如果名为 words 的变量包含字符串 "Something seriously interesting and bizarre"，那么在这一行运行之后，它将包含 "Something seriously bizarre"。

### 替换字符串的一部分

另一个有用的函数是 `replace()`。这个函数用另一个字符串替换字符串的某一部分。使用 replace 时，你要指定在字符串中开始替换的位置以及要替换的字符数，然后指定要用哪个字符串来替换旧的、磨损的部分。

例如，如果你的字符串是 "Something seriously bizarre"，你想用字符串 "body" 替换单词 "thing"，你可以告诉 `replace()` 从索引4开始，用 "body" 替换5个字符。为此，你输入：

```cpp
words.replace(4, 5, "body");
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_183_0.png)

请注意，你要替换的字符数不必与新字符串的长度相同。如果字符串最初是 "Something seriously bizarre"，在这次 `replace()` 调用之后，字符串将包含 "Somebody seriously bizarre"。

### 结合使用字符串函数

清单6-11中的 OperatingOnStrings 示例演示了所有这些函数协同工作的情况。

### 清单6-11：对字符串进行操作

```cpp
#include <iostream>

using namespace std;

int main()
{
    string words = "Something interesting and bizarre";
    cout << words << endl;
    words.insert(10, "seriously ");
    cout << words << endl;
    words.erase(19,16);
    cout << words << endl;
    words.replace(4, 5, "body");
    cout << words << endl;
    return 0;
}
```

当你运行这个应用程序时，会看到以下输出：

```text
Something interesting and bizarre
Something seriously interesting and bizarre
Something seriously bizarre
Somebody seriously bizarre
```

第一行是原始字符串。第二行是 `insert()` 函数的结果。第三行是 `erase()` 函数的结果。最后一行是 `replace()` 函数的结果。

### 理解 main()

到目前为止，本章中的所有应用程序都有一个 `main()`，它是一个函数。注意它的头部，后面是花括号内的代码：

```cpp
int main()
```

你可以看到这绝对是一个函数头部：它以返回类型开头，然后是函数名 `main()`。这只是 `main()` 函数的一种形式——Code::Blocks 默认使用的形式。然而，你可能决定让用户在控制台输入应用程序名称时能够提供输入。在这种情况下，你可以使用包含两个参数的 `main()` 函数的这种替代形式：

```cpp
int main(int argc, char *argv[])
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_186_0.png)

图6-3：命令行应用程序通常带有开关和参数。

要使这些开关及其关联的参数正常工作，`main()` 函数必须处理输入。你可以使用 `argc` 确定用户提供了多少个命令行参数，然后使用 `argv` 访问这些参数。第2册第2章讨论数组这一主题。数组是按一个名称存储的变量序列。`argv` 变量就是其中之一。要访问存储在名为 `argv` 的统一名称下的各个变量，你可以这样做：

```cpp
cout << argv[0] << endl;
```

在这个例子中，你使用的方括号与你访问字符串中各个字符时使用的一样。当使用 `/?` 开关时，你会看到 `/?` 作为输出。你可以使用for循环访问命令行参数。清单6-12中的 CommandLineParameters 示例演示了这一技术。

### 清单6-12：访问命令行参数

```cpp
#include <iostream>
#include <stdlib.h>

using namespace std;

int main(int argc, char *argv[])
{
    for (int index=1; index < argc; index++)
    {
        cout << argv[index] << endl;
    }

    return 0;
}
```

## 用函数划分你的工作

