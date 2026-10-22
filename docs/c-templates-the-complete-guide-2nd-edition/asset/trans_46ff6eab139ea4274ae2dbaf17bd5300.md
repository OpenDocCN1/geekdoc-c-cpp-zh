

materialization（但它同样可以被称为“prvalue 到 xvalue 转换”）：任何时候 prvalue 在需要 glvalue（包括 xvalue 情况）的地方有效出现时，都会创建一个临时对象并用 prvalue 初始化它（请回忆 prvalue 主要是指“初始化值”），并且 prvalue 被替换为指定该临时对象的 xvalue。例如：int f(int const&);
int r = f(3); 因为 f( ) 在此示例中具有引用参数，所以它期望一个 glvalue 参数。然而，表达式 3 是一个 prvalue。因此“临时 materialization”规则因此生效，表达式 3 被“转换”为指定用值 3 初始化的临时对象的 xvalue。

更一般地，临时对象在以下情况下会被 materialized 以用 prvalue 初始化：

- prvalue 被绑定到引用（例如，上面的 f(3) 调用）。
- 访问类 prvalue 的成员。
- 对数组 prvalue 进行下标访问。
- 数组 prvalue 转换为指向其第一个元素的指针（即数组衰变）。
- prvalue 出现在会为某种类型 X 初始化 std::initializer_list<X> 对象的花括号初始化列表中。
- sizeof 或 typeid 运算符应用于 prvalue。
- prvalue 是形如“expr;”的语句中的顶层表达式，或表达式被强制转换为 void。

因此，在 C++17 中，由 prvalue 初始化的对象始终由上下文决定，并且因此只有在真正需要时才会创建临时对象。在 C++17 之前，prvalue（特别是类类型）总是隐含一个临时对象。那些临时对象的拷贝可以随后选择性地被省略，但编译器仍必须强制执行拷贝操作的大多数语义约束（例如，拷贝构造函数可能需要可调用）。下面的示例展示了 C++17 规则修订的一个后果：Click here to view code image

```
class N {
public:
N();
N(N const&) = delete; // this class is neither copyable ...
N(N&&) = delete; // ... nor movable
};

N make_N() {
return N{}; // Always creates a conceptual temporary prior to C++17.
} // In C++17, no temporary is created at this point.
auto n = make_N(); // ERROR prior to C++17 because the prvalue needs
```
// conceptual copy. OK since C++17, because n is
// initialized directly from the prvalue.

在 C++17 之前，prvalue N{} 会产生一个类型为 N 的临时对象，但编译器被允许省略该临时对象的拷贝和移动（在实践中它们总是这样做）。在这种情况下，这意味着调用 make_N() 的临时结果可以直接构造在 n 的存储中；不需要拷贝或移动操作。不幸的是，C++17 之前的编译器仍必须检查是否可以进行拷贝或移动操作，而在此示例中这是不可能的，因为 N 的拷贝构造函数被删除（并且没有生成移动构造函数）。因此，C++11 和 C++14 编译器必须对此示例发出错误。

使用 C++17，prvalue N 本身不会产生临时对象。相反，它会初始化由上下文决定的对象：在我们的示例中，该对象就是由 n 表示的对象。永远不会考虑拷贝或移动操作（这不是优化，而是语言保证），因此代码是有效的 C++17。

我们以一个展示各种值类别情况的示例作为结尾：Click here to view code image

```
class X {
};
X v;
X const c;

void f(X const&); // accepts an expression of any value category
void f(X&&); // accepts prvalues and xvalues only but is a better match
// for those than the previous declaration
f(v); // passes a modifiable lvalue to the first
f(c); // passes a nonmodifiable lvalue to the first f()
f(X()); // passes a prvalue (since C++17 materialized as xvalue) to the 2nd f()
f(std::move(v)); // passes an xvalue to the second f()
```

## B.3 Checking Value Categories with decltype

使用关键字 decltype（在 C++11 中引入），可以检查任何 C++ 表达式的值类别。对于任何表达式 x，decltype((x))（注意双括号）会产生：
• type 如果 x 是 prvalue
• type& 如果 x 是 lvalue
• type&& 如果 x 是 xvalue
decltype((x)) 中的双括号是必要的，以避免在表达式 x 确实命名一个实体时产生该命名实体的声明类型（在其他情况下，括号没有效果）。例如，如果表达式 x 只是命名一个变量 v，则不带括号的构造变为 `decltype(v)`，它会产生变量 v 的类型，而不是反映表达式 x 引用该变量的值类别的类型。

