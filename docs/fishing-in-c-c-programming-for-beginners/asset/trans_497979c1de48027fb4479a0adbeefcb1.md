

## Hello World

看，这里 \b 将光标移回字符 'c'，然后我们用空格覆盖 c。我们也可以用空格覆盖任何字符。

### 请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"Helloc\b World";
}
```

### 输出

Hello World

这里，我们在 \b 后留了一个空格，因此 c 被空格覆盖，我们得到了所需的输出 Hello World。

## \f 换页符

该字符在程序中很少使用，但如果涉及打印机或 Word 文件，则广泛使用。该字符向操作系统发出信号，表明当前页面已结束，是时候开始新页面了。但是，在程序输出中，它只显示用于打印机或文件的该字符所起的作用。因此，如果我们想通过程序在 Word 文件中插入新页面，我们会在那里使用 \f。由于大多数书籍只介绍文本文件和二进制文件，因此它们不会告诉你这一点。

要验证我们在这里学到的内容，在学习完文件知识后，请返回此处并运行以下程序：

```cpp
#include<iostream>
#include<fstream>
using namespace std;
int main()
{
    fstream fout;
    fout.open("A.doc", ios::out);

    if(!fout)
    {
        cout<<"Can't open";
        return -1;
    }

    fout<<"Hello World\fHello World";

    fout.close();
}
```

这里，将创建并写入一个名为 A.doc 的文件。当你打开 A.doc 时，你会看到 Hello World 写在两个不同的页面上。这证实了字符 \f 分隔了页面。

![](img/5340985153962870d4e4a3b9453b9146_31_0.png)

## \n 换行

该字符用于换行，即在该字符之后写的任何内容都将写在新行上。请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello\nWorld";
}
```

### 输出

Hello

World

这里，Hello 和 World 将显示在不同的行上。

## \r 回车

这与 \n 不同。问题在于，人们通常从未被解释过在哪里使用 \r。因此，他们在论坛上关于其用法提出了许多问题。嗯，\r 将光标移动到当前显示行的开头。例如，请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello world\rBlack";
}
```

### 输出：

Black world

看，这里在打印 Hello World 之后，光标移动到行首，然后由于需要写入 Black，它用 Black 覆盖了它。现在你已经理解了，\r 有点像 \b，但与 \n 完全不同。你也可以说这相当于键盘上的 Home 键。

## \t 制表符

这用于在输出屏幕上留出一个制表符空格。一个制表符空格通常等于五个空格。例如，请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello world\tBlack";
}
```

### 输出

Hello world   Black

这通常用于在输出屏幕上创建菜单栏。例如，请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"1.File\t2.Edit\t3.View\t4.Search\t5.Exit";
}
```

### 输出

1.File   2.Edit   3.View   4.Search   5.Exit

## 反斜杠的各种用法

假设我们正在向某人演示 \b，并且我们必须显示 \b 而不是其效果。你可能会认为 `cout<<"\b";` 会显示 \b，但随后你会发现它反而会尝试将光标向后移动一步。那么，如何打印 \b 呢？解决方案是使用双反斜杠。例如，请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"\\b";
    cout<<"\\n";
    cout<<"\\n";
    cout<<"\\n";
    cout<<"\\"";
}
```

### 输出

\b



"

看，要打印单个撇号、双撇号和反斜杠，我们必须在它们前面使用反斜杠。

## puts() 函数

puts() 是一个用于打印字符串输出然后换行的函数。该函数在 stdio.h 中定义。因此，如果在编译时编译器报错说 puts() 应该有原型或 puts() 未声明，那么只需在程序开头添加 `#include<stdio.h>`。所有最新的编译器也在 iostream 中包含此函数。

例如，请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    puts("Aman");
    puts("Kumar");
}
```

### 输出：

Aman
Kumar

这里，Aman 和 Kumar 将分别打印在不同的行上，而不是使用换行符。这是 puts() 的一个特性。

## cout.put()

此函数在屏幕上放置一个字符。与 puts() 不同，它不插入任何换行。请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout.put('a');
    cout.put('k');
}
```

### 输出：

ak

现在，请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout.put('a').put('k');
}
```

### 输出：

ak

此程序显示 .put() 可以级联多次。

## cout.write()

这用于在输出屏幕上显示特定数量的字节。例如，请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout.write("Aman Kumar Jha", 7);
}
```

### 输出：

Aman Ku

这里，只会显示传递字符串的前七个字节。

## endl

该宏产生一个换行字符，就像插入 `\n` 一样，但当与缓冲流一起使用时，它还有一个额外行为：缓冲区会被刷新。例如，请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello"<<endl;
    cout<<"world";
}
```

### 输出

Hello

world

看，上面一行展示了 endl 的用法。请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello"<<endl<<"world";
}
```

此程序的输出与前一个程序相同。

## oct, dec, hex

这些是用于显示变量或常量的八进制和十六进制值的一些宏。例如，请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<17<<endl;
    cout<<oct<<17<<endl;
    cout<<hex<<17<<endl;
    cout<<dec<<17;
}
```

### 输出

17
21
11
17

这些宏也与函数配合使用良好。在阅读完函数章节后，请返回此处并查看以下程序：

```cpp
#include<iostream>
using namespace std;
int add(int, int);
int main()
{
    cout<<add(5, 6)<<endl;
    cout<<oct<<add(5, 6);
}

int add(int a, int b)
{
    return a + b;
}
```

### 输出
11
13

## iomanip.h

这是一个用于输入/输出操作的头文件。我们将出于各种目的包含它。它包括各种函数、宏和类。其中一些非常有用，我们将讨论它们。

- setprecision()
- setbase()
- setw()

### setbase()

setbase() 是 oct、dec 和 hex 三个不同宏的替代方案。

```cpp
#include<iostream>
#include<iomanip>
using namespace std;
int main()
{
    cout<<setbase(8)<<17<<endl;
    cout<<setbase(10)<<17<<endl;
    cout<<setbase(16)<<17;
}
```

### 输出
21
17
11

不能将任何数字作为参数传递给 setbase()，因为它只会显示八进制、十进制或十六进制值，因此只能使用 8、10、16。

### setprecision()

它用于设置精度点。假设你有一个值，例如 21.23456789，并且你想显示该数字直到五位数字；那么程序将是：

```cpp
#include<iostream>
#include<iomanip>
using namespace std;
int add(int, int);
int main()
{
    float a = 21.23456789;
    cout<<setprecision(5)<<a;
}
```

### 输出
21.345

现在，想想如果我们尝试将精度点设置为小于 2，输出会是什么。请参考以下程序：

```cpp
#include<iostream>
#include<iomanip>
using namespace std;
int add(int, int);
int main()
{
    float a = 21.23456789;
    cout<<setprecision(1)<<a;
}
```

### 输出
2e+001

因此，随着 setprecision() 中的值减小，它开始将数字转换为科学计数法。但是，使用它我们无法决定使用四舍五入显示小数点后的位数。在这里，使用了 setw()。

### setw()

此函数允许我们使用四舍五入显示小数点后固定数量的数字。例如，请参考以下程序：

```cpp
#include<iostream>
#include<iomanip>
using namespace std;
int add(int, int);
int main()
{
    float a = 21.23456789;
    cout<<setw(4)<<a;
}
```

### 输出
21.2346

