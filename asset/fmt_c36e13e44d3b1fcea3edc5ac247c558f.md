
```cpp
// 将两个数相加并返回和
int add(int a, int b)
{
    return a + b;
}
```

到目前为止，你一直将代码放在 `main(void)` 及其闭大括号内部。这段代码被称为主函数。函数声明和定义必须放在此区域之外。如果现在这看起来很困惑，不要担心；随着时间的推移，它会变得清晰。

编写此程序的另一种方法是将 `add` 定义放在代码的开头而不是末尾。在这种情况下，你不需要函数声明，因为函数本身就充当了自己的声明：

```cpp
#include <iostream>

int add(int a, int b)
{
    return a + b;
}
```

# 《C++ 编程入门》（第二版）

`int main(void)`

```cpp
int number1, number2;
    cout << "Enter the first value to be summed: ";
    cin >> number1;
    cout << "\nEnter the second: ";
    cin >> number2;
    cout << "nThe sum is: " << add(number1, number2) << "\n";
```

通过这种方式，将定义放在开头与添加声明并将定义放在程序末尾的效果一样。这两种方法都没有特别的优势，所以你选择哪一种仅仅取决于个人偏好。

## 函数重载 (OVERLOADING FUNCTIONS)

当你为超过一种可能的数据类型编写 `add` 函数时该怎么办？一种方法是为每个类型编写一个单独函数，并为每个函数使用不同的名称。你可能会将一个函数命名为 `int_add()` 来加两个整数，另一个函数命名为 `float_add()` 来加两个浮点数。

幸运的是，C++ 提供了替代方案。一种方法是函数重载（在此讨论），另一种方法是泛型编程（在第 7 章“代码重用：泛型编程”中讨论）。对于函数重载，你不必为每个函数使用不同的名称，而是给它们相同的名称。当你调用 `add` 函数时，计算机如何区分不同的版本？答案非常简单。计算机根据类型和参数数量来匹配函数调用。这是一个示例：

```cpp
int add (int a, int b)
{
    return a + b;
}
```

```cpp
double add (double a, double b)
{
    return a + b;
}
```

```cpp
int main(void) {
    cout << add(5,3);
    cout << add(5.5,4.7);
    return 0;
}
```

第一次调用 `add` 调用的是整数版本，因为 5 和 3 都是整数，这与整数版本的原型匹配。第二次调用 `add` 调用的是浮点数版本。

## 默认参数 (DEFAULTING ARGUMENTS)

某些函数非常有灵活性，提供了许多不同的选项来定制它们的工作方式。这导致调用函数时需要许多参数。然而，某些参数可能并不是需要的。在这种情况下，为这些参数设置默认值是合理的，这样就不需要每次都指定。

在 C++ 中，你可以指定默认值。这是实现参数的通用语法：

```cpp
return_type function_name(arg_name = default_value)
```

## 进一步了解作用域 (SEEING FURTHER WITH VARIABLE SCOPE)

到目前为止你学的所有内容可以分为四类，每类都有关于哪些变量可以访问它的规则：

- 主函数内部的代码
- 其他函数内部的代码
- 代码块内部（例如 `if` 语句或命名空间）
- 函数外部的代码

在这些每一个类别中，都有关于变量持续多长时间（变量生命周期）以及在哪里可以访问（变量作用域）的规则。

- 如果变量在代码块之外声明，它是全局变量，其作用域和生命周期从声明点开始持续到源文件结束。我们在本章前面提到过，代码块是任何位于大括号内的代码。这包括函数。
- 如果变量在代码块内部声明，它是局部变量，其作用域和生命周期持续到代码块结束。
- 如果变量在函数的参数列表中声明，它是参数，其作用域和生命周期持续到函数结束。

如果变量在一个嵌套在另一个代码块内部的代码块中声明，该变量的作用域将被限制在内部代码块中。

# 第 4 章 • 使用函数结构化代码

也许这个示例将有助于澄清前面的规则：

