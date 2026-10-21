

> 使用 `using namespace ::element` 的语法称为 using 声明。

## using Declaration

using 声明遵循 `namespace::element` 语法，用于仅使给定命名空间的元素可用。看下面的代码：

//usingDeclaration.cpp
#include <iostream>

// NO "using namespace std"
int main()
{
	using std::cout;
	using std::operator <<;
	cout << "Hi";
	return 0;
}
```

此代码中并未指定通常的 `using namespace std;`；然而，我们仍能将 `cout` 作为普通的 ostream 对象使用。这是因为已为 `cout` 对象以及在 `cout` 中重载的运算符 `<<` 提供了 using 声明。

以下语句被视为 using 声明。

- using std::cout;
- using std::operator <<;

> 语法 `using namespace namespace` 是 using 指令的示例。

## using Directive

通常的 `using namespace std;` 语句被称为 using 指令。请注意，单词 `namespace` 已包含在定义中。这使得 `std` 命名空间中定义的所有名称都可用于全局命名空间。这是使用命名空间的最简单机制。我们将在第 14.3.1 节看到如何定义用户定义的命名空间。假设已定义了一个名为 `mynamespace` 的命名空间。using 指令的示例如下：

- using namespace std;
- using mynamespace;

看一下指令和声明之间的区别。指令将整个命名空间引入全局命名空间，而声明只引入程序员想要使用的对象。

## Code without using Directive or Declaration

看下面的程序：

//WithoutUsing.cpp
#include <iostream>
// NO "using namespace std"
int main()
{
	using std::operator <<;
	std::cout << "Hi";
	return 0;
}
```

当我们使用完全限定的名称如 `std::cin` 时，我们不需要 using 指令或声明。

> 当我们使用完全限定的名称如 `std::cin` 时，我们不需要 using 指令或声明。

```
string MyString;
}
int main()
{
    using MyNamespace::MyNumber;
    using MyNamespace::MyString;
    cin >> MyNumber;
    cin >> MyString;
    cout << MyNumber << endl;
    cout << MyString << endl;
}
```

```
//UsingDirectiveMyNameSpace.cpp
#include <iostream>
#include <string>
using namespace std;

namespace MyNamespace
{
    int MyNumber;
    string MyString;
}

int main()
{
    using namespace MyNamespace;
    cin >> MyNumber;
    cin >> MyString;
    cout << MyNumber << endl;
    cout << MyString << endl;
}
```

> 与 `std` 命名空间类似，using 指令和声明也适用于用户定义的命名空间。

## 14.3.2 Defining Functions Inside a Namespace

除了变量，命名空间也可以容纳函数。可以将函数定义在命名空间内部并使用相同技术访问它们。下面的程序说明了如何做到这一点。

```
//DefiningFunctions.cpp
#include <iostream>
#include <string>
using namespace std;

namespace MyNamespace
{
    int MyNumber;
    string MyString;
    void InputAndDisplay()
    {
```

```
cin >> MyNumber;
cin >> MyString;
cout << MyNumber << endl;
cout << MyString << endl;
```

```
int main()
{
MyNamespace::InputAndDisplay();
}
```

> 可以在命名空间内部定义一个函数并使用完全限定的名称调用它。

注意函数是如何被调用的。它与变量一样是完全限定的，使用命名空间和函数名。可以利用 using 指令或声明来访问命名空间内部定义的函数。

甚至可以在命名空间内部定义类。看程序 14.1。

## PROGRAM 14.1 Defining classes inside a namespace

```
//DefineClassOutsideNS.cpp
#include <iostream>
#include <string>
using namespace std;

namespace MyNamespace
{
class brother
{
string Name;
public:
brother(string BrotherName)
{
Name = BrotherName;
}
friend ostream & operator <<(ostream &TempOut, brother TempBrother);
};
ostream & operator <<(ostream &TempOut, brother TempBrother)
{
TempOut << TempBrother.Name;
return TempOut;
}
}

int main()
{
MyNamespace::brother Lara("Brian Charles Lara");
cout << Lara;
}
```

> 当一个类在命名空间内部定义时，可以使用 `namespace::classname` 在该命名空间外部访问该类。

## How the Program Works

`brother` 类现在定义在 `MyNamespace` 内部并像其他变量一样被访问。定义 `brother` 类的对象是通过以下语句完成的：