因此，使用类型特征对于任何表达式 e，我们可以按如下方式检查其值类别：[Click here to view code image](#)

```
if constexpr (std::is_lvalue_reference<decltype((e))>::value) {
  std::cout << "expression is lvalue\n";
}
else if constexpr (std::is_rvalue_reference<decltype((e))>::value) {
  std::cout << "expression is xvalue\n";
}
else {
  std::cout << "expression is prvalue\n";
}
```

有关详细信息，请参阅第 298 页的第 15.10.2 节。

## B.4 Reference Types

C++ 中的引用类型——例如 `int&`——以两种重要方式与值类别交互。第一种是引用可能会限制表达式可以绑定的值类别。例如，非 const 左值引用类型 `int&` 只能用类型为 `int` 的左值表达式初始化。类似地，右值引用类型 `int&&` 只能用类型为 `int` 的右值表达式初始化。

值类别与引用交互的第二种方式是与函数的返回类型相关，其中使用引用类型作为返回类型会影响对该函数的调用的值类别。具体而言：

- 对返回类型为左值引用的函数的调用会产生左值。
- 对返回类型为对象类型的右值引用的函数的调用会产生 xvalue（对函数类型的右值引用的引用始终产生左值）。
- 对返回非引用类型的函数的调用会产生 prvalue。

我们通过以下示例说明引用类型与值类别之间的交互。给定：`int& lvalue();` `int&& xvalue();` `int prvalue();` 任何给定表达式的值类别和类型都可以通过 `decltype` 确定。如第 298 页的第 15.10.2 节所述，它使用引用类型来描述表达式是左值还是 xvalue：Click here to view code image

```
std::is_same_v<decltype(lvalue()), int&> // yields true because result is lvalue
std::is_same_v<decltype(xvalue()), int&&> // yields true because result is xvalue
std::is_same_v<decltype(prvalue()), int> // yields true because result is prvalue
```

因此，以下调用是可能的：Click here to view code image

```
int& lref1 = lvalue(); // OK: lvalue reference can bind to an lvalue
int& lref3 = prvalue(); // ERROR: lvalue reference cannot bind to a prvalue
int& lref2 = xvalue(); // ERROR: lvalue reference cannot bind to an xvalue

int&& rref1 = lvalue(); // ERROR: rvalue reference cannot bind to an lvalue
int&& rref2 = prvalue(); // OK: rvalue reference can bind to a prvalue
int&& rref3 = xvalue(); // OK: rvalue reference can bind to an xrvalue
```

1 用户定义的文字可能导致左值或右值，具体取决于相关文字运算符的返回类型。

2 这不幸意味着这些术语是误称。

3 在 C++11 值类别的世界中，短语 glvalue-to-prvalue 转换会更准确，但传统术语仍然更常见。

## Appendix C

## Overload Resolution

*Overload resolution* 是为给定的调用表达式选择要调用的函数的过程。考虑以下简单示例：[Click here to view code image](#)

```
void display_num(int);    // #1
void display_num(double); // #2

int main()
{
    display_num(399);   // #1 matches better than #2
    display_num(3.99);  // #2 matches better than #1
}
```

在此示例中，函数名 `display_num()` 被称为 *overloaded*。当此名称在调用中使用时，C++ 编译器必须因此使用额外信息在各种候选中进行区分；主要是，此信息是调用参数的类型。在我们的示例中，当函数被整数参数调用时调用 `int` 版本，而当提供浮点参数时调用 `double` 版本，这在直觉上是有意义的。尝试模拟这种直觉选择的正式过程就是重载决议过程。

指导重载决议的规则背后的总体思想很简单，但在 C++ 标准化过程中细节变得相当复杂。这种复杂性主要是由希望支持各种现实世界示例所驱动的，这些示例在直觉上（对人类而言）似乎有“明显最佳匹配”，但在尝试形式化这种直觉时出现了各种细微差别。

在本附录中，我们提供了重载决议规则的相当详细的概述。然而，该过程的复杂性使得我们无法声称涵盖该主题的每个部分。

## C.1 When Does Overload Resolution Kick In?