```cpp
//4.2 - 变量作用域示例 - Mark Lee
#include <iostream>

int subtract(int a, int b);

int global = 5;

int main(void)
{
    using std::cout;
    int a, b;
    a = 5;
    b = 3;
    cout << "The value of main's a is: " << a;
    cout << "\nThe value of main's b is: " << b;
    cout << "\nThe value of global is: " << global << "\n";
    global = 2 + subtract(a,b);
    cout << "The value of main's a now is: " << a;
    cout << "\nThe value of main's b now is: " << b;
    cout << "\nThe value of global now is: " << global << "\n";
    return 0;
}

int subtract(int a, int b)
{
    using std::cout;
    cout << "The value of subtract's a is: " << a;
    cout << "\nThe value of subtract's b is: " << b << "\n";
    a = b + global;
    return a;
}
```

输出：

The value of main's a is: 5

The value of main's b is: 3

The value of global is: 5

The value of subtract's a is: 5

The value of main's a now is: 5

The value of main's b now is: 3

The value of global now is: 9

在任何函数之前，声明了全局变量 `global`。在 `main` 开始处，声明了两个局部变量 `a` 和 `b`。当调用 `subtract` 时，`main` 中 `a` 和 `b` 的值被复制到 `subtract` 的 `a` 和 `b` 中。然后 `subtract` 计算差值并赋值给 `a`。当这个值从 `subtract` 函数返回时，执行 `global = 2 + subtract(a,b)`，你将得到结果：

```cpp
global = 2 + 7;
```

换句话说，因为 `subtract` 返回了 `subtract::a` 的值，这一行只是在返回值上加了 2，在这种情况下返回值是 7。

记住，这段代码中存在两个独立的、不相关的 `a` 和 `b` 的版本；`main` 的 `a` 与 `subtract` 的 `a` 没有任何关系。通常情况下，如此误用变量名并不是一个好主意。它们应该清晰地指示自己在所在作用域内的用途。

注意，对 `cout` 的 `using` 声明重复了两次，每个函数一次。这只适用于它所出现的代码块。如果你愿意，可以将该声明放在全局层级，即在每个函数之外，如下所示：

```cpp
//4.2 - 变量作用域示例 - Mark Lee
#include <iostream>

using std::cout;

int subtract(int a, int b);

int global = 5;

int main(void) {
    int a, b;
    a = 5;
    b = 3;
    cout << "The value of main's a is: " << a;
    cout << "\nThe value of main's b is: " << b;
    cout << "\nThe value of global is: " << global << "\n";
    global = 2 + subtract(a,b);
    cout << "The value of main's a now is: " << a;
    cout << "\nThe value of main's b now is: " << b;
    cout << "\nThe value of global now is: " << global << "\n";
    return 0;
}

int subtract(int a, int b)
{
  cout << "The value of subtract's a is: " << a
  << "\nThe value of subtract's b is: " << b << "\n";
  a = a - global;
  return a;
}
```

然而，将 `using` 声明放在适用的函数内部是更优的。这有助于代码更加清晰，让你确切知道在何处使用了什么。

### 使用作用域解析运算符进行指定

有时你可能会遇到全局变量和局部变量同名的情况。这在 C++ 中是合法的，但但可能会引起一些困惑。这是一个示例：

```cpp
int intVar;
int main(void)
{
  int intVar; // 与全局的 intVar 不同
  intVar = 5;
}
```

初眼很难看出哪一个版本的 `intVar` 被赋值为 5，但存在一条规则：如果局部变量与全局变量同名，则该局部变量被认为**遮蔽**（shadow）了该全局变量。对该同名变量执行的所有操作都都是在局部变量上执行的。

如果可能的话，最好避免这种情况。如果你的变量名发生冲突，说明设计不佳。请考虑重新组织你的代码。然而，了解你如何处理此类情况是有益的。那么，在这些情况下如何访问全局变量呢？

答案是使用作用域解析运算符。如果你想确保使用变量的全局版本，只需在它前面加上两个冒号（`::`）。例如，为了让前面的代码使用全局版本，请将之前的代码更改为：

```cpp
int intVar;

int main(void)
{
    int intVar;
    ::intVar = 5;
    return 0;
}
```

