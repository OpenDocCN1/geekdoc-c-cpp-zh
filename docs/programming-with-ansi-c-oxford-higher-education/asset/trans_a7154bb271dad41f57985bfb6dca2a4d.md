

```cpp
template <typename Type = int> // This is incorrect
```

令人惊讶的是，这在类模板中是允许的。这是因为模板函数的默认参数提议得太晚，标准化委员会来不及接受。

## Efficiency

我们已经看到了模板的用处。模板设计者的目标之一是效率。让我们看看使用模板的效率如何。模板的第一个问题是它可能以意想不到的方式膨胀代码。

假设我们有以下三个数组：

```cpp
int IntArray[10];
short ShortArray[10];
char CharArray[10];
```

以及调用 `GenericBubbleSort(IntArray)`、`GenericBubbleSort(ShortArray)`、`GenericBubbleSort(CharArray)`，那么将生成三个不同的函数。实际上，一个以 `int` 作为参数的单个函数就可以胜任此目的。如果我们必须用此类数据类型解决一个问题，则不建议使用模板函数。

另一个需要注意的点是，与模板相关的所有操作都是在编译时完成的。因此，使用模板时几乎没有运行时的开销。

## Flexibility

灵活性是使用函数模板的一个重要优点，它可用于内置类型以及用户定义的类型。已经提到过，如果算法要与对象作为参数一起使用，则可能需要重载运算符。算法只有在为给定对象有意义地重载了适当的运算符时才灵活。例如，`BubbleSort(CompArray, size)` 只有在 `<` 和 `=` 被定义时才有用且正确。

## 7.3 Class Templates

我们迄今为止已经看到了通用函数及其用途。同样，在 C++ 中也可能存在接受数据类型作为参数的通用类。可以定义一个栈类，它具有栈的所有可能功能。栈类的对象可以定义如下：

```cpp
Stack <int> MyIntStack;
```

这里，栈类的内容类型为整数。也可以有 `Stack <char>`、`Stack <employee>` 等。如何构建这种功能？程序 7.9 使用了第 3 章程序 3.2 中使用的相同栈，但现在使用的是通用类型元素。

### Program 7.9 Generic stack class

```cpp
//GenericStackClass.cpp
#include <iostream>
using namespace std;
template <typename ElementType>
```

无法对类模板进行类型推导。我们必须在定义类时显式指定类型。

`template <typename ElementType>` 在类定义之前，以便类在其主体中使用 `ElementType` 作为通用类型。

- 定义 `Stack MyStack` 变为 `Stack <int> MyStack`。
- `push` 的 `int` 元素类型参数和 `pop` 的返回类型在此处已被 `ElementType` 替换。

也可以像 int 栈一样拥有 char 栈和 employee 栈。可以观察到，程序在 Stack 类定义中不会有任何变化。

需要注意的是，在类模板中不可能进行自动参数推导，因为编译器无法从诸如 `Stack Mystack` 的对象声明中推导出类型。这与函数调用不同，在函数调用中存在参数和推导，可能告诉编译器 Type 的数据类型。

### 7.3.1 Defining Functions of Class Templates outside the Class

如果 `push()` 和 `pop()` 在类外定义，类 `Stack` 将必须按如下方式定义：

```cpp
template <typename ElementType>
class Stack
{
private:
    int StackPointer;
    ElementType StackArray[10];
public:
    Stack()
    {
        StackPointer = 0;
    }
    void push(ElementType);
    ElementType pop();
};
```

```cpp
template <typename ElementType>
void Stack <ElementType>::push(ElementType value)
{
    if(StackPointer == 9)
    {
        cout << "Stack overflow! Cannot insert";
    }
    else
    {
        StackArray[StackPointer] = value; StackPointer++;
    }
}
```

```cpp
template <typename ElementType>
ElementType Stack <ElementType>::pop()
{
    if(StackPointer == 0)
        cout << "Stack underflow! Cannot pop";
    else
    {
        StackPointer--;
        return StackArray[StackPointer];
    }
}
```

函数头部的语法乍一看似乎很晦涩。函数头部前面有 `template <...>`，这与之前在类定义前出现的模板规范相同。类名（例如 `Stack`）也应使用相同的 `<>` 对来指示类中使用的类型变量（例如 `int`），以指示名称，即 `Stack <int>`。请注意，模板规范包含 `typename`（已经提到它也可以是关键字 `class` 而不是 `typename`）后跟类型变量名（例如 `typename ElementType`）。类部分将只有类型（例如程序 7.9 中的 `ElementType`）。

在程序 7.10 中，函数已移出模板类，并引入了 Employee 栈。

### Program 7.10 Employee stack

