

事实上，每个函数（不仅仅是重载函数）都被认为有一个签名，其中函数的签名由其名称和参数列表决定。程序中的所有函数必须具有唯一的签名；否则程序无法编译。

## 使用重载函数试一试

你可以用已经定义的函数 max() 来练习重载功能。尝试一个包含 int、long 和 double 数组的三个版本的示例。

```
// Ex6_07.cpp
// Using overloaded functions
#include <iostream>
using std::cout;
using std::endl;

int max(int array[], int len);        // Prototypes for
long max(long array[], int len);     // a set of overloaded
double max(double array[], int len); // functions

int main(void)
{
    int small[] = {1, 24, 34, 22};
    long medium[] = {23, 245, 123, 1, 234, 2345};
    double large[] = {23.0, 1.4, 2.456, 345.5, 12.0, 21.0};

    int lensmall = sizeof small/sizeof small[0];
    int lenmedium = sizeof medium/sizeof medium[0];
    int lenlarge = sizeof large/sizeof large[0];

    cout << endl << max(small, lensmall);
    cout << endl << max(medium, lenmedium);
    cout << endl << max(large, lenlarge);

    cout << endl;
    return 0;
}

// Maximum of ints
int max(int x[], int len)
{
    int max = x[0];
    for(int i = 1; i < len; i++)
        if(max < x[i])
            max = x[i];
    return max;
}

// Maximum of longs
long max(long x[], int len)
{
    long max = x[0];
    for(int i = 1; i < len; i++)
        if(max < x[i])
            max = x[i];
    return max;
}

// Maximum of doubles
double max(double x[], int len)
{
    double max = x[0];
    for(int i = 1; i < len; i++)
        if(max < x[i])
            max = x[i];
    return max;
}
```

该示例按预期工作并产生以下输出：

```
34
2345
345.5
```

## 工作原理

你为函数 max() 的三个重载版本提供了三个原型。在每三个输出语句中，编译器根据参数列表类型选择适当的 max() 函数版本。这之所以可行，是因为 max() 函数的每个版本都有唯一的签名，因为其参数列表与其他 max() 函数不同。

## 何时重载函数

函数重载为你提供了一种确保函数名描述所执行的功能并且不会因诸如正在处理的数据类型等无关信息而混淆的手段。这与 C++ 中基本操作发生的情况类似。要将两个数字相加，你使用相同的运算符，而不管操作数的类型如何。我们的重载函数 max() 的名称相同，而不管正在处理的数据类型如何。这有助于使代码更具可读性，并使这些函数更易于使用。

> 函数重载的意图很明确：使同一操作能够使用不同的操作数通过单个函数名执行。因此，只要你有一系列本质上执行相同操作但参数类型不同的函数，你就应该重载它们并使用一个公共函数名。

## 函数模板

上一个示例有点乏味，因为你必须为每个函数重复本质上相同的代码，但使用不同的变量和参数类型，然而，有一种方法可以避免这种情况。你可以创建一种配方，使编译器能够自动生成具有各种参数类型的函数。定义用于生成特定函数组的配方的代码称为函数模板。

函数模板有一个或多个类型参数，你通过为模板的每个参数提供具体的类型参数来生成特定函数。因此，函数模板生成的函数都具有相同的基本代码，但由你提供的类型参数进行定制。你可以通过为上一个示例中的函数 max() 定义函数模板来实际了解其工作原理。

## 使用函数模板

你可以按如下方式为函数 max() 定义模板：

```
template<class T> T max(T x[], int len)
{
    T max = x[0];
    for(int i = 1; i < len; i++)
        if(max < x[i])
            max = x[i];
    return max;
}
```

template 关键字标识这是模板定义。template 关键字后面的尖括号括起用于创建特定函数实例的类型参数，以逗号分隔；在这种情况下，你只有一个类型参数 T。T 前面的 class 关键字表示 T 是此模板的类型参数，class 是类型的通用术语。书中后面你将看到，定义一个类本质上就是定义你自己的数据类型。因此，C++ 中有基本类型，例如类型 int 和类型 char，你也有自己定义的类型。请注意，你可以使用 typename 关键字代替 class 来标识函数模板中的参数，在这种情况下，模板定义看起来像这样：

```
template<typename T> T max(T x[], int len)
{
    T max = x[0];
    for(int i = 1; i < len; i++)
        if(max < x[i])
            max = x[i];
    return max;
}
```

