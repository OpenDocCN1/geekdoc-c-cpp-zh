

## 显示 12.7 格式化输出（第 3 部分，共 3 部分）

示例对话

# Rawdata.txt
（未被程序更改）

```
10.37    -9.89897
2.313   -8.950   15.0

7.33333   92.8765
-1.237568432e2
```

# neat.txt
（程序运行后）

```
+10.37000
-9.89897
+2.31300
-8.95000
+15.00000
+7.33333
+92.87650
-123.75684
```

# 屏幕输出

```
+10.37000
-9.89897
+2.31300
-8.95000
+15.00000
+7.33333
+92.87650
-123.75684
End of program.
```

# 示例：编辑文本文件

这里讨论的程序是文本编辑应用于文件的一个非常简单的例子。此程序可用于以一种相当简单的方式从现有的 C 广告材料自动生成 C++ 广告材料。程序从包含赞美 C 的广告文案的文件中读取输入，并将类似的关于 C++ 的广告文案写入另一个文件。包含 C 广告文案的文件称为 cad.txt，而接收 C++ 广告文案的新文件称为 cppad.txt。程序显示在显示 12.8 中。程序只是读取文件 cad.txt 中的每个字符并将字符复制到文件 cppad.txt 中。每个字符都被原样复制，除了当从输入文件读取大写字母 'C' 时，程序将字符串 "C++" 写入输出文件。该程序假设只要字母 'C' 在输入文件中出现，它就表示 C 编程语言；因此这种更改正是产生更新后的广告文案所需的。

请注意，当程序从输入文件读取字符并将字符写入输出文件时，换行符得以保留。换行符 '\n' 被当作任何其他字符对待。它使用成员函数 get 从输入文件读取，并使用插入运算符 << 写入输出文件。我们必须使用成员函数 get 来读取输入（而不是提取运算符 >>），因为我们希望读取空白字符。

## 显示 12.8 编辑文本文件（第 1 部分，共 2 部分）

```cpp
//Program to create a file called cpplad.txt that is identical
//to the file cad.txt except that all occurrences of 'C' are replaced
//by "C++". Assumes that the uppercase letter 'C' does not occur in
//cad.txt except as the name of the C programming language.
#include <fstream>
#include <iostream>
#include <cstdlib>
using std::ifstream;
using std::ofstream;
using std::cout;

void addPlus(ifstream& inStream, ofstream& outStream)
//Precondition: inStream has been connected to an input file with open.
//outStream has been connected to an output file with open.
//Postcondition: The contents of the file connected to inStream have been
//copied into the file connected to outStream, but with each 'C' replaced
//by "C++". (The files are not closed by this function.)

int main( )
{
    ifstream fin;
    ofstream fout;

    cout << "Begin editing files.\\n";

    fin.open("cad.txt");
    if (fin.fail( ))
    {
        cout << "Input file opening failed.\\n";
        exit(1);
    }

    fout.open("cppad.txt");
    if (fout.fail( ))
    {
        cout << "Output file opening failed.\\n";
        exit(1);
    }
}
```

## 12.3 流层次结构：继承的预览
组织类的一个非常有用的方法是使用“派生自”的关系。当我们说一个类派生自另一个类时，我们的意思是派生类是通过添加特性从另一个类获得的。例如，输入文件流的类是通过添加诸如 open 和 close 之类的额外成员函数从所有输入流的类派生而来的。流 cin 属于所有输入流的类，但不属于输入文件流的类，因为 cin 没有名为 open 和 close 的成员函数。本节介绍派生类的概念，作为思考和组织预定义流类的一个方式。（第 14 章展示了如何使用派生类的思想来定义自己的类。）

### 流类之间的继承

预定义的流 cin 和输入文件流都是输入流。因此在某种意义上它们是相似的。例如，你可以使用提取运算符 >> 与任何一种流一起使用。另一方面，输入文件流可以使用成员函数 open 连接到文件，但流 cin 没有名为 open 的成员函数。输入文件流是一种与 cin 相似但不同的流类型。输入文件流的类型为 ifstream。对象 cin 是类 istream 的对象（拼写时不带 'f'）。类 ifstream 和 istream 是不同但密切相关的类型。类 ifstream 是类 istream 的派生类。让我们看看这意味着什么。

