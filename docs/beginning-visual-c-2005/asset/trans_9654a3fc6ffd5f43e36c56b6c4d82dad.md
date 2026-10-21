

# 试一试   作用域解析运算符

正如你所见，一个全局变量可以被同名局部变量隐藏。然而，仍然可以通过使用作用域解析运算符（::）来访问全局变量，你在第 1 章讨论命名空间时见过它。我可以用上一个示例的修订版本来演示其工作原理：

// Ex2_08.cpp
// Demonstrating variable scope
#include <iostream>

using std::cout;
using std::endl;

int count1 = 100;                     // Global version of count1

int main()
{
    // Function scope starts here
    int count1 = 10;
    int count3 = 50;
    cout << endl
         << "Value of outer count1 = " << count1
         << endl;
    cout << "Value of global count1 = " << ::count1      // From outer block
         << endl;

    {
        // New scope starts here...
        //This hides the outer count1
        int count1 = 20;
        int count2 = 30;
        cout << "Value of inner count1 = " << count1
             << endl;
        cout << "Value of global count1 = " << ::count1      // From inner block
             << endl;

        count1 += 3;               // This affects the inner count1
        count3 += count2;          // ...and ends here.
    }

    cout << "Value of outer count1 = " << count1
         << endl
         << "Value of outer count3 = " << count3
         << endl;

    //cout << count2 << endl;      // uncomment to get an error

    return 0;
}                                   // Function scope ends here
```

如果你编译并运行这个示例，你会得到以下输出：

```
Value of outer count1 = 10
Value of global count1 = 100
Value of inner count1 = 20
```

```
Value of global count1 = 100
Value of outer count1 = 10
Value of outer count3 = 80
```

阴影代码行表示我对前一个示例所做的更改；我只需要讨论这些更改的影响。 在函数 main() 定义之前声明的 count1 是全局的，因此原则上它在函数 main() 中的任何地方都可用。 这个全局变量被初始化为 100：

```
int count1 = 100;                      // Global version of count1
```

然而，你在 main() 内定义了另外两个名为 count1 的变量，因此在整个程序中，全局 count1 被局部 count1 变量隐藏。 第一个新的输出语句是：

```
cout << "Value of global count1 = " << ::count1        // From outer block
    << endl;
```

这使用了作用域解析运算符（::）来明确告诉编译器你想要引用全局变量 count1，而不是局部变量。 你可以从输出中显示的值看出这一点。

在内部块中，全局 count1 被两个名为 count1 的变量隐藏：内部 count1 和外部 count1。 我们可以在内部块中看到全局作用域解析运算符发挥作用，正如我们在那里添加的语句生成的输出所示：

```
cout << "Value of global count1 = " << ::count1        // From inner block
    << endl;
```

这输出的值为 100，与之前一样 — 以这种方式使用的作用域解析运算符的长臂总是到达全局变量。

> 你之前看到过，你可以通过将名称与命名空间名称限定，例如 std::cout 或 std::endl，来引用 std 命名空间中的名称。 编译器会在作用域解析运算符左操作数指定的命名空间中搜索你作为右操作数指定的名称。 在前面的示例中，你正在使用作用域解析运算符在全局命名空间中搜索变量 count1。 通过不在运算符前面指定命名空间名称，你是在告诉编译器在全局命名空间中搜索其后的名称。

当你进入第 9 章探索面向对象编程时，你会看到更多这个运算符的使用，在那里它被广泛使用。

## 静态变量

可以想象，你可能想要一个在局部定义和可访问的变量，但它在退出声明它的块后仍然存在。 换句话说，你需要在块作用域内声明一个变量，但要赋予它静态存储期。 static 说明符为你提供了这样做的手段，并且当我们在第 5 章处理函数时，这种需求会变得更加明显。

事实上，静态变量将在程序的生命周期内继续存在，即使它是在块内声明的并且只能从该块（或其子块）内访问。 它仍然具有块作用域，但具有静态存储期。 要声明一个名为 count 的静态整数变量，你可以写：

```
static int count;
```

如果你在声明静态变量时没有提供初始值，它会为你初始化。 这里声明的变量 count 将被初始化为 0。 静态变量的默认初始值始终为 0，转换为适用于该变量的类型。 请记住，自动变量并非如此。

> 如果你没有初始化自动变量，它们将包含上一个使用它们所占内存的程序留下的垃圾值。

## 命名空间

我多次提到命名空间，所以是时候让你更好地了解它们了。 它们未在支持 MFC 的库中使用，但支持 CLR 和 Windows 窗体的库大量使用命名空间，当然 ANSI C++ 标准库也是如此。

你已经知道 ISO/ANSI C++ 标准库中使用的所有名称都在名为 std 的命名空间中定义。 这意味着标准库中使用的所有名称都有一个额外的限定名称 std，因此例如 cout 实际上是 std::cout。 你可以在一个简单的示例中看到完全限定的名称的使用：

// Ex2_09.cpp
// Demonstrating namespace names
#include <iostream>

    int value = 0;

int main()
{
    std::cout << "enter an integer: ";
    std::cin  >> value;
    std::cout << "\nYou entered " << value
              << std::endl;
    return 0;
}
```

变量 value 的声明在 main() 的定义之外。 该声明被称为在全局命名空间作用域，因为变量声明没有出现在命名空间内。 该变量可以从 main() 内的任何位置以及同一源文件中可能拥有的任何其他函数定义中访问。 我只是把 value 的声明放在 main() 之外，以便在下一节中演示它如何位于命名空间中。

注意 cout 和 endl 的 using 声明的缺失。 在这种情况下并非必要，因为你正在完全限定从命名空间 std 使用的名称。 这很愚蠢，但你可以在这里使用 cout 作为整数变量的名称，并且不会有混淆，因为 cout

你不能在函数内部声明命名空间。 它 intended 的使用方式是相反的；你使用命名空间来包含程序中的函数、全局变量和其他命名实体，如类。 你不能把 main() 的定义放在命名空间中。 执行开始的函数 main() 必须始终位于全局命名空间作用域，否则编译器不会识别它。

```cpp
// Ex2_10.cpp
// Declaring a namespace
#include <iostream>

namespace myStuff
{
	int value = 0;
}

int main()
{
	std::cout << "enter an integer: ";
	std::cin >> myStuff::value;
	std::cout << "\nYou entered " << myStuff::value
	<< std::endl;
	return 0;
}
```

myStuff 命名空间定义了一个作用域，命名空间作用域内的所有内容都用命名空间名称限定。 要从命名空间外部引用在命名空间内声明的名称，你必须用命名空间名称限定它。 在命名空间作用域内，可以在不加限定地引用其中声明的任何名称 — 它们都是同一个家族的一部分。 现在你必须用 myStuff，即我们的命名空间的名称，来限定名称 value。 如果不这样做，程序将无法编译。 函数 main() 现在引用了两个不同命名空间中的名称，通常你的程序中可以有任意多的命名空间。 你可以通过添加 using 指令来消除限定 value 的需要：

```cpp
// Ex2_11.cpp
// Using a using directive
#include <iostream>

namespace myStuff
{
	int value = 0;
}

using namespace myStuff; // Make all the names in MyStuff available

int main()
{
	std::cout << "enter an integer: ";
	std::cin >> value;
	std::cout << "\nYou entered " << value
	<< std::endl;
	return 0;
}
```

