
函数定义（如刚才所示）采用以下形式：

```
type name(parameter-declaration-list)
{
   body
}
```

定义中左花括号之前的部分指定返回类型、函数名和参数列表。花括号之间的部分是函数体。

有值函数（即返回值的函数）的返回类型是函数将返回的值的数据类型。有值函数的函数体必须包含以下形式的语句：

```
return expression;
```

有值函数必须使用 return 返回一个值，其中 expression 为要返回的值。

每个参数都代表函数的输入或输出。声明参数时，需写出数据类型和参数名，并用逗号将其与其他参数声明分隔，如下所示：

```
int x, int y
```

调用（或称用）函数 computeMax 时，需传递与参数在数量、顺序和数据类型上对应的实参。例如，以下语句包含对 max 的两次调用：

```
int a = 0;
int b = 0;
int c = 0;
cin >> a >> b >> c;
int largerAB = computeMax(a, b);
cout << "The largest of " << a << ", " << b << ", "
     << "and " << c << " is " << computeMax(largerAB, c) << ".\n";
```

调用函数时，需传递与参数在数量、顺序和数据类型上对应的实参。

按所示形式，computeMax 的定义表明其实参是按值传递的。也就是说，函数会对实参的值（例如 a 和 b）制作局部副本，并在函数定义中出现 x 和 y 的地方使用这些副本。因此，函数无法修改你传递给它的实参。在此示例中，这一限制是可取的，因为 x 和 y 是输入参数，而 computeMax 不会更改它们。

按值传递的实参会在函数内被复制。

或者，实参可以按引用传递。函数不会复制此类实参；相反，每当参数出现在函数定义中时，它都会引用实参的位置。这样，函数就可以更改实参的值，从而实现输出参数。

按引用传递的实参不会被复制，而是在函数内直接访问。

例如，请考虑函数 computeMax 的以下变体：

```
void computeMax(int x, int y, int& larger)
{
   larger = ((x > y) ? x : y);
} // end computeMax
```

computeMax 是一个 void 函数，而非有值函数。也就是说，其返回类型为 void，且不使用 return 语句返回值。4 相反，computeMax 在输出参数 larger 中返回 x 和 y 中较大的一个。紧跟在 larger 的数据类型 int 之后的 & 表示 larger 是一个引用参数。因此，computeMax 将访问并修改与 larger 对应的实参，而函数则会制作并使用与值参数 x 和 y 对应的实参值的副本。

void 函数不使用 return 返回值。

4 而有值函数必须包含形式为 return expression 的语句，void 函数则不能包含此类语句。不过，void 函数可以包含不带表达式的 return。此类语句会导致函数返回到其调用之后的语句。本书不在 void 函数中使用 return。

输出实参应为引用实参。

以下语句演示了如何调用 computeMax：

```cpp
int a = 0;
int b = 0;
int larger = 0;
cin >> a >> b;
computeMax(a, b, larger);
cout << "The larger of " << a << " and " << b
     << " is " << larger << ".\n";
```

输入实参应为值实参或常量引用实参。

如果函数的输入实参是一个大对象（如你将在本书中遇到的对象），你可能不希望函数复制它。因此，你不会按值传递该实参。然而，由于它是输入实参，你也不希望函数能够修改它。常量引用参数是标记为 const 的引用参数。函数使用传递给此类参数的实际实参，而非其副本，但无法修改它。

例如，对于以以下内容开头的函数 f：

```cpp
void f(const int& x, int y, int& z)
```

x 是常量引用参数，y 是值参数，z 是引用参数。在此，x 和 y 适合作为输入参数，因为 f 不能更改它们，而 z 是输出参数。请注意，z 也可以是输入参数。也就是说，与 z 对应的实参既可以向函数提供一个值，也可以从函数返回一个值。此类实参必须按引用传递。

注意：使用引用参数时需谨慎，因为你可能会无意中更改实参。另一方面，常量引用参数可以安全使用。

函数声明以分号结尾。

如果你编写另一个调用 computeMax 的函数 f，则必须将 f 的定义放在 computeMax 的定义之后，或在 f 的定义之前加上 computeMax 的函数声明。例如，你可以使用以下任一语句来声明函数 computeMax：

```cpp
void computeMax(int x, int y, int& max);
```

或

```cpp
void computeMax(int, int, int&);
```

函数声明提供函数参数的数据类型及其返回类型。在函数声明中，参数名是可选的，尽管从风格角度来看它们很有帮助。然而，在函数定义中，参数名是必需的。虽然函数声明以分号结尾，但函数定义中不会出现分号。

每个函数的声明通常出现在程序开头。

典型的 C++ 程序包含程序中每个函数的函数声明。这些声明出现在程序的最前面，通常附有描述每个函数用途、参数和假设的注释。清单 A-1 演示了函数声明、函数定义和 main 函数的位置：

```
LISTING A-1 A program that contains a function declaration
#include <iostream>
using namespace std;
/* Returns the larger of two given integers.
@param x An integer.
@param y An integer.
@return The larger of x and y. */
int computeMax(int x, int y); // A function declaration

int main()
{
    int a = 0;
    int b = 0;
    cout << "Please enter two integers: ";
    cin >> a >> b;

    int largerAB = computeMax(a, b);
    cout << "The larger of " << a << " and " << b
        << " is " << largerAB << ".\n";
} // end main

int computeMax(int x, int y)
{
    return (x > y) ? x : y;
} // end computeMax
```

## A.3.1 标准函数

C++ 提供了许多标准函数，例如平方根函数 sqrt 和输入函数 get。附录 H 对标准函数进行了汇总，并指明你需要在程序中包含哪个头文件才能访问它们。例如，图 A-5 中列出的标准函数有助于字符处理，并需要头文件 cctype。因此，当你想要使用 isupper 和 toupper 等函数时，需要在程序中包含以下语句：

```
#include <cctype>
```

对于字符变量 ch，如果 ch 是大写字母，则 isupper (ch) 为真，而 toupper (ch) 返回字母 ch 的大写版本，但不会实际更改 ch。

## A.4 选择语句

选择语句允许你根据表达式的值在多种行动方案中进行选择。在这类语句中，C++ 提供了 if 语句和 switch 语句。

### A.4.1 if 语句

可以用两种方式编写 if 语句：

```
if (expression)
statement1
```

if 语句有两种基本形式
