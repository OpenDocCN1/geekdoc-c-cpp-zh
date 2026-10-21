

你可以使用联合作为在类型事先未知的情况下传递对象或数据值的一种手段。联合可以提供存储你可能拥有的各种可能类型范围中的任意一种类型。

## 定义联合

你使用关键字 union 来定义一个联合。最好通过一个定义示例来理解它：

```
union shareLD        // Sharing memory between long and double
{
    double dval;
    long lval;
};
```

这定义了一个联合类型 shareLD，它提供 long 和 double 类型的变量占用同一内存。联合类型名通常被称为标签名。这与类定义类似，因为你实际上还没有定义联合实例，所以此时你还没有任何变量。在联合类型定义之后，你可以在声明中定义联合的实例。例如：

```
shareLD myUnion;
```

这定义了之前定义的联合类型 shareLD 的一个实例。你也可以在联合定义语句中包含它来定义 myUnion：

```
union shareLD        // Sharing memory between long and double
{
    double dval;
    long lval;
} myUnion;
```

要引用联合的成员，你使用直接成员选择运算符（句点）与联合实例名，就像你访问类成员时所做的那样。因此，你可以用以下语句将联合实例 myUnion 中的 long 变量 lval 设置为 100：

```
myUnion.lval = 100;        // Using a member of a union
```

在程序后面的某个类似语句中初始化 double 变量 dval 会覆盖 lval。使用联合在同一内存中存储不同类型的值的基本问题是，由于联合的工作方式，你还需要某种手段来确定当前是哪一个成员值有效。这通常通过维护另一个充当存储值类型指示符的变量来实现。

联合不仅限于在两个变量之间共享。如果你愿意，可以在多个变量之间共享同一内存。联合占用的内存是其最大成员所需的内存。例如，假设你定义了这个联合：

```
union shareDLF
{
    double dval;
    long lval;
    float fval;
} uinst = {1.5};
```

shareDLF 的一个实例占用 8 个字节，如图 8-2 所示。

![](img/2359b0c604600c58fba3539c738a356e_450_0.png)

图 8-2

在示例中，你定义了联合的一个实例 uinst，以及联合的标签名。你还用值 1.5 初始化了该实例。

> 在声明实例时，你只能初始化联合的第一个成员。

## 匿名联合

你可以定义一个没有联合类型名的联合，在这种情况下联合的实例会自动声明。例如，假设你像这样定义一个联合：

```
union
{
    char* pval;
    double dval;
    long lval;
};
```

此语句定义了一个没有名称的联合以及一个没有名称的联合实例。因此，你可以通过联合定义中出现的名称 pval、dval 和 lval 直接引用它所包含的变量。这比使用类型名的普通联合更方便，但你需要小心不要将联合成员与普通变量混淆。联合的成员仍然共享同一内存。作为说明，上面匿名联合的工作方式，使用 double 成员，你可以写下这个语句：

```
dval = 99.5;    // Using a member of an anonymous union
```

正如你所见，没有任何东西能将变量 dval 与其作为联合成员区分开来。如果你需要使用匿名联合，你可以使用命名约定使成员更明显，从而使你的代码不易被误解。

## 类和结构中的联合

你可以在类或结构中包含联合实例。如果你打算在不同时间存储不同类型的值，这通常需要维护一个类数据成员来指示联合中存储的是何种值。使用联合作为类或结构体成员通常并不会带来太多好处。

## 运算符重载

**运算符重载** 是一个非常重要的功能，因为它使你能够让标准 C++ 运算符，如 +、-、* 等，与你自己的数据类型对象一起工作。它允许你编写一个函数重新定义特定运算符，以便在它与类对象一起使用时执行特定操作。例如，你可以重新定义运算符 >，使其在使用类 CBox 的对象时，如果第一个 CBox 参数的体积大于第二个，则返回 true。

运算符重载不允许你发明新运算符，也不能改变运算符的优先级，因此你重载的运算符在表达式求值序列中的优先级与原始基础运算符相同。运算符优先级表可以在本书第 2 章和 MSDN 库中找到。

