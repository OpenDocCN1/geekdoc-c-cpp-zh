

```cpp
int GenericSearch(Type TempGenericArray[], Type EleToBeSearched)
{
for(int i = 0; i < 10; i++)
{
if(EleToBeSearched == TempGenericArray[i])
return i;
}
return -1;
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
cout << "Stack overflow! Cannot insert!";
else
StackArray[StackPointer] = value;
StackPointer++;
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

template <>
class Stack <employee>
{
private:
int StackPointer;
int EmpNoArray[10];
public:
Stack()
{
StackPointer = 0;
}
void push(employee);
}
```

```cpp
employee pop();
};

template <>
void Stack <employee>::push(employee TempEmp)
{
    if(StackPointer > 9)
        cout << "Stack overflow! Cannot insert";
    else
    {
        EmpNoArray[StackPointer] = TempEmp.EmpNo;
        StackPointer++;
    }
}

template <>
employee Stack <employee>::pop()
{
    if(StackPointer == 0)
        cout << ".Stack underflow! Cannot pop";
    else
    {
        StackPointer--;
        int TempEmpNo = EmpNoArray[StackPointer];
        int SearchIndex = GenericSearch(UniEmployee, employee TempEmpNo " , " );
        return UniEmployee [SearchIndex];
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
    YourStack.push('0');
    cout << YourStack.pop() << "\n";
    cout << YourStack.pop() << "\n";

    Stack <employee> EmpStack;
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

## 程序的工作原理

通用搜索例程 我们添加了一个通用搜索例程，它可以对任何数组进行排序。员工编号（EmpNo）需要定义为 public 且员工数组为全局，以便搜索例程可以对其进行操作。在为真实世界问题编程时，这些解决方案是不可接受的。最好有一个员工编号的链表，并且访问函数应定义为友元，而不是将员工编号定义为 public。然而，由于这里的重点是学习特化，我们以这种方式呈现了程序。

## 生成 Stack <employee>

当 Stack <employee> 被编译时，编译器不会自动从 Stack 模板生成类，而是会采用已明确提供的定义并生成该类。

## 使用单独的类

完成相同任务的另一种方法是定义一个特殊类 StackEmp，其中包含相同的定义。然后，可以编写

```
StackEmp EmpStack;
```

而不是

```
Stack <employee> EmpStack.
```

区别不在于定义或使用，而在于编译器的处理方式。对于 StackEmp，编译器在编译 StackEmp 的定义时生成该类并为其生成 push 和 pop。在前一种情况下，只有在定义了 Stack <employee> 的对象时，类才会被实例化，并且函数只有在被调用时才会存在，否则不会存在。

如果员工栈被定义为模板特化，用户无需了解员工栈作为特殊实现的方式，可以将员工栈对象与其他对象类似地对待。这增加了使用程序库（其中定义了栈类）的用户操作的简便性。

因此，如果用户需要生成一个整数栈，可以写下以下内容：

```
Stack <int>
```

此外，如果需要员工栈，用户只需写下

```
Stack <employee>
```

无需学习其他任何内容。相反，如果我们有一个 StackEmp 类，用户必须记住名称 StackEmp 才能实例化对象。

## 7.3.2 具有多个通用数据类型的类

类与函数模板类似，可以具有一个以上的通用类型。以下程序支持这一事实。

//TwoGenericTypes.cpp
#include <iostream>
#include <string>
using namespace std;

template <typename Type1, typename Type2>
class ClassWithTwoTypes
{
    Type1 FirstValue;
    Type2 SecondValue;

public:
    ClassWithTwoTypes(Type1 TempVal1, Type2 TempVal2)
    {
```

```
{
    cout << "Subscript out of range!";
    exit(1);
}
else
    return Array[Index];
}
};
void main()
{
    SafeGenericArray <int, 5> SafeIntArray;
    SafeGenericArray <char, 3> SafeCharArray;
    int i = 5;
    // SafeGenericArray <char, i> NotAcceptable;
    SafeIntArray[0] = 5;
    // SafeArray[-3] = 7;
    SafeCharArray[5] = 'j';
}
```

> 非类型参数的值在编译时被替换。

非类型参数的使用现在应该清楚了。main() 中的前两个语句中的值五和三将在编译时替换通用数组的 Size。第四行将不会被编译，因为 i 的值在编译期间不可用。如果我们查看模板类的定义，Size 看起来是类型为 int 的变量。然而，它是一个必须在编译时已知的常量值。这适用于所有非类型参数。

## 7.3.4 使用默认参数

模板类可以使用默认参数。之前的示例可以用默认参数重写如下：

//DefArgsGenFunc.cpp
#include <iostream>
using namespace std;
template <typename Type = int, int Size = 10>
// 注意默认参数的使用
class SafeGenericArray
{
    Type Array[Size];
public:
    Type & operator [](int Index)
    {
        if((Index < 0) || (Index > Size - 1))
        {
            cout << "Subscript out of range!";
            exit(1);
        }
    }
```

class Stack
{
private:
    int StackPointer;
    ElementType StackArray[10];
public:
    static int TotalStacks;
    Stack()
    {
        StackPointer = 0;
        TotalStacks++;
    }
    void push(ElementType);
    ElementType pop();
};

template <typename ElementType>
int Stack <ElementType>::TotalStacks;

template <typename ElementType>
void Stack <ElementType>::push(ElementType value)
{
    if(StackPointer > 9)
    {
        cout << "Stack overflow! Cannot insert";
    }
    else
    {
        StackArray[StackPointer] = value;
        StackPointer++;
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
    Stack <int> MyStack1;
    cout << "Integer stack total elements = " << Stack <int>::TotalStacks << "\t";
```

```
cout << "Character stack total elements = " << Stack <char>::TotalStacks << "\n";
Stack <char> YourStack1;
cout << "Integer stack total elements = " << Stack <int>::TotalStacks << "\t";
cout << "Character stack total elements = " << Stack <char>::TotalStacks << "\n";
Stack <int> MyStack2;
cout << "Integer stack total elements = " << Stack <int>::TotalStacks << "\t";
cout << "Character stack total elements = " << Stack <char>::TotalStacks << "\n";
Stack <char> YourStack2;
cout << "Integer stack total elements = " << Stack <int>::TotalStacks << "\t";
cout << "Character stack total elements = " << Stack <char>::TotalStacks << "\n";
getchar();

```

```
Integer stack total elements = 1 Character stack total elements = 0
Integer stack total elements = 1 Character stack total elements = 1
Integer stack total elements = 2 Character stack total elements = 1
Integer stack total elements = 2 Character stack total elements = 2
```

因此，我们有两个不同的 TotalStack 变量，Stack <int>::TotalStack 和 Stack <char>::TotalStack。我们可以看到多个类的实例具有静态成员的单独副本。输出显示两个栈的成员数量都在增加。

## 7.3.6 类模板的友元

类模板的友元可以是以下之一：

- 1. 类模板
- 2. 函数模板
- 3. 普通（非模板）函数
- 4. 普通（非模板）类
- 5. 类模板的特化
- 6. 函数模板的特化

以下代码说明了如何为类模板拥有多种类型的友元。

```
class ClassNo1; // 前向定义
template <typename Type1>
class TemplateClassNo1
{
Body of the class
}

template <typename Type2>
class TemplateClassNo2
{
Body of the class
}

template <typename Type3>
class TemplateClassNo3
{
private:
Body of the class
}
```

