
Array 类，你将确实理解对象技术的本质——创建、使用和重用有价值的类。

本章以讨论如何在类型之间进行转换（包括类类型）、某些隐式转换的问题以及如何防止这些问题作为结尾。

## 18.2 使用标准库类 string 的重载运算符

图 18.1 演示了类 string 的许多重载运算符以及其他几个有用的成员函数，包括 empty、substr 和 at。函数 empty 判断一个字符串是否为空，函数 substr 返回表示现有字符串的一部分的字符串，而函数 at 返回字符串中特定索引处的字符（在检查索引是否在范围内之后）。

```
    1  // Fig. 18.1: fig18_01.cpp
    2  // Standard Library string class test program.
    3  #include <iostream>
    4  #include <string>
    5  using namespace std;
    6
    7  int main()
    8  {
    9      string s1( "happy" );
    10     string s2( " birthday" );
    11     string s3;
    12
    13     // test overloaded equality and relational operators
    14     cout << "s1 is \"" << s1 << "\"; s2 is \"" << s2
    15          << "\"; s3 is \"" << s3 << "\""
    16          << "\n\nThe results of comparing s2 and s1:"
    17          << "\ns2 == s1 yields " << ( s2 == s1 ? "true" : "false" )
    18          << "\ns2 != s1 yields " << ( s2 != s1 ? "true" : "false" )
    19          << "\ns2 >  s1 yields " << ( s2 >  s1 ? "true" : "false" )
    20          << "\ns2 <  s1 yields " << ( s2 <  s1 ? "true" : "false" )
    21          << "\ns2 >= s1 yields " << ( s2 >= s1 ? "true" : "false" )
    22          << "\ns2 <= s1 yields " << ( s2 <= s1 ? "true" : "false" );
    23
    24     // test string member-function empty
    25     cout << "\n\nTesting s3.empty():" << endl;
    26
    27     if ( s3.empty() )
    28     {
    29         cout << "s3 is empty; assigning s1 to s3;" << endl;
    30         s3 = s1; // assign s1 to s3
    31         cout << "s3 is \"" << s3 << "\"";
    32     } // end if
    33
    34     // test overloaded string concatenation operator
    35     cout << "\n\ns1 += s2 yields s1 = ";
```

图 18.1 | 标准库 string 类测试程序。（第 1 部分，共 3 部分。）

s2 >= s1 的结果为 false
s2 <= s1 的结果为 true

测试 s3.empty()：
s3 为空；将 s1 赋给 s3；
s3 为 "happy"

s1 += s2 得到 s1 = happy birthday

s1 += " to you" 得到
s1 = happy birthday to you

s1 从位置 0 开始的 14 个字符的子串，s1.substr(0, 14)，是：
happy birthday

s1 从位置 15 开始的子串，s1.substr(15)，是：
to you

s4 = happy birthday to you

将 s4 赋给 s4
s4 = happy birthday to you

s1 在执行 s1[0] = 'H' 且 s1[6] = 'B' 之后为：Happy Birthday to you

尝试将 'd' 赋给 s1.at( 30 ) 得到：
发生异常：无效的字符串位置

**图 18.1** | 标准库 string 类测试程序。（第 3 部分，共 3 部分。）

行 9–11 创建了三个 `string` 对象——`s1` 用字面量 "happy" 初始化，`s2` 用字面量 " birthday" 初始化，而 `s3` 使用默认的 `string` 构造函数创建一个空字符串。行 14–15 使用 `cout` 和 `operator <<` 输出这三个对象，而 `string` 类的设计者重载了该运算符以处理 `string` 对象。然后行 16–22 通过使用类 `string` 的重载相等运算符和关系运算符比较 `s2` 与 `s1` 的结果，这些运算符执行按字典顺序的比较（即像字典排序一样），使用每个 `string` 中字符的数值（参见附录 B，ASCII 字符集）。

类 `string` 提供了成员函数 `empty` 来判断一个 `string` 是否为空，我们在行 27 中演示了它。成员函数 `empty` 如果 `string` 为空则返回 `true`；否则返回 `false`。

行 30 通过将 `s1` 赋给 `s3` 演示了类 `string` 的重载拷贝赋值运算符。行 31 输出 `s3` 以证明赋值正确完成。

行 36 演示了类 `string` 用于字符串连接的重载 `+=` 运算符。在此情况下，`s2` 的内容被追加到 `s1`。然后行 37 输出存储在 `s1` 中的结果字符串。行 41 演示了使用 `operator +=` 可以将字符串字面量追加到 `string` 对象。行 42 显示结果。

类 `string` 提供了成员函数 `substr`（行 47 和 52）以将 `string` 的一部分作为 `string` 对象返回。行 47 中对 `substr` 的调用获取 `s1` 从位置 0（由第一个参数指定）开始的 14 个字符的子串（由第二个参数指定）。行 52 中对 substr 的调用获取从 s1 的位置 15 开始的子串。当未指定第二个参数时，substr 返回对其调用的字符串的剩余部分。

行 55 创建字符串对象 s4 并用 s1 的副本初始化它。这会导致对类 string 的拷贝构造函数调用。行 60 使用类 string 的重载拷贝赋值 (=) 运算符来演示它能正确处理自赋值——我们将在本章后面构建类 Array 时看到，自赋值可能是危险的，我们将展示如何处理这些问题。

行 64-65 使用类 string 的重载 [] 运算符创建左值，从而使新字符能够替换 s1 中的现有字符。行 67 输出 s1 的新值。类 string 的重载 [] 运算符不执行任何边界检查。因此，你必须确保使用标准类 string 的重载 [] 运算符的操作不会意外地操作字符串边界之外的元素。类 string 在其成员函数 at 中确实提供了边界检查，如果其参数是无效下标则抛出异常。如果下标有效，函数 at 返回指定位置的字符作为可修改的左值或不可修改的左值（例如 const 引用），具体取决于调用出现的上下文。行 73 演示了使用无效下标调用函数 at；这会抛出 out_of_range 异常。

## 18.3 运算符重载的基础

如图 18.1 所示，运算符为操作字符串对象提供了简洁的记法。你也可以将运算符与自己的用户定义类型一起使用。虽然 C++ 不允许创建新运算符，但它允许大多数现有运算符被重载，以便在与对象一起使用时具有适合这些对象的含义。

运算符重载不是自动的——你必须编写运算符重载函数来执行所需操作。运算符通过编写非静态成员函数定义或非成员函数定义来重载，与你通常编写的方式相同，只是函数名以关键字 operator 开头，后跟被重载运算符的符号。例如，函数名 operator+ 将用于重载加法运算符 (+) 以供特定类（或枚举）的对象使用。当运算符作为成员函数重载时，它们必须是非静态的，因为它们必须在类的对象上调用并操作该对象。

要在类的对象上使用运算符，你必须为该类定义重载的运算符函数——有三个例外：
- 赋值运算符 (=) 可以与大多数类一起使用以执行数据成员的逐成员赋值——每个数据成员都从赋值的“源”对象（在右侧）赋给“目标”对象（在左侧）。对于具有指针成员的类，逐成员赋值是危险的，因此我们将显式重载此类类的赋值运算符。
- 地址 (&) 运算符返回指向对象的指针；该运算符也可以被重载。
- 逗号运算符先计算其左侧的表达式，然后计算右侧的表达式，并返回后者表达式的值。该运算符也可以被重载。