虽然你不能重载所有运算符，但限制并不特别苛刻。以下是不允许重载的运算符：

- 作用域解析运算符 ::
- 条件运算符 ?:
- 直接成员选择运算符 .
- sizeof 运算符
- 解引用指向类成员的指针运算符 .*

其他一切都是可以的，这给了你很大的发挥空间。显然，确保你的标准运算符版本与它们的正常用法合理一致，或者至少在操作上合理直观，是一个好主意。用一个对类对象执行类乘法等效操作的类来生成重载的 + 运算符并不是一个明智的做法。理解运算符重载如何工作的最好方法是举例说明，所以让我们实现我刚才提到的，类 CBox 的大于运算符 >。

### 实现重载运算符

要为类实现重载运算符，你必须编写一个特殊函数。假设它是类 CBox 的成员，在类定义中重载 > 运算符的函数声明如下：

```
class CBox
{
    public:
        bool operator>(const CBox& aBox) const;  // Overloaded 'greater than'
    // Rest of the class definition...
};
```

这里的 operator 是关键字。结合运算符符号或名称，在本例中为 >，它定义了一个运算符函数。在本例中函数名为 operator>()。你可以在 operator 关键字和运算符本身之间有或没有空格来编写运算符函数，只要没有歧义即可。歧义出现在运算符具有名称而非符号的情况，如 new 或 delete。如果你写 operatornew 和 operatordelete 而不加空格，它们是普通函数的合法名称，因此对于这些运算符的运算符函数，你必须在 operator 关键字和运算符名称本身之间留一个空格。请注意，你将 operator>() 函数声明为 const，因为它不修改类的数据成员。

对于 operator>() 运算符函数，运算符的右操作数由函数参数定义。左操作数由指针 this 隐式定义。因此，如果你有以下 if 语句：

```
if(box1 > box2)
    cout << endl << "box1 is greater than box2";
```

if 中的表达式将调用我们的运算符函数，等价于以下函数调用：

```
box1.operator>(box2);
```

表达式中 CBox 对象与运算符函数参数之间的对应关系如图 8-3 所示。

![](img/2359b0c604600c58fba3539c738a356e_452_0.png)

图 8-3

让我们看看 operator>() 函数的代码如何工作：

```
// Operator function for 'greater than' which
// compares volumes of CBox objects.
bool CBox::operator>(const CBox& aBox) const
{
    return this->Volume() > aBox.Volume();
}
```

你使用对函数的引用参数来避免函数调用时不必要的复制。因为函数不改变调用它的对象，所以你可以将其声明为 const。如果你不这样做，就完全无法使用该运算符比较类型为 CBox 的 const 对象。

返回表达式使用成员函数 Volume() 计算指针 this 所指向的 CBox 对象的体积，并使用基础运算符 > 将结果与对象 aBox 的体积进行比较。基础 > 运算符返回类型为 int（而不是 bool）的值，因此如果指针 this 所指向的 CBox 对象的体积大于作为引用参数传递的对象 aBox，则返回 1，否则返回 0。比较结果将自动转换为运算符函数的返回类型 bool。

### 试一试 运算符重载

你可以用一个示例来练习 operator>() 函数：

```
// Ex8_03.cpp
// Exercising the overloaded 'greater than' operator
#include <iostream>                // For stream I/O
using std::cout;
using std::endl;

class CBox                         // Class definition at global scope
{
public:
    // Constructor definition
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0):
        m_Length(lv), m_Width(wv), m_Height(hv)
    {
        cout << endl << "Constructor called.";
    }

    // Function to calculate the volume of a box
    double Volume() const
    {
        return m_Length*m_Width*m_Height;
    }

    bool operator>(const CBox& aBox) const;  // Overloaded 'greater than'

    // Destructor definition
    ~CBox()
    {
        cout << "Destructor called." << endl;
    }
