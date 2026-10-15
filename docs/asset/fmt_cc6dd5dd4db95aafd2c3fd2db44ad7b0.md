
{ // set courseName to first 25 characters of parameter name

    courseName = name.substr( 0, 25 ); // select first 25 characters

    cout << "Name \"" << name << "\" exceeds maximum length (25).\n"

         << "Limiting courseName to first 25 characters.\n" << endl;

} // end if...else

} // end function setCourseName

// function to retrieve the course name

string GradeBook::getCourseName()

{

    return courseName;

} // end function getCourseName

// display a welcome message to the GradeBook user

void GradeBook::displayMessage()

{

    // this statement calls getCourseName to get the

    // name of the course this GradeBook represents

    cout << "Welcome to the grade book for\n" << getCourseName() << "!\n"

         << endl;

} // end function displayMessage

// input three grades from user; determine maximum

void GradeBook::inputGrades()

{

    int grade1; // first grade entered by user

    int grade2; // second grade entered by user

    int grade3; // third grade entered by user

    cout << "Enter three integer grades: ";

    cin >> grade1 >> grade2 >> grade3;

    // store maximum in member maximumGrade

    maximumGrade = maximum( grade1, grade2, grade3 );

} // end function inputGrades

// returns the maximum of its three integer parameters
int GradeBook::maximum( int x, int y, int z )
{

64  int maximumValue = x; // assume x is the largest to start

65

66  // determine whether y is greater than maximumValue
67  if ( y > maximumValue )
68      maximumValue = y; // make y the new maximumValue

69

70  // determine whether z is greater than maximumValue
71  if ( z > maximumValue )
72      maximumValue = z; // make z the new maximumValue

73

74  return maximumValue;
75 } // end function maximum
76

77  // display a report based on the grades entered by user
78 void GradeBook::displayGradeReport()
79 {

80     // output maximum of grades entered
81     cout << "Maximum of grades entered: " << maximumGrade << endl;
82 } // end function displayGradeReport

图 6.3 | `GradeBook` 类定义函数 `maximum`。 (第 3 部分，共 3 部分。)

```cpp
// Fig. 6.4: fig06_04.cpp
// Create GradeBook object, input grades and display grade report.
#include "GradeBook.h" // include definition of class GradeBook

int main()
{
    // create GradeBook object
    GradeBook myGradeBook( "CS101 C++ Programming" );

    myGradeBook.displayMessage(); // display welcome message
    myGradeBook.inputGrades(); // read grades from user
    myGradeBook.displayGradeReport(); // display report based on grades
    return 0; // indicate successful termination
} // end main
```

```
Welcome to the grade book for
CS101 C++ Programming!

Enter three integer grades: 86 67 75
Maximum of grades entered: 86
```

```
Welcome to the grade book for
CS101 C++ Programming!

Enter three integer grades: 67 86 75
Maximum of grades entered: 86
```

图 6.4 | 演示函数 `maximum`。 (第 1 部分，共 2 部分。)

```
Welcome to the grade book for
CS101 C++ Programming!

Enter three integer grades: 67 75 86
Maximum of grades entered: 86
```

图 6.4 | 演示函数 `maximum`。 (第 2 部分，共 2 部分。)

## 软件工程观察 6.2

图 6.3 第 58 行中用于分隔函数 `maximum` 参数的逗号并不是第 5.3 节中讨论的逗号运算符。逗号运算符保证其操作数按从左到右的顺序求值。然而，函数参数的求值顺序并未由 C++ 标准指定。因此，不同的编译器可以以不同的顺序求值函数参数。C++ 标准确实要求在调用的函数执行之前，必须先求值函数调用中的所有参数。

## 可移植性提示 6.1

有时当函数的参数是更复杂的表达式时，例如包含对其他函数的调用，编译器求值参数的顺序可能会影响一个或多个参数的值。如果不同编译器之间的求值顺序发生变化，则传递给函数参数的值可能会有所不同，从而导致微妙的逻辑错误。

## 错误预防提示 6.1

如果您对函数参数的求值顺序以及该顺序是否会影响传递给函数的值存在疑问，请在函数调用之前在单独的赋值语句中求值参数，将每个表达式的结果赋给局部变量，然后将这些变量作为参数传递给函数。