当我们说某个类 D 是某个类 B 的派生类时，这意味着类 D 具有类 B 的所有特性，但它还具有附加特性。例如，任何类型为 istream（不带 'f'）的流都可以使用提取运算符 >>。类 ifstream（带 'f'）是类 istream 的派生类，因此类型为 ifstream 的对象可以使用提取运算符 >>。类 ifstream 的对象具有类 istream 对象的全部属性。特别是，类 ifstream 的对象也是类型为 istream 的对象。

然而，ifstream 具有附加特性，因此你可以用类型为 ifstream 的对象做更多的事情，而不仅仅是类型为 istream 的对象。例如，一个附加特性是类型为 ifstream 的流可以使用函数 open。流 cin 仅为类型 istream 而不是类型 ifstream。你不能使用函数 open 使用 cin。请注意，类 ifstream 和 istream 之间的关系不是对称的。每个类型为 ifstream 的对象都是类型为 istream 的对象（文件输入流是输入流），但类型为 istream 的对象不一定是类型为 ifstream 的对象（对象 cin 是类型为 istream 但不是类型为 ifstream）。

派生类的思想其实很常见。来自日常生活的例子可能有助于使这个思想更清晰。例如，所有敞篷车的类是所有汽车类的派生类。每辆敞篷车都是汽车，但敞篷车不仅仅是一辆汽车。敞篷车是一种具有其他汽车不具备的特殊属性的特殊汽车。如果你有一辆敞篷车，你可以放下车顶使汽车敞开。（你可以说敞篷车具有作为附加特性的“打开”功能。）

如果 D 是类 B 的派生类，则每个类型为 D 的对象也是类型为 B 的对象。敞篷车也是汽车。文件输入流（类 ifstream 的对象）也是输入流（也是类 istream 的对象）。因此，如果我们使用 istream 作为函数参数的类型，而不是使用 ifstream，那么可以为该参数插入更多对象。考虑以下两个函数定义，它们仅在参数类型（和函数名）上有所不同：

```
void twoSumVersion1(ifstream& sourceFile) //ifstream with an 'f'
{
    int n1, n2;
    sourceFile >> n1 >> n2;
    cout << n1 << " + " << n2 << " = " << (n1 + n2) << endl;
}
```

和

```
void twoSumVersion2(istream& sourceFile) //istream without an 'f'
{
    int n1, n2;
    sourceFile >> n1 >> n2;
    cout << n1 << " + " << n2 << " = " << (n1 + n2) << endl;
}
```

对于 twoSumVersion1，参数必须是类型 ifstream。因此如果 fileIn 是一个连接到文件的输入文件流，则

```
twoSumVersion1(fileIn);
```

是合法的，但

```
twoSumVersion1(cin); //ILLEGAL
```

不合法，因为 cin 不是类型 ifstream。对象 cin 只是一个流且仅为类型 istream；cin 不是文件输入流。

函数 twoSumVersion2 更通用。以下两者都是合法的：

```
twoSumVersion2(fileIn);
twoSumVersion2(cin);
```

寓意很清楚：只要可以，就使用 istream 而不是 ifstream 作为参数类型。在选择参数类型时，使用你能用的最通用的类型。（为了做一个现实生活的类比考虑以下：你可能更喜欢拥有一辆敞篷车，但你不会想要一个只能容纳敞篷车的车库。如果朋友借给你一辆轿车呢？你仍然希望能把轿车停进你的车库。）

你不能总是使用参数类型 istream 代替参数类型 ifstream。如果你定义一个参数类型为 istream 的函数，则该参数只能使用 istream 成员函数。特别是，它不能使用函数 open 和 close。如果你不能将对成员函数 open 和 close 的所有调用都放在函数定义之外，则必须使用类型为 ifstream 的参数。

到目前为止，我们讨论了输入流的两个类：istream 及其派生类 ifstream。输出流的情况类似。第 1 章介绍了