```cpp
//EmpStack.cpp
#include <iostream>
#include <string>
using namespace std;

class employee
{
int EmpNo;
string Name;
string DeptName;
string Designation;
public:
employee(){};
employee(int TempNo, string TempName, string TempDept, string TempDesi)
{
EmpNo = TempNo;
Name = TempName;
DeptName = TempDept;
Designation = TempDesi;
}

friend ostream & operator <<(ostream &TempOut, employee &TempEmployee);
};

ostream & operator <<(ostream & TempOut, employee & TempEmployee)
{
TempOut << "Details of employee number" << TempEmployee.EmpNo << "\n";
TempOut << "Name is" << TempEmployee.Name << "\n";
TempOut << "Department is" << TempEmployee.DeptName << "\n";
TempOut << "Designation is" << TempEmployee.Designation << "\n";
return TempOut;
}

template <typename ElementType>
class Stack
{
private:
int StackPointer;
ElementType StackArray[10];
public:
Stack()
{
StackPointer = 0;
}
void push(ElementType);
ElementType pop();
};

template <typename ElementType>
void Stack <ElementType>::push(ElementType value)
{
if(StackPointer > 9)
{
cout << "Stack overflow! Cannot insert";
}
else
{
StackArray[StackPointer] = value; StackPointer++;
}
}

template <typename ElementType>
ElementType Stack <ElementType>::pop()
{
if(StackPointer == 0)
cout << "Stack underflow! Cannot pop";
else
{
StackPointer--;
return StackArray[StackPointer];
}
}

void main()
{
Stack <int> MyStack;
MyStack.push(1);
MyStack.push(2);
cout << MyStack.pop() << "\n";
cout << MyStack.pop() << "\n";
Stack <char> YourStack;
YourStack.push('n');
YourStack.push('o');
cout << YourStack.pop() << "\n";
cout << YourStack.pop() << "\n";
Stack <employee> EmpStack;
employee UniEmployee[10] =
{
employee(1, "Lara", "Exam", "Professor"),
employee(2, "Ponting", "Marksheet", "Clerk"),
employee(3, "Laxman", "Accounts", "Head Clerk"),
employee(4, "Flintoff", "Exam", "Clerk"),
employee(5, "Murlidharan", "Accounts", "CAO"),
employee(6, "Sarfaraz", "Exam", "Informer"),
employee(7, "Dean Jones", "Exam", "Invigilator"),
employee(8, "Madugalie", "Exam", "Examiner"),
employee(9, "Ganguly", "Marksheet", "Repeater"),
employee(10, "Nafees", "Accounts", "Clerk")
};

for(int i = 0; i < 10; i++)
{
    EmpStack.push(UniEmployee[i]);
}

for(int i = 0; i < 10; i++)
{
    cout << EmpStack.pop();
}
}
```

### How the Program Works

我们将看到通用类如何从中生成真实类并在程序中使用。

### Constructing a class

让我们看看类 stack 如何用作 int 栈以及 char 栈。与函数模板类似，当类模板被定义时，即当 `template <typename ElementType>` 被定义时，它会通知编译器以下类定义包含一个名为 `ElementType` 的通用数据类型。这并不会定义类，因为没有生成函数，也没有创建元素。这也表明当类在主程序中实际定义时，`ElementType` 的类型将被知道。

程序中栈的定义 `Stack <int> MyStack` 表明 `int` 作为类型传递给模板类。编译器仅在定义此类对象时才创建类。它在那一刻创建 `Stack` 类模板的整数版本（称为 `Stack <int>`）。它还创建该类的一个对象（`MyStack`）。因此，类和对象是同时创建的。

### Generating the second class

当编译器遇到 `Stack <char> YourStack` 时，它会创建另一个类，即 Stack 的 char 版本以及该类的一个对象（`YourStack`）。此过程（从模板类生成普通类）称为实例化。这里称为从类模板的类实例化。`Stack <int>` 和 `Stack <char>` 都称为特化（实例化）。现在，如果我们再有一个定义 `Stack <char> YourStack2`，编译器将不会生成新的类，即它不会从 `Stack` 模板生成新的特化，因为它已经实例化了 `Stack <char>`。它只会创建类 `Stack <char>` 的一个对象（`YourStack2`）。

### Explicit specialization

如果 `Stack <employee>` 类要与 `Stack` 模板的行为不同，则可以将其定义为显式特化，就像对模板函数所做的那样。

程序 7.11 是显式类特化的一个例子。不是将完整的 employee 对象插入栈中，而是插入 employee 对象的员工编号。当元素被弹出时，需要搜索数组以获取具有相同员工编号的 employee 对象。此解决方案存储高效，但由于涉及搜索操作，执行时间会更长。

> 从通用类为特定数据类型生成普通类称为实例化，所生成的类称为特化。