成员函数 `maximum` 的原型 (图 6.2，第 17 行) 表明该函数返回一个整数值，函数名为 `maximum`，并且该函数需要三个整数参数来完成其任务。函数 `maximum` 的头 (图 6.3，第 62 行) 与函数原型匹配，并表明参数名称为 `x`、`y` 和 `z`。当调用 `maximum` 时 (图 6.3，第 58 行)，参数 `x` 用参数 `grade1` 的值初始化，参数 `y` 用参数 `grade2` 的值初始化，参数 `z` 用参数 `grade3` 的值初始化。函数调用中必须为每个参数提供一个参数 (也称为形式参数)。

请注意，函数原型和函数头中都以逗号分隔的列表形式指定了多个参数。编译器参考函数原型来检查对 `maximum` 的调用是否包含正确数量和类型的参数，以及参数类型的顺序是否正确。此外，编译器使用原型来确保函数返回的值可以在调用该函数的表达式中正确使用 (例如，返回类型为 `void` 的函数调用不能用作赋值语句的右侧)。每个参数必须与相应参数的类型一致。例如，类型为 `double` 的参数可以接收像 `7.35`、`22` 或 `−0.03456` 这样值，但不能接收像 `"hello"` 这样的字符串。如果传递给函数的参数与函数原型中指定的类型不匹配，编译器会尝试将参数转换为这些类型。第 6.5 节讨论了这种转换。

## 常见编程错误 6.1

将具有相同类型的多个方法参数声明为 `double x, y` 而不是 `double x, double y` 是语法错误——参数列表中每个参数都需要显式类型。

## 常见编程错误 6.2

如果函数原型、函数头和函数调用在参数和参数的数量、类型和顺序以及返回类型上不一致，则会发生编译错误。

## 软件工程观察 6.3

具有许多参数的函数可能执行了太多任务。考虑将函数分解为执行单独任务的更小函数。如果可能，请将函数头限制为一行。

为了确定最大值 (图 6.3 第 62–75 行)，我们首先假设参数 `x` 包含最大值的，因此函数 `maximum` 的第 64 行声明局部变量 `maximumValue` 并用参数 `x` 的值初始化它。当然，参数 `y` 或 `z` 可能包含实际的最大值，因此我们必须将这些值与 `maximumValue` 进行比较。第 67–68 行的 `if` 语句确定 `y` 是否大于 `maximumValue`，如果是，则将 `y` 赋给 `maximumValue`。第 71–72 行的 `if` 语句确定 `z` 是否大于 `maximumValue`，如果是，则将 `z` 赋给 `maximumValue`。此时，三者中最大的值在 `maximumValue` 中，因此第 74 行将该值返回给第 58 行的调用。当程序控制返回到程序中调用 `maximum` 的点时，`maximum` 的参数 `x`、`y` 和 `z` 不再可供程序访问。我们将在下一节看到原因。

有三种方法可以将控制权返回到函数被调用的位置。如果函数不返回结果 (即函数具有 `void` 返回类型)，则当程序到达函数结束的右大括号时控制权返回，或通过执行语句

```
return;
```

返回。如果函数确实返回结果，则语句

```
return expression;
```

计算 `expression` 并将 `expression` 的值返回给调用者。

## 6.5 函数原型和参数强制转换

函数原型 (也称为函数声明) 告诉编译器函数的名称、函数返回的数据类型、函数期望接收的参数数量、这些参数的类型以及期望这些类型参数的顺序。

## 软件工程观察 6.4

C++ 要求使用函数原型。使用 `#include` 预处理器指令从适当的库的头文件中获取 C++ 标准库函数的函数原型 (例如，数学函数 `sqrt` 的原型在头文件 `<cmath>` 中；C++ 标准库头文件部分列表出现在第 6.6 节)。还使用 `#include` 来获取您或您的小组成员编写的包含函数原型的头文件。

## 常见编程错误 6.3

> 如果在函数被调用之前定义了该函数，则该函数的定义本身也充当函数的原型，因此不需要单独的原型。如果在函数被定义之前调用了该函数，并且该函数没有函数原型，则会发生编译错误。

## 软件工程观察 6.5

> 始终提供函数原型，即使在函数在使用前定义的情况下可以省略它们（此时函数头本身也充当函数原型）。提供原型可以避免将代码绑定到函数定义的顺序（随着程序的演进，该顺序很容易发生变化）。

## 函数签名

函数原型中包含函数名及其参数类型的部分称为 **函数签名** 或简称为 **签名**。函数签名不指定函数的返回类型。同一作用域中的函数必须具有唯一的签名。函数的范围是函数在其中已知且可访问的程序区域。我们将在第 6.10 节中进一步讨论作用域。

## 常见编程错误 6.4

