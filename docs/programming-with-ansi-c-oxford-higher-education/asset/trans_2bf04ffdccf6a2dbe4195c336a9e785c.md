

构造函数是一个与类同名的函数。当类的对象被定义时，它会自动被调用。

```
Student()
{
    roll_no = 0;
}
};

Student st1;

/* Defining an object of class Student, notice the use of
class name 'Student' instead of 'class Student' as a type */
```

这里 st1.roll_no 在语句 Student st1; 执行时会自动初始化为零。这是因为函数 Student() 在类 Student 内部定义。函数 Student()（而不是类 Student）被称为构造函数。构造函数会在对象被定义时自动调用。在本例中，当我们定义 Student st1; 时，Student() 函数会被调用。调用该函数的效果是将学号初始化为零。其优点是我们无需在定义学生对象时显式地将学号初始化为零。假设我们定义了 100 个学生或一个学生数组。每次构造函数函数都会自动调用，所有这些学生的学号都会被初始化为零。我们将在第 5 章详细学习构造函数和析构函数。

## 运算符重载

假设我们定义了一个复数变量的类。复数变量有两个部分，实部和虚部。如果我们将类命名为 complex，那么就可以定义

```
complex c1, c2;
```

这里，complex 是类名，c1 和 c2 是 complex 类型的变量，即类 complex 的对象。可以写出 c1 + c2 作为表达式，其中 + 将分别相加实部和虚部的值。默认情况下 + 仅对内置类型如 int、float 和 double 进行加法。C++ 提供了将 + 赋予新含义的设施，使其现在也可以相加两个复数变量。该设施称为运算符重载。这里，我们需要重载 + 运算符以获得所需的效果。 （有兴趣了解如何实现的读者可以参阅第 6 章运算符重载，其中提供了复数对象相加的程序。）

提供所有这些设施的最终目标是使用户定义的对象尽可能自然地表现。在 C++ 中，用户定义的对象实际上可以自然地表现。仅通过查看用户定义对象的使用，几乎不可能将其与内置对象区分开来。在 C 中，用户定义的数据类型始终与内置类型看起来不同（例如，struct，struct Student，struct employee 等）。

### 1.11.2 语法差异

C 与 C++ 之间存在许多语法差异。主要差异源于提供类构造及其相关问题的需要。几乎所有 C 语法在所有 C++ 编译器中都能正常工作。一些语法差异总结如下。

#### 注释

C++ 中的注释有两种类型。C 风格的注释（/* 和 */ 之间包围的内容）是可以接受的，以 // 开始的注释也是允许的。当 // 在某行中出现时，该行的其余部分将被忽略。看下面的代码：

```
/* This itself is a C-like comment, whereas the
following is a C++-like comment */
if (a > b) // checking for a greater than b
printf ("a is greater!");
```

下面是一个例子，说明 C++ 注释如何替代 C 风格注释：

```
/* This is the first line of comment.
This is the second line of it.
And this is the third! */

// This is the first line of comment.
// This is the second line of it.
// And this is the third!
```

简而言之，// 对于单行注释很有用，但对于多行，可以更喜欢使用 /* 和 */。

而且，// 在行尾有效，因此它不能替代以下语句中使用的 C 风格注释：

```
if (a > b)        /* checking for a > b!*/
printf("a is greater!");
```

#### 输入/输出运算符

尽管在第 1.11.2 节给出的程序语句中使用了 printf()，但它通常不用于 C++ 程序中。

```
cout << "a is greater";
```

可以在 C++ 中完成与 printf() 相同的任务。

这里，cout 是标准输出流类的对象。它是 C++ 中最有用的对象之一。我们需要包含 <iostream> 文件以获得 iostream（更准确地说是输入输出流）对象的原型。我们可以看到 iostream 类似于 C 中使用的 stdio.h。应该记住，我们仍然需要使用 stdio.h 来使用输入和输出流的函数原型，例如 printf() 和 scanf()。