这种遮蔽效应也会发生在代码块中。例如，如果在 `main` 函数中使用局部变量覆盖全局变量，可以使用作用域运算符来指定全局变量。这里有一个示例：

```cpp
#include <iostream>
#include <string>

using std::cout;

string str = "Humans can coexist.";

int main(void)
{
    using std::cout;
    cout << str << "\n";
    if (true)
    {
        string str = "Humans often live in.";
        cout << str << "\n";
    }
    return 0;
}
```

输出：

Humans can coexist.

Humans often live in.

## 静态变量

有时你可能会发现需要变量在每次调用函数时保持不变。全局变量可以做到，但它们在每次调用函数时都会重新初始化。静态变量的作用域与普通变量相同，但它们的生命周期持续到程序结束。静态变量只初始化一次，并持续到程序结束。你可以使用 `static` 关键字来定义静态变量：

```cpp
static int var;
```

这意味着 `static` 语句只会被执行一次。请看下面的示例：

```cpp
//4.3 - 静态变量示例 - Dirk Henemans and Mark Lee
#include <iostream>

int incrementFunction1(void);
int incrementFunction2(void);

//运行这些函数
int main(void)
{
    using std::cout;
    for(int c = 0; c < 4; c++) {
        cout << "Incrementing both variables.\n";
        cout << "Value of function1 is: " << incrementFunction1() << "\n";
        cout << "Value of function2 is: " << incrementFunction2() << "\n";
    }
    return 0;
}

// 使用静态变量的函数
int incrementFunction1(void)
{
    static int x = 0;
    x++;
    return x;
}

// 使用静态变量的函数
int incrementFunction2(void)
{
    int y = 0;
    y++;
    return y;
}
```

输出：

Incrementing both variables.

Value of function1 is: 1

Value of function2 is: 1

Incrementing both variables.

Value of function1 is: 2

Value of function2 is: 1

Incrementing both variables.

Value of function1 is: 3

Value of function2 is: 1

Incrementing both variables.

Value of function1 is: 4

Value of function2 is: 1

在这个示例中，`x` 和 `y` 都是局部变量。虽然 `x` 是静态的并且初始化一次，但 `y` 在每次调用 `incrementFunction2` 时都会初始化为 0。由于这个原因，`incrementFunction2` 总是返回 1，而 `incrementFunction1` 会持续增加 `x`。

```cpp
switch(userResponse)
{
    case 1:
    case 2:
    case 3:
        money +=
        race(placeBet(userResponse), userResponse);
        break;
    case 4: //用户没有下注
        race();
        break;
}
return 0;
```

//显示主菜单并返回用户的选择

int menu(void)

{

```cpp
using std::cout;
using std::cin;
int userResponse;
cout << "You have " << money << " dollars.\n"
do
{
    cout << "Races Menu\n";
    cout << "1" Bet on snail 1\n";
    cout << "2" Bet on snail 2\n";
    cout << "3" Bet on snail 3\n";
    cout << "4" Just Watch\n";
    cout << "0" Leave the races\n";
    cin >> userResponse;
} while (userResponse < 0 && userResponse > 4);
return userResponse;
```

//决定某人将对蜗牛下注多少

int placeBet(int userResponse)

## 第 4 章 • 使用函数构建你的代码

```cpp
{
using std::cout;
using std::cin;
int betAmount;
cout << "Snail " << userResponse << " is a good choice!\n"
cout << "How much would you like to bet on your snail " 
  << userResponse << " ?";
cin >> betAmount;
return betAmount;
}
```

```cpp
//如果他们只是在比赛
void race(void)
{
    race(0, 0);
}

//如果他们正在下注
int race (int money, int userResponse)
{
using std::cout;
using std::rand;
//存储随机数
int winner = rand() % 3 + 1;
cout << "And the snails are GO!\n"
  << "Look at them GO!!!\n"
  << "The winner is snail " << winner << "\n"
if(winner == userResponse)
{
  cout << "You Win!\n";
  return 2 * money;
}

cout << "You lose " << money << " dollars.\n";
return -1 * money;
}

//处理程序初始化
void init(void)
{
using std::srand;
using std::time;
rand(time(0));
}
```
