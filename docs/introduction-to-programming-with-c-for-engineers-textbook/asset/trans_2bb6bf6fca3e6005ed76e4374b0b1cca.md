

```cpp
double to_val {};

wcout << L"Enter from currency code:"; wcin >> from_curr; wcout << endl;
wcout << L"Enter value to exchange:"; wcin >> from_val; wcout << endl;
wcout << L"Enter to currency code :"; wcin >> to_curr; wcout << endl;

if( currencyExchangerObj.Convert( from_curr, stod( from_val ),
                                  to_curr, to_val ) == true )
    wcout << from_val << L" " + from_curr + L" => " << to_val
          << L" " + to_curr << endl;
else
    wcout << L"Cannot convert these currencies" << endl;
}
catch( ... )
{
    wcout << L"Error - wrong input." << endl;
}

// Ask the user what to do next
wcout << endl << L"New conversion [y/n]?";
wcin >> answer;
wcout << endl;

} while( answer.find( L"y" ) != wstring::npos );

}
```

UserInterface 在一个 do-while 循环中运行，从第 [79] 行开始。在第 [81–96] 行，循环内部设置了一个 try-catch 语句，用于拦截被调用函数可能抛出的异常对象。其中之一是 stod，它在第 [91] 行被调用，用于将字符串转换为 double 值。

在第 [112] 行，定义了 Run 函数，它接收 TCurrencyExchanger 对象。该函数只是简单地调用我们已经见过的三个函数：DisplayCurrentTime [115]、DisplayAllCurrencies [118] 和 UserInterface [120]：

```cpp
// Run if we already have the currency exchanger object
void Run( const TCurrencyExchanger & currExchObj )
{
    wcout << L"*** Welcome to the currency exchanger ***" << endl;
    DisplayCurrentTime();
    wcout << endl;

    DisplayAllCurrencies( currExchObj );

    UserInterface( currExchObj );
}
```

另一个重载函数 Run 在第 [123] 行定义。这一次，它在内部通过调用 CreateCurExchanger 来创建 TCurrencyExchanger 对象。正如我们已经指出的，要创建它，必须有一个初始化文件。该文件通过第 [125] 行的 std::filesystem²⁴ 访问，并在第 [127] 行创建 iniPath。（关于 C++ 文件系统的更多细节将在 6.2.7 节中介绍。）然后在第 [130] 行调用 CreateCurExchanger。如果返回一个有效对象，则在第 [132] 行调用 Run。否则，在第 [136] 行显示一条错误消息，程序终止。

```cpp
// All actions
void Run( void )
{
    namespace fs = std::filesystem;
    wstring iniPath( fs::current_path() / fs::path( initDefaultFileName ) );
    // At first try to get the currency object
    if( CurrExch_Optional all_my_options { CreateCurExchanger( iniPath ) }; all_my_options )
    {
        Run( * all_my_options );
    }
    else
    {
        wcout << L"Error, check Currency.txt file." << endl
        << L"Exiting ..." << endl;
    }
}
// End of CurrExchanger namespace
```

最后，main 函数如下所示。在第 [156] 行，调用 setmode 函数来设置终端的显示模式。这样做是为了正确处理 Unicode 字符。然后，在第 [157] 行调用 CurrExchanger::Run。最后，在第 [158] 行返回成功代码。

```cpp
#include <io.h>
#include <fcntl.h>

namespace CurrExchanger
{
    void Run( void );
}

// Keep main() simple
int main( void )
{
    setmode( _fileno( stdout ), _O_U16TEXT );
    CurrExchanger::Run();
    return 0; // Although not absolutely required, return a value also from main
}
```

关于何时使用类（class）、何时使用命名空间（namespace）或两者兼用的问题尚无定论，软件设计者的意见也各不相同。像往常一样，没有单一的答案或通用的法则，所选择的方法取决于具体问题。在这种情况下，尝试预见给定组件的未来使用场景和调用上下文，并选择最自然、最简单、最通用的解决方案是很有帮助的。通常，这是通过迭代方式获得的，在第一个版本得到改进之后。编程之美在于，同一件事可以通过许多不同的方式实现，而且往往会产生不同的后果。这也是本节中介绍的 *CurrencyExchanger* 背后的故事。另一种方法留作练习。

在 *CurrencyCalc* 项目中，我们学到了以下内容：