一些程序员更喜欢使用 typename 关键字，因为 class 关键字往往暗示用户定义的类型，而 typename 更中性，因此更易于理解为暗示基本类型以及用户定义的类型。实际上你会看到两种关键字都被广泛使用。

在函数模板的定义中出现的任何地方，T 都被你创建模板实例时提供的特定类型参数，例如 long 所替换。如果你手动尝试通过将 T 替换为 long 来进行测试，你会看到这会生成一个完全令人满意的用于计算 long 类型数组的最大值的函数：

```
long max(long x[], int len)
{
    long max = x[0];
    for(int i = 1; i < len; i++)
        if(max < x[i])
            max = x[i];
    return max;
}
```

创建特定函数实例的过程称为**实例化**。

每次在程序中使用函数 max() 时，编译器都会检查是否已存在与你在函数调用中使用的参数类型相对应的函数。如果所需的函数不存在，编译器会通过将你在函数调用中使用的参数类型替换为模板定义中相应源代码中的参数 T 来创建它。你可以用上一个示例中使用的同一个 main() 函数来练习 max() 函数模板。

## 使用函数模板试一试

以下是修改后的上一个示例，使用模板为 max() 函数：

```
// Ex6_08.cpp
// Using function templates

#include <iostream>
using std::cout;
using std::endl;

// Template for function to compute the maximum element of an array
template<typename T> T max(T x[], int len)
{
    T max = x[0];
    for(int i = 1; i < len; i++)
        if(max < x[i])
            max = x[i];
    return max;
}

int main(void)
{
    int small[] = { 1, 24, 34, 22};
    long medium[] = { 23, 245, 123, 1, 234, 2345};
    double large[] = { 23.0, 1.4, 2.456, 345.5, 12.0, 21.0};

    int lensmall = sizeof small/sizeof small[0];
    int lenmedium = sizeof medium/sizeof medium[0];
    int lenlarge = sizeof large/sizeof large[0];

    cout << endl << max(small, lensmall);
    cout << endl << max(medium, lenmedium);
    cout << endl << max(large, lenlarge);

    cout << endl;
    return 0;
}
```

如果运行此程序，它会产生与上一个示例完全相同的输出。

## 工作原理

对于每个输出数组中最大值语句，都会使用模板实例化 max() 的新版本。当然，如果你添加另一条使用之前使用过的类型调用函数 max() 的语句，则不会生成新的代码版本。

请注意，使用模板不会以任何方式减少编译后程序的大小。编译器会为你需要的每个函数生成源代码版本。事实上，使用模板通常会增加程序的大小，因为即使通过强制转换参数也可以令人满意地使用现有版本，也会自动创建函数。你可以通过显式包含其声明来强制创建模板的特定实例。例如，如果你想确保为函数 max() 的模板创建对应于类型 float 的实例，你可以在模板定义之后放置以下声明：

```
float max(float, int);
```

这会强制创建此函数模板的版本。在我们的程序示例中它没有多大价值，但在你知道可能会生成模板函数的多个版本，但希望强制生成你计划在必要时将参数强制转换为适当类型后使用的子集时，它会很有用。

## 使用函数的示例

到目前为止，你已经在 C++ 中涵盖了很多内容，仅本章关于函数的内容就很多。在浏览了各种语言功能菜单后，不总是很容易看出它们如何相互关联。现在是时候看看这些东西如何结合起来产生比简单演示程序更有实质性的东西。

让我们通过一个更现实的示例来了解如何将问题分解为函数。该过程涉及定义要解决的问题，分析问题以了解如何用 C++ 实现它，最后编写代码。这里的方法旨在说明各种函数如何组合起来构成最终结果，而不是提供如何开发程序的教程。

## 实现计算器

假设你需要一个充当计算器的程序；不是那种带有大量按钮和装置、为容易满足的人设计的设备，而是为在算术上知道自己要去哪里的人设计的。你可以真正大干一场，将计算从键盘输入为单个算术表达式，并立即显示答案。你输入的内容示例是：

```
2*3.14159*12.6*12.6 / 2 + 25.2*25.2
```

为了暂时避免不必要的复杂性，你不会允许表达式中出现括号，并且整个计算必须在一行中输入；然而，为了让用户使输入看起来更具吸引力，你将允许在任何地方放置空格。输入的表达式可能包含