```
MyNamespace::brother Lara("Brian Charles Lara");
```

即，完全限定类名并使用它。也可以像前面的程序中使用 using 声明或指令。

```
// using directive
int main()
{
    using namespace MyNamespace;
    brother Lara("Brian Charles Lara");
    cout << Lara;
}
```

```
// using declaration
int main()
{
    using MyNamespace::brother;
    brother Lara("Brian Charles Lara");
    cout << Lara;
}
```

在这两种情况下，运算符 `<<` 都是在不加限定使用的，即代码中不包含语句 `using MyNamespace::operator <<`。那它是如何工作的呢？这在第 14.8 节中解释，我们在那里讨论 Koenig 查找。

## 14.3.4 Declaring Inside and Defining Outside the Namespace

与类定义类似，可以在命名空间内部声明一个元素并在外部定义它。在下面的程序中，函数 `InputAndDisplay()` 在命名空间外部定义。

```
//DefineOutsideNS.cpp
#include <iostream>
#include <string>
using namespace std;

namespace MyNamespace
{
    int MyNumber;
    string MyString;
    void InputAndDisplay(); // Declaration
}
/* Qualifying the function name and defining it outside */
void MyNamespace::InputAndDisplay()
{
    cin >> MyNumber;
    cin >> MyString;
    cout << MyNumber << endl;
```

```
cout << MyString << endl;
}

int main()
{
    using namespace MyNamespace;
    InputAndDisplay();
}
```

> 当函数在命名空间外部定义时，需要限定。

需要注意的是，函数的定义位于命名空间外部，因此需要限定。之前在命名空间内部定义时则不需要。

程序 14.2 展示了如何在命名空间外部定义类成员函数。然而，与非成员函数类似，其声明必须在命名空间内部完成。

## PROGRAM 14.2 Define a member function outside the namespace

```
//DefineClassOutsideNS2.cpp
#include <iostream>
#include <string>
using namespace std;

namespace MyNamespace
{
    class brother
    {
        string Name;
    public:
        brother(string BrotherName);  // Compulsory declaration
        friend ostream & operator <<(ostream & TempOut, brother TempBrother);
    };
}
MyNamespace::brother::brother(string BrotherName)
{
    MyNamespace::brother::Name = BrotherName;
}
std::ostream & MyNamespace::operator <<(ostream & TempOut, MyNamespace::brother TempBrother)
{
    TempOut << TempBrother.Name;
    return TempOut;
}
int main()
{
    MyNamespace::brother Lara("Brian Charles Lara");
    cout << Lara;
}
```

## How the Program Works

构造函数现在定义如下：

```
MyNamespace::brother::brother(string BrotherName)
```

此外，变量赋值如下：

```
MyNamespace::brother::Name = BrotherName;
```

> 可以通过使用相同名称在命名空间内部定义额外组件来扩展命名空间。

这两个构造看起来都很长。减少它们长度的一种方法是使用 using 声明或指令。还有另一种方法可以解决这个问题。它被称为命名空间别名。我们将在第 14.6 节学习它。

## 14.3.5 Extending a Namespace

可以扩展先前定义的命名空间。看程序 14.3。在什么情况下需要此功能？大型项目通常涉及多个开发者。他们都可以开发自己命名空间的一部分，如果他们使用相同的命名空间名称为自己的部分定义，那么在程序代码中插入时就会累加。

## PROGRAM 14.3 Extending a namespace

```cpp
//ExtendingNamespace.cpp
#include <iostream>
#include <string>
using namespace std;

namespace MyNamespace
{
    class brother
    {
        string Name;
    public:
        brother(string BrotherName)
        {
            Name = BrotherName;
        }
        friend ostream & operator <<(ostream &TempOut, brother TempBrother);
    };
    ostream & operator <<(ostream &TempOut, brother TempBrother)
    {
        TempOut << TempBrother.Name;
        return TempOut;
    }
}

/* This definition extends the previous definition; does not overwrite it */
namespace MyNamespace
{
    int Test = 20;
}

int main()
{
    MyNamespace::brother Lara("Brian Charles Lara");
    cout << Lara;
    cout << endl << MyNamespace::Test;
}
```

## How the Program Works

如程序所示，第二个定义扩展了之前的定义。在某些情况下这非常有用。可以有如下代码：

```cpp
#include <FirstHeaderFile>
```
