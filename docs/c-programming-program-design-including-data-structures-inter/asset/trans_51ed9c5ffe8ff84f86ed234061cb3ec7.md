
示例运行：在此示例运行中，用户输入以底纹显示。

```
Line 9: firstNum = 18
Line 10: Enter an integer: 15
Line 13: secondNum = 15
Line 15: The new value of firstNum = 60
```

前面的程序工作方式如下：第 1 行的语句包含头文件 *iostream*，以便程序能够执行输入/输出。第 2 行的语句使用 *using namespace* 语句，以便头文件 *iostream* 中声明的标识符（如 *cin*、*cout* 和 *endl*）无需使用前缀 *std::* 即可使用。第 3 行的语句声明命名常量 *NUMBER* 并将其值设为 12。第 4 行的语句包含函数 *main* 的标题，第 5 行的左花括号标记函数 *main* 的开始。第 6 行和第 7 行的语句声明变量 *firstNum* 和 *secondNum*。

第 8 行的语句将 *firstNum* 的值设为 18，第 9 行的语句输出 *firstNum* 的值。接下来，第 10 行的语句提示用户输入一个整数。第 11 行的语句读取该整数并将其存储到变量 *secondNum* 中，在示例运行中该值为 15。第 12 行的语句将屏幕上的光标定位到下一行的开头。第 13 行的语句输出 *secondNum* 的值。第 14 行的语句计算表达式：

```
firstNum + NUMBER + 2 * secondNum
```

并将该表达式的值赋给变量 *firstNum*，在示例运行中该值为 60。第 15 行的语句输出 *firstNum* 的新值。第 16 行的语句包含 *return* 语句，这是最后一条可执行语句。第 17 行的右花括号标记函数 *main* 的结束。

## 调试：理解并修复语法错误

本章前面的各节介绍了 C++ 程序的基本组成部分。当你输入程序时，拼写错误和无意的语法错误很可能会出现。因此，当你编译程序时，编译器将识别语法错误。在本节中，我们将展示如何识别并修复语法错误。

考虑以下 C++ 程序：

```
1. #include <iostream>
2. 
3. using namespace std;
4. 
5. int main()
6.  {
7.      int num
8.
9.      num = 18;
10.
11.     tempNum = 2 * num;
12.
13.     cout << "Num = " << num << ", tempNum = " < tempNum << endl;
14.
15.     return ;
16. }
```

（注意，左侧的数字 1 到 16 不是程序的一部分。我们给语句编号以便参考。）该程序包含语法错误。当你编译该程序时，编译器会产生以下错误。（该程序使用 Microsoft Visual Studio 2010 编译。）

```
ExampleCh2_Syntax_Errors.cpp
c:\examplech2_syntax_errors.cpp(9): error C2146: syntax error : missing ';'
 before identifier 'num'
c:\examplech2_syntax_errors.cpp(11): error C2065: 'tempNum' : undeclared identifier
c:\examplech2_syntax_errors.cpp(13): error C2065: 'tempNum' : undeclared identifier
c:\examplech2_syntax_errors.cpp(13): error C2563: mismatch in formal parameter list
c:\examplech2_syntax_errors.cpp(13): error C2568: '<<' : unable to resolve
 function overload
        c:\program files\microsoft visual studio
10.0\vc\include\ostream(1021): could be 'std::basic_ostream<_Elem,_Traits>
&std::endl(std::basic_ostream<_Elem,_Traits> &)'
        with
            [
                _Elem=unsigned short,
                _Traits=std::char_traits<unsigned short>
            ]
        c:\program files\microsoft visual studio
10.0\vc\include\ostream(1011): or       'std::basic_ostream<_Elem,_Traits>
&std::endl(std::basic_ostream<_Elem,_Traits> &)'
        with
            [
                _Elem=wchar_t,
                _Traits=std::char_traits<wchar_t>
            ]
        c:\program files\microsoft visual studio
10.0\vc\include\ostream(1003): or       'std::basic_ostream<_Elem,_Traits>
&std::endl(std::basic_ostream<_Elem,_Traits> &)'
        with
            [
                _Elem=char,
                _Traits=std::char_traits<char>
            ]
c:\program files\microsoft visual studio 10.0\vc\include\ostream(977):
or		'std::basic_ostream<_Elem, _Traits>&
&std::endl(std::basic_ostream<_Elem, _Traits>&)'
c:\examplech2_syntax_errors.cpp(15): error C2561: 'main' : function must return a
value
c:\examplech2_syntax_errors.cpp(5) : see declaration of 'main'
```

