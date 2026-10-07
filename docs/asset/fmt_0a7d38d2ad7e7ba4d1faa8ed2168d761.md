
在这个示例中，`HoldsPair`类接受命名为`T1`和`T2`的模板参数。我们可以使用该类持有相同类型或不同类型的对象，如下所示：

```cpp
// int 和 double 的模板实例化
HoldsPair<int, double> pairIntDouble(6, 1.99);
```

```cpp
// int 和 int 的模板实例化
HoldsPair<int, int> pairIntDouble(6, 500);
```

# 使用默认参数声明模板

我们可以修改上一个版本的`HoldsPair<...>`，将`int`声明为默认模板类型。

```cpp
template <typename T1=int, typename T2=int>
class HoldsPair
{
    // ... 方法声明
};
```

这在构造上与定义了默认输入参数值的函数相似，区别在于，在这种情况下，我们定义的是默认类型。

因此，`HoldsPair`的第二次用法可以简化为：

```cpp
// 将一个 int 与一个 int 配对（默认类型）
HoldsPair<> pairInts(6, 500);
```

# 模板类<> HoldsPair 示例

是时候对目前介绍的`HoldsPair`模板版本进行进一步开发了。请看列表 14.4。

## 列表 14.4 具有成对成员属性的模板类

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: // 带有默认参数的模板：int & double
4: template <typename T1=int, typename T2=double>
5: class HoldsPair
6: {
7:   private:
8:     T1 value1;
9:     T2 value2;
10:  public:
11:     HoldsPair(const T1& val1, const T2& val2) // 构造函数
12:       value1(val1), value2(val2) {}
13:
14:     // 访问函数
15:     const T1& GetFirstValue() const
16:     {
17:       return value1;
18:     }
19:
20:     const T2& GetSecondValue() const
21: {
22:     return value2;
23: }
24: };
25:
26: int main ()
27: {
28:     HoldsPair<int> pairIntDbl(300, 10.09);
29:     HoldsPair<short,const char*>pairShortStr(25,"Learn templates, love C++");
30:
31:
32:     cout << "The first object contains - " << endl;
33:     cout << "Value 1: " << pairIntDbl.GetFirstValue() << endl;
34:     cout << "Value 2: " << pairIntDbl.GetSecondValue() << endl;
35:
36:     cout << "The second object contains - " << endl;
37:     cout << "Value 1: " << pairShortStr.GetFirstValue() << endl;
38:     cout << "Value 2: " << pairShortStr.GetSecondValue() << endl;
39:
     return 0;
40: }
```

## 输出

```
The first object contains -
Value 1: 300
Value 2: 10.09
The second object contains -
Value 1: 25
Value 2: Learn templates, love C++
```

## 分析

这个简单的程序说明了如何声明模板类`HoldsPair`，以持有一组依赖于模板参数列表的类型值。第 1 行包含一个模板参数列表，定义了两个模板参数`T1`和`T2`，其默认类型分别为`int`和`double`。访问函数`GetFirstValue()`和`GetSecondValue()`用于查询对象持有的值。注意`GetFirstValue`和`GetSecondValue`如何根据模板实例化的语法进行调整，以返回适当的对象类型。你成功在`HoldsPair`中定义了一种模式，可以对不同的变量类型重用相同的逻辑。因此，模板增加了代码的可重用性。

# 模板实例化与特化

模板类是一个蓝图，因此在被实例化之前，它对编译器来说并不真正存在。然而，当你通过提供模板参数来实例化模板类时，例如：

```cpp
HoldsPair<int, double> pairIntDbl;
```

你是在指示编译器为特定的类型创建一个类。另一方面，某些情况需要你对模板参数均为`int`类型的类进行显式特化。这种针对特定类型的模板特化看起来如下所示：

```cpp
template<> HoldsPair<int, int>
{
    // 实现代码
};
```

无需多说，特化模板的代码必须遵循模板定义。列表 14.5 是一个模板特化的示例，展示了如何产生模板的一个不同版本。

## 列表 14.5 展示模板特化

```cpp
0: #include <iostream>
1: using namespace std;
2:
3: template <typename T1 = int, typename T2 = double>
4: class HoldsPair
5: {
6:   private:
7:     T1 value1;
8:     T2 value2;
9: public:
10:    HoldsPair(const T1& val1, const T2& val2) // 构造函数
11:        value1(val1),value2(val2) {}
12: };
13: // 访问函数
14: const T1& GetFirstValue() const;
15: const T2& GetSecondValue() const;
16: };
17:
18: // int & int 类型的 HoldsPair 特化
19: template<> class HoldsPair<int,int>
20: {
21:   private:
22:     int value1;
23:     int value2;
24:     string strFun;
25:   public:
26:     HoldsPair(const int& val1, const int& val2) // 构造函数
27:     : value1(val1),value2(val2) {}
28: 
29:     const int& GetFirstValue() const
30: {
31:         cout << "Returning " << value1 << endl;
32:         return value1;
33: }
34: };
35:
36: int main ()
37: {
38:     HoldsPair<int, int> pairInt(222, 333);
39:     pairInt.GetFirstValue();
40:     return 0;
41: }
```

## 输出

```
Returning 222
```

## 分析

显然，当你将列表 14.4 中的模板类行为与形式一个进行比较时，你会发现模板的行为有所不同。事实上，第 18-34 行的特化显示了针对`int`实例化对原始模板定义进行了修改。这是因为编译器只需要`<int, int>`的实现，而我们已经提供了它。

# 模板简介

## 输出

```
Setting staticVal for intInstance to 2011
Setting staticVal for Double_2 to 1011
intInstance.staticVal = 2011
dblinstance.staticVal = 1011
```

# 分析

在第 17 行和第 21 行中，你分别为`int`和`double`类型的实例化设置了成员`staticVal`。输出显示，编译器在两个不同的静态成员中存储了两个不同的值，尽管它们的名称都为`staticVal`。因此，编译器确保了静态变量在特定类型的模板类实例化中的行为保持完好。

> 注意：不要错过列表 14.6 中第 11 行中模板类的静态成员实例化语法。

`template<typename T> int TestStatic<T>::staticVal;`
这遵循了以下模式：

`template<template parameters> StaticType ClassName<Template> Arguments::Static<;`

# 变量模板，也称为变长模板

假设你想写一个相加两个值的泛型函数。模板函数`Sum()`正是为此：

```cpp
template<typename T1, typename T2, typename T3>
void Sum(T1& result, T2 num1, T3 num2) {
  result = num1 + num2;
  return;
}
```

这很简单。然而，如果你被要求写一个能够添加任意数量值（每个值作为参数传递）的单一函数，你可能需要在定义此类函数时使用变量模板。变量模板或变长模板是 C++ C14 标准的一部分，于 2014 年发布。列表 14.7 展示了在定义此类函数时使用变量模板。

## 列表 14.7 使用变长模板的函数演示变长参数

```cpp
0: #include <iostream>
1: using namespace std;
2: 
3: template <typename Res, typename ValType>
4: void Sum(Res& result, ValType& val)
5: {
6:     result = result + val;
7: }
8: 
9: template <typename Res, typename First, typename... Rest>
10: void Sum(Res& result, First val, Rest... valN)
11: {
12:     result = result + val;
13:     return Sum(result, valN...);
14: }
15: 
16: int main()
17: {
18:     double dResult = 0;
19:     Sum(dResult, 3.14, 4.56, 1.1111);
20:     cout << "dResult = " << dResult << endl;
21: 
22:     string strResult;
23:     Sum(strResult, "Hello", "World");
24:     cout << "strResult = " << strResult.c_str() << endl;
25: 
26:     return 0;
27: }
```

# 输出

```
dResult = 8.8111
strResult = Hello World
```

# 分析

示例展示了我们使用变量模板定义的函数`Sum()`不仅处理了完全不同的参数类型（如第 19 行和第 23 行所示），而且处理了数量的参数。第 19 行调用的`Sum()`使用了四个参数，而第 23 行的使用了三个参数，其中一个是`std::string`，另外两个是`const char*`。在编译期间，编译器实际上会为适合调用的正确`Sum()`创建代码，递归进行，直到所有参数都处理完毕。

# 模板简介 | 415

注意

> 你可能注意到前面的代码示例中使用了省略号`...`。C++ 中与模板一起使用的省略号告诉编译器，该模板类或函数可以接受任意数量、任意类型的模板参数。

变量模板是 C++ 的一项强大补充，不仅适用于数学处理，也适用于完成简单任务。使用变量模板可以节省自己通过在多个重载版本中实现执行某任务的函数的重复劳动，使生成的代码更短且更易于维护。

注意

C++14 为你提供了一个运算符，可以告诉在调用变量模板时传递了多少个模板参数。在列表 14.7 中，你可以在像`Sum()`这样的函数内部该运算符，如下：

```cpp
int arrNums[sizeof...(Rest)];
// 数组长度在编译时使用 sizeof...) 进行评估
```

你绝不能将`sizeof(...)(()`与`sizeof(Type)`混淆。后者返回类型的大小，而前者返回变长模板中模板参数的数量。

变量模板的支持也引入了对元组（tuples）的标准支持。`std::tuple`是实现元组的类模板。它可以用不同数量的成员元素及其引用进行实例化。这些元素可以使用标准库函数`std::get`单独访问。列表 14.8 展示了`std::tuple`的实例化和使用。

## 列表 14.8 实例化和使用 std::tuple

```cpp
0: #include <iostream>
1: #include <tuple>
2: #include <string>
3: using namespace std;
4:
5: template <typename tupleType>
6: void DisplayInfo(tupleType& tuple)
7: {
8: const int numMembers = tuple_size<tupleType>::value;
9: cout << "Num elements in tuple: " << numMembers << endl;
10: }
11: int main()
12: {
13:     tuple<int, double, string> t1(1, 2.2, "hello");
14:     DisplayInfo(t1);
15: 
16:     tuple<string, int> t2("world", 123456);
17:     DisplayInfo(t2);
18: 
19:     tuple<char, char, char, char> t3('a', 'b', 'c', 'd');
20:     DisplayInfo(t3);
21: 
22:     return 0;
23: }
```

# 输出

```
Num elements in tuple: 3
Num elements in tuple: 2
Num elements in tuple: 4
```

# 分析

首先，如果 14.8 中的代码让你感到困惑，请不要！元组是一个高级概念，通常用于泛型编程。尽管如此，书中引入该主题是为了让你有一个大致的了解。第 15、18 和 21 行包含了不同的实例化。第 5 行的模板函数`DisplayInfo()`展示了使用`tuple_size`来解析包含的元素数量。第 10 行的`std::get`是使用索引访问元组中值的机制。最后，第 26 行的`std::tie`展示了如何将元组的内容解包或拷贝到单独的对象中。

## 模板简介

# 使用 static_assert 执行编译检查

这是自 C++11 起引入的一项功能，允许你在某些检查不时不阻止编译。这听起来可能很奇怪，但对于模板类非常有用。例如，你可能希望确保你的模板类不会为整数实例化；`static_assert`是一种编译时断言，可以在开发环境（或控制台）中显示自定义消息：

```cpp
static_assert(表达式表达式, "检查失败时的错误消息");
```

为了确保你的模板类不会为`int`类型实例化，你可以将`static_assert()`用于`sizeof(T)`，与`sizeof(int)`进行比较并在不等检查失败时显示错误消息：

```cpp
static_assert(sizeof(T) != sizeof(int), "No int please!");
```

使用`static_assert`阻塞某些实例化类型的模板类见列表 14.9。

## 列表 14.9 一个在为类型实例化时会抗议的挑剔模板类

```cpp
0: template <typename T>
1: class EverythingButInt
2: {
3: public:
4:   EverythingButInt()
5:   {
6:     static_assert(sizeof(T) != sizeof(int), "No int please!");
7:   }
8: };
9:
10: int main()
11: {
12:   EverythingButInt<int> test; // 与 int 的模板实例化。
13:   return 0;
14: }
```