如果可以在 C++ 中使用 stdout（即 printf()、scanf() 等），那么为什么我们需要一种新的输出方式？这个问题将在第 12 章中详细解答。简而言之，更新的方法更好且更易于编程。有时，这种方法是在为用户定义对象提供与内置类型类似的输入和输出时唯一的方法。例如，可以有一个学生 Lara，然后使用 cout<< Lara 打印关于 Lara 的详细信息。我们需要为此重载运算符 <<。这对于 printf() 来说是不可能的。如前所述，如果使用 printf()，则需要包含 <stdio.h>。运行程序的用户在 printf() 和 cout 产生的输出之间找不到区别。

在使用 ANSI C++ 时，应使用 <cstdio> 而不是 <stdio.h>。使用 <cstdio> 与 <stdio.h> 的功能相似，即

在编写 C++ 程序时，应使用 cin 进行读取而不是 scanf()，使用 cout 进行打印而不是 printf()。这些构造更简单更好。

对于可以编译 C 和 C++ 程序的编译器，文件名扩展名决定了代码的类型。在 TurboC 或 VC++ 中，'.c' 是 C 程序，而 '.cpp' 是 C++ 程序。

cout 使用的 << 运算符和 cin 使用的 >> 是运算符重载的例子。

<cstdio> 或 <stdio.h> 将以完全相同的方式提供 printf()、scanf() 等。尽管如此，它们之间仍有巨大差异。该差异在第 14 章中解释。同样，如果我们想使用其他 C 头文件（例如，<math.h> 变为 <cmath>），也会有差异。

使用 C 和 C++ 中的 printf() 等函数之间还有另一个看似微小的差异。对于大多数 C 编译器，可以在不包含 <stdio.h> 的情况下使用 printf() 或 scanf()。这样的程序可以编译并且也能按预期工作。包含 <stdio.h> 似乎不是必要的（因为 stdio.h 仅包含函数的原型）。为什么会这样？让我们试着理解这一点。

printf()（以及其他函数）的编译代码保存在库中。库包含所有属于库的函数的目标代码。printf() 和 scanf() 的代码在编译后、在生成可执行代码之前被添加到程序代码中。

注意 C 程序在使用函数时不需要原型。如果缺少函数的原型，C 编译器最多会发出警告。相反，C++ 程序如果没有原型就不会编译。原型在 C++ 中是必须的。如果我们使用 printf() 或 scanf() 并且没有 stdio.h 的头文件，程序在 C++ 中将无法编译。

在 cout 的情况下，<< 实际上是一个重载的运算符。这意味着 <<，本质上是一个按位左移运算符，在这里被赋予了新的含义。给现有运算符提供新的附加含义的过程称为运算符重载。应该记住，我们仍然可以将 << 用作按位左移运算符。这里赋予的新含义是额外的（除了原始含义之外）。

同样，我们可以使用 >> 运算符（同样是重载的）用于读取目的。为此，我们使用标准输入流对象 cin。iostream 类的内置对象 cin 用于从控制台读取元素。因此，以下语句可用于读取字符串变量，其名称假定为 StringVariable：

```
cin >> StringVariable
```

我们不需要为 cin 或 cout 提供数据类型（如 %d 或 %s），也不需要在读取变量值时在变量前附加 & 运算符，如 scanf 中那样。在 C++ 中，cout 以默认方式格式化输出，这适用于大多数情况。我们将在第 12 章学习如何以不同于默认方式格式化数据。

#### C++ 头文件

我们不能使用 stdio.h 来使用 cout 或 cin。我们需要在程序中写 #include <iostream> 来使用 cout 和 cin。头文件名 <iostream> 中省略 .h 应该注意。这是 ANSI C++ 中的新风格。旧的 C++ 程序使用文件 <iostream.h>。如果我们写 <iostream.h> 而不是 <iostream>，它可能在大多数现有的 C++ 编译器中都能工作。请理解它仅为向后兼容而提供。不再建议在 C++ 中使用 <iostream.h>。

当我们在第 14 章学习命名空间时，我们将看到使用 iostream 和 iostream.h 之间的区别。

#### 返回类型

C 中的返回类型默认为 int，而在 C++ 中则不是，因此我们必须指定它。例如，