最好尝试自上而下地纠正错误，因为第一个错误可能会使编译器混淆，并在较早行实际上只有一个错误时标记多个后续错误。因此，让我们先考虑以下错误：

```
c:\examplech2_syntax_errors.cpp(9): error C2146: syntax error : missing ';'
before identifier 'num'
```

表达式 examplech2_syntax_errors.cpp(9) 表明第 9 行存在错误。该错误的其余部分指明在标识符 num 之前缺少 ;。如果我们查看第 7 行，会发现语句 int num 末尾缺少分号。因此，我们必须在第 7 行语句末尾插入 ;。

接下来，考虑第二个错误：

```
c:\examplech2_syntax_errors.cpp(11): error C2065: 'tempNum' : undeclared identifier
```

此错误发生在第 11 行，并指明标识符 tempNum 未声明。当我们查看代码时，发现该标识符尚未声明。因此，我们必须将 tempNum 声明为 int 变量。

错误：

```
c:\examplech2_syntax_errors.cpp(13): error C2065: 'tempNum' : undeclared identifier
```

发生在第 13 行，并指明标识符 tempNum 未声明。与前一个错误一样，我们必须声明 tempNum。请注意，一旦我们声明 tempNum 并重新编译，此错误和前一个错误都将消失。

下一个错误是：

```
c:\examplech2_syntax_errors.cpp(13): error C2563: mismatch in formal parameter list
```

此错误发生在第 13 行，并表明某个形参列表不匹配。对于初学者来说，这个错误有些难以理解。（在第 13 章中，我们将解释运算符 << 的形参列表。）然而，随着实践，你将学会如何解释和纠正语法错误。如果你查看下一个错误，这个错误就会变得清楚，其部分内容为：

```
c:\examplech2_syntax_errors.cpp(13): error C2568: '<<' : unable to resolve
function overload
```

它告诉我们，此错误与运算符 << 有关。当我们仔细查看第 13 行的语句，即：

```
cout << "Num = " << num << ", tempNum = " < tempNum << endl;
```

我们发现，在表达式 < tempNum 中，我们无意中使用了 < 代替了 <<。因此，我们必须纠正此错误。

让我们看看最后一个错误，即：

```
c:\examplech2_syntax_errors.cpp(15): error C2561: 'main': function must return a value
    c:\examplech2_syntax_errors.cpp(5): see declaration of 'main'
```

此错误发生在第 15 行。然而，此时给出的解释，尤其是对初学者来说，有些不清楚。但是，如果你查看第 15 行中的语句 `return ;` 并记住函数 main 的语法以及本书中给出的所有程序，我们会发现缺少数字 0，也就是说，该语句必须是 `return 0;`

从编译器报告的错误中，我们看到编译器不仅识别错误，还指明错误发生的行号和错误类型。我们可以有效地利用这些信息来修复语法错误。

纠正所有语法错误后，正确的程序是：

```
#include <iostream>

using namespace std;

int main()
{
    int num;
    int tempNum;

    num = 18;

    tempNum = 2 * num;

    cout << "Num = " << num << ", tempNum = " << tempNum << endl;

    return 0;
}
```

输出是：

```
Num = 18, tempNum = 36
```

当你学习 C++ 并练习编写和执行程序时，你将学会如何发现并修复语法错误。编译器报告的错误列表可能比程序本身还长。这是因为，如上所述，一行中的语法错误可能导致后续行出现语法错误。在这种情况下，按列出的顺序纠正语法错误并编译程序。如有必要，在每次纠正后重新编译。你会看到语法错误列表迅速缩短。重要的是不要惊慌。

在下一节中，我们将描述一些可以遵循的简单规则，以便你的程序结构正确。

