
operator<<₂( operator<<₁(cout, temp1) , temp2);

```

因此 `<<₁` 的返回值被用作 `<<₂` 的左参数：

```

operator<<₂( operator<<₁'s return_value, temp2);

```

这意味着 `<<₂` 会尝试将 `temp2` 插入到 `<<₁` 返回的任意值中。

由此可以看出，`<<₁` 必须返回一个 `ostream`。而且，它应该就是 `<<₁` 将值插入其中的那个 `ostream`，因此它应当返回其参数 `out`。

另一个微妙之处与 `operator<<` 的返回类型有关。我们为什么将其返回类型定义为 `ostream &`？原因是，当 C++ 函数以通常方式返回一个值时，它实际上是将该值的一个副本返回给函数的调用者，这意味着对于输出语句 `cout << temp1 << temp2;`，`temp1` 会被插入到 `cout` 中，而 `temp2` 则会被插入到 `cout` 的一个副本中，其结果无法预知。

为了避免这种复制，C++ 允许函数使用引用返回类型，这实际上“关闭”了复制机制，并返回实际对象。因此，当我们编写 `inline ostream & operator<<(ostream & out, const Temperature & theTemp) { theTemp.display(out); return out; }` 时，实际上是在告诉编译器：“不要返回 `out` 的副本，而是返回它所引用的实际 `ostream`。”

重载输入运算符 `>>` 与 `<<` 类似。示例 14.13 给出了 `operator>>()` 的定义。

## 示例 14.13 重载 Temperature 类的运算符 >>

```

// ------- Temperature istream input -----------------------

inline istream & operator>>(istream & in, Temperature & aTemp)

{

aTemp.read(in);

return in;

}

```

注意，与输出运算符不同，输入运算符确实会修改其 `Temperature` 参数，因此它被声明为引用参数，而不是常量引用参数。

现在，将针对 `Temperature` 对象的这些新 I/O 操作添加到我们的温度库中后，示例 14.1 中的温度转换程序就可以编译并运行了。尽管肯定还有其他操作可以添加，但就我们的目的而言，我们可以认为这个库已经完整了。

## 14.4 类的其他特性

在本章中，我们讨论了设计和实现类的主要特性。然而，还有很多内容可以探讨，在本节中我们将讨论另外两个特性。一是提供对类数据成员访问的另一种方式，我们将通过在不使用 `read()` 和 `display()` 等方法的情况下实现输入和输出操作来说明这一点。另一个是“类包装器”，应将其添加进来，使我们的类适用于可能使用许多不同类的大型项目。

### 14.4.1 友元函数

尽管对类对象的大多数操作都可以实现为函数成员，但有些情况下这是不可能的。例如，我们看到输出运算符 `<<` 和输入运算符 `>>` 不能定义为 `Temperature` 的方法，因为它们的左操作数分别是 `ostream` 和 `istream`，而不是 `Temperature`：

```

cout << "Enter a temperature (e.g., 98.6 F): ";

cin >> theTemperature;

cout << "The temperature is " << theTemperature << endl;

```

我们的解决方案是为 `operator<<` 和 `operator>>` 定义使用 `Temperature` 的 `display()` 和 `read()` 方法的“普通”函数：

```

inline ostream & operator<<(ostream & out, const Temperature & aTemp)

{

    aTemp.display(out);

    return out;

}

```

```

inline istream & operator>>(istream & in, Temperature & aTemp)

{

    aTemp.read(in);

    return in;

}

```

现在，假设我们希望在不调用 `display()` 的情况下定义 `operator<<`——例如，假设我们的 `Temperature` 类没有 `display()` 方法。如果 `operator<<` 试图直接访问其参数 `aTemp` 的数据成员，

```

inline ostream & operator<<(ostream & out,const Temperature & aTemp)

{

    out << theTemp.myDegrees << ' '   // ERROR!

        << theTemp.myScale;           // ERROR!

    return out;

}

```

编译器将生成如下错误信息：

```

Member 'myDegrees' is private in class 'Temperature'

```

编译器通过不允许该函数访问类的私有数据成员来强制实现信息隐藏机制。

但假设实现某个操作的唯一合理方式是使用一个必须能够访问类的私有数据成员的函数。在这种罕见的情况下，C++ 允许类通过将该函数指定为友元来授予它这种特殊的访问权限。

为了说明这一点，假设我们从 `Temperature` 类中删除 `display()` 方法。那么我们可以将 `operator<<` 定义为：

```

inline ostream & operator<<(ostream & out, const Temperature & aTemp)

{

    out << theTemp.myDegrees << ' '

        << theTemp.myScale;

    return out;

}

```

前提是我们在类内部放置一个 `operator<<( )` 的原型，并在其前面加上关键字 `friend`：

```

class Temperature

{

public:                    // The class interface

    .

    .

    .

    friend ostream & operator<<(ostream& out, const Temperature & aTemp);

    .

    .

    .

private:                   // The hidden details

    double myDegrees;

    char myScale;

};

```

之前会产生编译错误的同一个定义现在可以正确编译了，因为通过将该函数命名为友元，类授予了该函数访问其私有部分的权限。还要注意，`operator<<( )` 没有被指定为 `const` 函数。这是因为 `const` 只能应用于函数成员，而 `operator<<( )` 不是函数成员。

类似地，我们也可以用 `operator>>()` 的友元版本替换 `read()` 方法。在这种情况下，引用参数 `aTemp` 将不是 `const` 引用参数，而只是引用参数，因为输入操作会修改它。

### 14.4.1.1 友元的使用

实现类操作时很少需要友元机制。正如我们在 `Temperature` 类中看到的，对类对象的大多数操作都可以定义为函数成员，因此它们不需要友元机制。

当操作的左操作数类型与正在构建的类不同时，就不能使用方法，必须定义普通函数。但即使在这种不常见的情况下，也可以定义一个公共的中介函数（如 `display()` 或 `read()`）供该函数调用。友元机制绝对必要的唯一情况是：操作的左操作数类型与正在构建的类不同，并且该操作必须直接访问类的数据成员。

由于友元机制体现的是定义类操作的外部方法（函数从外部操作一个对象），而不是面向对象方法中“我自己能做”的原则，因此友元机制只应在那些确属必要的罕见情况下使用。

### 14.4.2 条件编译与类“包装器”

每当编译存储在文件中的程序时，首先会由一个名为预处理器的特殊程序对其进行检查。预处理器会扫描整个文件，在文件传递给编译器之前进行一些初步分析。例如，预处理器会去除程序中的所有注释，这样编译器就不必花时间去查找并忽略它们。预处理器的另一项任务是处理所有预处理指令，这些指令是以 `#` 字符开头的行，例如：

```

#include FileName

```

当预处理器遇到该指令时，它会找到名为 `FileName` 的文件，并将其插入到程序中的该位置。

对于由许多库文件组成的大型项目，通常每个文件都会包含它所需的类声明。这意味着同一个类可能在项目的多个不同位置被声明，这会导致错误，因为 C++ 不允许一个类被声明多次。

然而，如果头文件 `<iostream>` 被多次包含，则不会导致错误。为什么？因为 `<iostream>` 的内容被包含在这样一些指令中，这些指令基本上是告诉预处理器：“如果这是你第一次看到这个类，就继续处理该声明。如果你以前见过它，就跳过该声明。”

我们可以用指令将 `Temperature` 类包裹起来，告诉预处理器对 `Temperature` 类也执行同样的操作：

```

#ifndef TEMPERATURE

#define TEMPERATURE

class Temperature

{

public:

    // function members

private:

    // data members

};

#endif

```





这些被称为 **条件编译指令**，因为它们的功能如此。指令

```

#ifndef TEMPERATURE

```

指示预处理器：“如果 `TEMPERATURE` 未定义，则继续正常处理。否则，跳过从此处到第一个 `#endif` 指令之间的所有内容。”⁶ 因为 `TEMPERATURE` 在预处理器第一次检查文件时未定义，所以它继续处理下一行。在这里它遇到了指令

```

#define TEMPERATURE

```

它定义了标识符 `TEMPERATURE`。预处理器随后继续处理类声明并将其传递给编译器。

如果预处理器再次遇到 `Temperature.h`，第一个看到的就是指令

```

#ifndef TEMPERATURE

```

这次，`TEMPERATURE` 已被定义，因此预处理器跳过该点与 `#endif` 指令之间的所有内容。

结果是，无论有多少个不同的文件包含 `Temperature.h`，类声明都只会被处理一次。为了防止头文件在一个项目中被包含多次时出现重新声明错误，类应该用这些指令包裹起来。习惯上，与 `#ifndef` 和 `#define` 指令一起使用的标识符（本例中为 `TEMPERATURE`）是类名的全大写形式。

## CHAPTER SUMMARY

关键术语

- attribute
- class
- class declaration
- class invariant
- class method
- constant method
- constructor
- data member
- default-value constructor
- dot notation
- encapsulation
- explicit-value constructor
- external perspective
- friend function
- function member
- I-can-do-it-myself principle
- information hiding
- instance variable
- interface
- internal perspective
- method
- object autonomy
- object-centered design
- operator overloading
- postcondition
- preprocessor
- private
- public
- reference return type
- scope operator

### NOTES

- 良好的类设计中，独立于实现细节很重要。
- 在程序中工作并使用类时，采用类的观察者/使用者 *外部* 视角。在类内部工作或构建其函数成员时，采用所设计对象的 *内部* 视角。
- 与其他声明一样，类声明必须以分号结束。
- 类设计的两个基本原则：
  - *封装*——单个对象可以通过将其包装在类声明中来存储不同类型的值。
  - *信息隐藏*——通过在类声明中将其设为 `private` 来防止直接访问数据成员。
- 应制定并在数据成员被修改时检查 *类不变式*，该不变式指定类的数据成员可以具有的值的限制。
- 可以将类包装在条件编译指令中，以防止头文件在一个项目中被包含多次时出现重新声明错误。
- 不修改类的数据成员的方法应声明为 `const` 方法。
- 构造函数用于初始化类的数据成员。构造函数的名称始终与类的名称相同。
- 可以通过定义名为 `operatorΔ` 的函数来重载运算符 `Δ`，前提是其签名与 `operatorΔ` 的任何现有定义不同。
- 设计良好的类接口——由其公共操作组成——需要时间和思考，应谨慎进行。如果它稳定，那么仅通过接口使用该类的程序即使类的私有部分被修改也不会中断。频繁更改它会导致使用该类的程序经常需要修订。
- 一个类可以命名一个函数为 `friend`，从而授予它访问其私有部分的权限。

### Style and Design Tips

- 当程序中的对象无法直接使用预定义类型表示时，定义一个类来表示此类对象。类的一个目的是允许不同数据类型被封装在单个对象中。
- 使用缩进来反映类的结构，因为这会提高其可读性。
- 为数据成员使用描述性标识符以强化 I-can-do-it-myself 原则。例如，每个名称以前缀 `my` 开头。
- 将类的所有数据成员保持为 `private` 并提供访问函数来检索这些成员的值。这是隐藏实现细节的一部分，并简化程序维护。
- 不修改类的数据成员的方法应声明并定义为常量方法，通过在其标题末尾附加关键字 `const` 来实现。这样可以让编译器帮助你找到逻辑错误，如果此类方法无意中更改数据成员的值（或调用可能这样做的函数）。
- 将简单方法的内联定义放在该类头文件中的类声明之后。C++ 确实允许在类声明内部定义简单方法，但这样会使声明变得杂乱，降低其可读性，因此应避免这种做法。
- 在单独编译的实现文件中定义更复杂的方法。如果定义存储在头文件中，每次编译包含该定义的程序时它都会被重新编译，这会浪费时间。将函数存储在单独编译的实现文件中可消除这项额外工作。
- 仅重载运算符以执行与其符号一致的操作。避免为了好玩而滥用重载机制，给运算符赋予违反直觉的定义，因为这会降低代码的可读性。

## Warnings

1. 在 `private:` 关键字之后声明的类的成员在类外部不可访问。私有成员只能由方法和友元函数访问。
2. 在类的方法定义中，方法的名称必须用类的名称和作用域运算符 `(::)` 限定。
3. 构造函数的名称与类的名称相同，且构造函数没有返回类型。
4. 由于类数据成员值被无意修改而导致的错误可能难以找到。为了避免此类错误，访问数据成员但不修改它们的方法应为常量方法。这是通过在其参数列表后的右括号后放置关键字 `const` 来实现的。
5. 可能在多个文件中被 `#include` 的包含类声明的文件应将类声明用条件编译预处理器指令括起来以避免错误：

```

#ifndef Something

#define Something

...

Class Declaration,

...

#endif

```

6. 友元函数必须由其为之成为友元的类命名，通过在类声明中在其声明前加上关键字 `friend`。

## TEST YOURSELF

Section 14.2

1. 对于无法直接用现有类型表示的对象，我们设计并构建一个 __________ 来表示它并将其存储在一个 __________ 中。
2. 创建一个类有两个阶段：一个 __________ 阶段和一个 __________ 阶段。
3. 在设计类时必须确定哪两件事？
4. 其中哪一个通常首先被确定？
5. 对象自主性体现在 __________ 原则中。

Section 14.3

1. 数据项存储在类的 __________ 成员中，也称为 __________ 变量。
2. __________ 允许单个对象存储不同类型的值。
3. 什么是信息隐藏及其目的？
4. 通过将它们声明为 __________ 来隐藏数据成员。
5. 数据成员必须为真的条件集合称为类 __________。
6. 类操作使用 __________ 成员实现，也称为 __________。
7. 在函数成员的定义中，其名称前面加上 __________ 和 __________ 运算符。
8. 不更改类的数据成员的函数成员应声明为 __________ 方法，通过在其标题末尾附加关键字 __________。
9. 类 `Fraction` 中的构造函数将被命名为 __________。

10. 命名并描述两种构造器。

11. （真或假）构造器的返回类型是 `bool`。

12. 类的 __________（`public` 或 `private`）部分充当该类与其使用程序之间的接口。

13. 在操作结束时必须为真的布尔表达式被称为 __________-条件。

14. 对象的函数成员是通过使用 __________ 记法调用的，并被称为向该对象发送一个 __________。

15. 用于检索数据成员中的值的函数成员称为 __________ 方法。

16. 可以通过使用名为 __________ 的函数成员向类添加加法操作 `+`。

17. 编写一个类 `Component` 的声明，该类有两个数据成员，`myID` 类型为 `int`，`myName` 类型为 `string`，一个输出方法，以及一个输入方法。

## Section 14.4

1. 一个类可以通过指定它是 __________ 来允许一个函数访问其数据成员。

2. 在程序被编译之前，它首先由 __________ 检查。

3. 所有以 __________ 字符开头的行都是预处理器指令。

4. 形式为

```