> 如果同一作用域中的两个函数具有相同的签名但返回类型不同，则为编译错误。

在图 6.2 中，如果第 17 行的函数原型被写成

```
void maximum( int, int, int );
```

编译器会报告错误，因为函数原型中的 `void` 返回类型与函数头中的 `int` 返回类型不同。同样，此类原型也会导致语句

```
cout << maximum( 6, 7, 0 );
```

生成编译错误，因为该语句依赖于 `maximum` 返回一个值以供显示。

## 参数强制转换

函数原型的一个重要特性是 **参数强制转换**——即强制参数为参数声明中指定的适当类型。例如，程序可以用整数参数调用一个函数，即使函数原型指定了 `double` 参数——函数仍然可以正确工作。

## 参数提升规则

有时，参数值与函数原型中的参数类型不完全对应，可以由编译器在函数被调用之前转换为适当的类型。这些转换是按照 C++ 的 **提升规则** 指定的。提升规则说明如何在不丢失数据的情况下在类型之间转换。`int` 可以转换为 `double` 而不会改变其值。但是，`double` 转换为 `int` 会截断 `double` 值的分数部分。请记住，`double` 变量可以保存比 `int` 变量大得多的数量级数字，因此数据丢失可能相当大。在将大整数类型转换为小整数类型（例如 `long` 到 `short`）、有符号到无符号或无符号到有符号时，值也可能被修改。

提升规则适用于包含两种或更多数据类型的表达式；此类表达式也称为 *混合类型表达式*。混合类型表达式中每个值的类型都会提升为表达式中的“最高”类型（实际上为表达式创建并使用每个值的临时版本——原始值保持不变）。当函数参数的类型与函数定义或原型中指定的参数类型不匹配时也会发生提升。图 6.5 按从“最高类型”到“最低类型”的顺序列出了基本数据类型。

将值转换为较低的基本类型可能会导致错误的值。因此，只能通过显式将值赋给较低类型的变量（某些编译器在此情况下会发出警告）或使用强制转换运算符（参见第 4.7 节）将值转换为较低的基本类型。函数参数值被转换为函数原型中的参数类型，就好像它们被直接赋给这些类型的变量一样。如果使用整数参数的 `square` 函数被浮点参数调用，则参数将被转换为 `int`（较低类型），并且 `square` 可能会返回错误的值。例如，`square(4.5)` 返回 16，而不是 20.25。

## 常见编程错误 6.5

从提升层次结构中的较高数据类型转换为较低类型，或在有符号和无符号之间转换，可能会损坏数据值，导致信息丢失。

## 常见编程错误 6.6

如果函数调用中的参数与相应函数原型中声明的参数数量和类型不匹配，则为编译错误。如果调用中的参数数量匹配，但参数无法隐式转换为预期类型，也是错误。

| Data types |
|---|
| *long double* |
| *double* |
| *float* |
| *unsigned long int* (synonymous with *unsigned long*) |
| *long int* (synonymous with *long*) |
| *unsigned int* (synonymous with *unsigned*) |
| *int* |
| *unsigned short int* (synonymous with *unsigned short*) |
| *short int* (synonymous with *short*) |
| *unsigned char* |
| *char* |
| *bool* |

**Fig. 6.5** | Promotion hierarchy for fundamental data types.

## 6.6 C++ 标准库头文件

C++ 标准库分为许多部分，每部分都有自己的头文件。头文件包含构成库每个部分的 related 函数的函数原型。头文件还包含各种类类型和函数的定义，以及这些函数所需的常量。头文件“指示”编译器如何与库和用户编写的组件进行接口。

图 6.6 列出了一些常见的 C++ 标准库头文件，其中大多数将在本书后面讨论。图 6.6 中多次使用的术语“宏”将在附录 D、预处理器中详细讨论。以 `.h` 结尾的头文件名是已被 C++ 标准库头文件取代的“旧式”头文件。我们在本书中仅使用 C++ 标准库版本的每个头文件，以确保我们的示例可在大多数标准 C++ 编译器上运行。

| C++ Standard Library header file | Explanation |
|---|---|
| <iostream> | Contains function prototypes for the C++ standard input and standard output functions, introduced in Chapter 2, and is covered in more detail in Chapter 15, Stream Input/Output. This header file replaces header file <iostream.h>. |
| <iomanip> | Contains function prototypes for stream manipulators that format streams of data. This header file is first used in Section 4.7 and is discussed in more detail in Chapter 15, Stream Input/Output. This header file replaces header file <iomanip.h>. |