- 创建带有构造函数以初始化数据的简单类
- 创建带有默认特殊成员函数和虚析构函数的类，以备将来继承
- 使用 `std::map` 容器存储 `<key,value>` 对
- 在访问 `std::map` 元素时使用结构化绑定
- 输入/输出：
  - 重载 `operator <<` 和 `operator >>` 用于数据输出和输入
  - 流操纵符
  - 使用宽字符（Unicode）与 `std::wstring`、`std::wcout`、`std::wifstream` 和 `std::wofstream` 对象
  - 使用 `std::filesystem` 命名空间中的文件系统元素进行文件的写入和读取
- 使用 `stod` 函数将 `std::wstring` 转换为 double
- 使用 `std::optional` 表示一个可选可用的对象
- 使用 try-catch 语句
- 创建具有已定义命名空间的软件组件
- 使用 `std::chrono::system_clock` 中的对象访问系统时间

在 6.2 节中，我们将进一步扩展 *CurrencyCalc* 项目。

## 3.19 运算符

在本节的表格中，我们按优先级列出了所有 C++ 运算符，并附有简短说明和简要示例。请记住，在编写 C++ 程序时，并非所有运算符都同等重要。此外，其中一些运算符很少使用或已过时。有些运算符的完整描述将在后续章节中给出。为了完整起见，还指出了 C 特有运算符和 C++ 特有运算符之间的差异（附录 A.2）。

为了完全理解运算符的工作方式，我们需要定义*左值*和*右值*：

- *左值* – 可以用于赋值运算符（`=`）左侧的对象。也就是说，它必须是一个可以被赋值的对象。
- *右值* – 位于赋值运算符右侧的对象。也就是说，它是充当一个值的对象。

下一个重要的概念是运算符优先级和结合性：

- *优先级* – 在计算表达式时，指示哪个运算应该在其他运算之前执行的规则。
- *结合性* – 当在相同优先级的运算符之间进行选择时，用于选择首先执行的运算符的规则。大多数 C++ 运算符是左结合的，但一元运算符和赋值运算符除外，它们是右结合的。如果一个操作数位于相同优先级的运算符之间（例如在 a + b − c 中），就必须检查结合性规则；见图 3.30。在这种情况下，b 位于 + 和 − 之间，它们属于同一优先级组。两者都是左结合的，因此 b 首先被 + “取用”；从而先执行 a + b，然后从该结果中减去 c。因此，原表达式将被计算为 (a + b) − c。另一方面，右结合运算符的示例见图 3.31。

![图 3.30](img/31dee73f41f3d43a1f2e2b4eaffa2afd_209_0.png)

**图 3.30** 左结合（左）和右结合（右）情况下表达式求值顺序的示例。在 C++ 中，加法 + 和减法 − 运算符具有相同的优先级，并且是左结合的。因此，使用左侧的求值顺序：操作数 b 首先被其左侧的运算符 + 使用，计算 a + b；然后将该运算的结果用于减法 − c。这第二个结果就是表达式的值。

![图 3.31](img/31dee73f41f3d43a1f2e2b4eaffa2afd_209_1.png)

**图 3.31** 右结合赋值运算符的示例。为了获得正确、直观的结果，必须先将 c 赋值给 b，然后再将 b 赋值给 a。

让我们考虑以下示例：

```cpp
char * ptr = "The book";
char first_letter = * ptr++;
```

在第一行中，* 不是运算符，因为在这个上下文中，它的左侧有一个类型名；它们合在一起表示“指向 char 的指针”，我们将其命名为 ptr。指针 ptr 是一个左值，因为它位于赋值运算符 = 的左侧。它的右边是字符串字面量 "The book"，它必须是一个右值，因为它不能被修改。更准确地说，该文本被放置在程序常量内存中的某个位置，而指向其开头的指针被用作右值，然后将其赋值给 ptr。

在示例的第二行中，有两个由 first_letter 和 ptr 标识符指示的对象。这里，first_letter 充当左值，因为它是被赋值的对象。我们有三个运算符：=、* 和 ++。它们的求值顺序由它们在所有运算符层次结构中的级别严格定义，如下一节中的表格所示。为了找到它们正确的优先级，首先让我们确切地确定我们正在处理哪些运算符，因为许多符号（例如 *）在不同的上下文中使用时含义完全不同。例如，* 在第一行中与 char 关键字一起使用，但 * 也可以表示二元乘法运算符或一元指针解引用。在这个示例中，* 不在两个操作数之间，而是在指针 ptr 的前面，因此它表示指针解引用。查看以下各节中的表格，我们可以很容易地发现它属于第 3 组（表 3.15）。

