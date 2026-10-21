

与他相关的三条语句类似，也有三条语句来定义她。使用在堆上创建的两个 Person 对象，你首先使用以下语句输出关于她的信息：

```
Console::WriteLine(L"She is {0}", her->Name);
Console::WriteLine(L"Her weight is {0:F2} kilograms.",
						her->getWeight().kilograms);
Console::WriteLine(L"Her height is {0} which is {1:F2} meters.",
						her->getHeight(),her->getHeight().meters);
```

在第一条语句中，你使用表达式 her->Name 访问由句柄 her 引用的对象的 Name 属性；执行此表达式的结果是属性 get() 值返回的字符串的句柄，因此其类型为 String^。

在第二条语句中，你使用表达式 her->getWeight().kilograms 访问由 her 引用的对象的 wt 字段的 kilograms 属性。表达式中 her->getWeight() 部分返回 wt 字段的副本，并用它来访问 kilograms 属性；因此 kilograms 属性的 get() 函数返回的值成为 WriteLine() 函数的第二个参数的值。

在第三条输出语句中，第二个参数是表达式 her->getHeight() 的结果，该表达式返回 ht 的副本。为了以适合输出的形式生成此值，编译器安排调用该对象的 ToString() 函数，因此该表达式等价于 her->getHeight().ToString()，实际上如果你愿意也可以这样写。WriteLine() 函数的第三个参数是 getHeight() 函数返回的 Height 对象 的 meters 属性，该函数属于 Person 对象 her。

最后三条输出语句以与 her 对象类似的方式输出关于 him 对象的信息。在这种情况下，weight 是通过对 him 对象中 wt 字段的 ToString() 函数的隐式调用产生的。

## 定义索引属性

索引属性是类中一组属性值，你使用方括号中的索引访问它们，就像访问数组元素一样。你已经对字符串使用了索引属性，因为 String 类将字符串中的字符作为索引属性提供。如你所见，如果 str 是 String 对象的句柄，则表达式 str[4] 访问第五个索引属性值，对应于字符串中的第五个字符。通过在引用对象的变量名后放置方括号中的索引来访问的属性，这是默认索引属性的示例。具有属性名的索引属性被描述为命名索引属性。

这里有一个包含默认索引属性的类：

```
ref class Name
{
private:
array<String^>^ Names;            // Stores names as array elements

public:
Name(...array<String^>^ names) Names(names) {}

// Indexed property to return any name
```

```
property String^ default[int]
{
    // Retrieve indexed property value
    String^ get(int index)
    {
        if(index >= Names->Length)
            throw gcnew Exception(L"Index out of range");
        return Names[index];
    }
};
```

Name 类的想法是将一个人的名字存储为单个名字的数组。构造函数接受任意数量的类型为 String^ 的参数，然后将它们存储在 Names 字段中，以便 Name 对象可以容纳任意数量的名字。

这里的索引属性是默认索引属性，因为名称由 default 关键字指定。如果你在此属性规范的位置提供常规名称，它将是命名索引属性。default 关键字后的方括号表示它确实是索引属性，并且它们所包含的类型 — 本例中为 int 类型 — 是在检索属性值时要使用的索引值类型。索引的类型不必是数值类型，并且你可以在访问索引属性值时拥有多个索引参数。

对于通过单个索引访问的索引属性，get() 函数必须具有指定索引的参数，其类型与属性名后方括号之间出现类型相同。对于此类索引属性的 set() 函数必须有两个参数：第一个参数是索引，第二个是要为与第一个参数对应的属性设置的新值。

让我们看看索引属性在实践中的行为。

## 使用默认索引属性试用

这里有一个使用 Name 类的稍微扩展版本的示例：

```
// Ex7_17.cpp : main project file.
// Defining and using default indexed properties
```

```
#include "stdafx.h"

using namespace System;
```

```
ref class Name
{
private:
    array<String^>^ Names;

public:
    Name(...array<String^>^ names) : Names(names) {}

    // Scalar property specifying number of names
    property int NameCount
```

```
{
    int get() {return Names->Length; }
}

// Indexed property to return names
property String^ default[int]
{
    String^ get(int index)
    {
        if(index >= Names->Length)
            throw gcnew Exception(L"Index out of range");
        return Names[index];
    }
};
```

```
int main(array<System::String ^> ^args)
{
    Name^ myName = gcnew Name(L"Ebenezer", L"Isaiah", L"Ezra", L"Inigo", L"Whelkwhistle");

    // List the names
    for(int i = 0 ; i < myName->NameCount ; i++)
        Console::WriteLine(L"Name {0} is {1}", i+1, myName[i]);
    return 0;
}
```

此示例产生以下输出：

```
Name 1 is  Ebenezer
Name 2 is  Isaiah
Name 3 is  Ezra
Name 4 is  Inigo
Name 5 is  Whelkwhistle
Press any key to continue . . .
```

## 工作原理

示例中的 Name 类基本上与上一节中的相同，但添加了一个名为 NameCount 的标量属性，该属性返回 Name 对象中的名字数量。在 main() 中，你首先使用五个名字创建一个 Name 对象：

```
Name^ myName = gcnew Name(L"Ebenezer", L"Isaiah", L"Ezra", L"Inigo", L"Whelkwhistle");
```

Name 类中构造函数的参数列表以省略号开头，因此它接受任意数量的参数。当调用它时提供的参数将被存储在 names 数组的元素中，因此用 names 初始化 Names 字段会使 Names 引用 names 数组。在前一条语句中，你向构造函数提供了五个参数，因此由 myName 引用的对象中的 Names 字段是一个包含五个元素的数组。

你在一个 for 循环中访问 myName 的属性以列出对象包含的名字：

```
for(int i = 0 ; i < myName->NameCount ; i++)
    Console::WriteLine(L"Name {0} is {1}", i+1, myName[i]);
```

你使用 NameCount 属性值来控制 for 循环。没有此属性，你就不知道要列出多少个名字。在循环内，WriteLine() 函数的最后一个参数访问第 i 个索引属性。如你所见，访问默认索引属性只需在 myName 变量名后放置方括号中的索引值。输出证明索引属性按预期工作。

索引属性是只读的，因为 Name 类仅为该属性包含 get() 函数。要允许更改属性，你可以为默认索引属性添加 set() 函数的定义，如下所示：

```
ref class Name
{
    // Code as before...

    // Indexed property to return names
    property String^ default[int]
    {
        String^ get(int index)
        {
            if(index >= Names->Length)
                throw gcnew Exception(L"Index out of range");
            return Names[index];
        }

        void set(int index, String^ name)
        {
            if(index >= Names->Length)
                throw gcnew Exception(L"Index out of range");
            Names[index] = name;
        }
    }
};
```

现在你可以通过在 main() 中添加一条语句来设置最后一个索引属性值，从而使用设置索引属性的能力：

```
Name^ myName = gcnew Name(L"Ebenezer", L"Isaiah", L"Ezra",
                            L"Inigo", L"Whelkwhistle");
myName[myName->NameCount - 1] = L"Oberwurst";  // Change last indexed property

// List the names
for(int i = 0 ; i < myName->NameCount ; i++)
    Console::WriteLine(L"Name {0} is {1}", i+1, myName[i]);
```

有了此添加，你会从新版本程序的输出中看到，最后一个名字确实已被将新值分配给索引位置 myName->NameCount-1 的属性的语句所更新。

