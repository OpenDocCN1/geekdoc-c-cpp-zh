

```
file1
int volts;
double current;
static double power;
.
.
int main()
{
    func1();
    func2();
    func3();
    func4();
}
int func1()
{
    .
    .
}
int func2()
{
    .
    .
    .
}
```

```
file2
double factor;
int func3()
{
    .
    .
}
int func4()
{
    .
    .
    .
}
```

## 图 6.13 程序可以跨越多个文件

对于图 6.13 中所示的文件，在 file1 中声明的全局变量 volts、current 和 power 只能被该文件中的 main()、func1() 和 func2() 函数使用。在 file2 中声明的唯一全局变量 factor 只能被 file2 中的 func3() 和 func4() 函数使用。

虽然变量 volts 是在 file1 中创建的，但您可能希望在 file2 中使用它。为此，您需要在 file2 中放置声明语句 `extern int volts;`，如图 6.14 所示。将此语句放在 file2 的顶部会将 volts 的作用域扩展到 file2，以便 func3() 和 func4() 都能使用它。extern 指定符只是声明一个在另一个文件中定义的全局变量。因此，在 func4() 中放置语句 `extern double current;` 会将这个在 file1 中创建的全局变量的作用域扩展到 func4()。此外，通过在 func1() 之前放置声明语句 `extern double factor;`，可以将 file2 中创建的全局变量 factor 的作用域扩展到 func1() 和 func2()。请注意，factor 对 main() 不可用。

```
file1
int volts;
extern double current;
static double power;
.
.
int main()
{
func1();
func2();
func3();
func4();
}
extern double factor;
int func1()
{
.
.
}
int func2()
{
.
.
}
```

```
file2
double factor;
extern int volts;
int func3()
{
.
.
}
int func4()
{
extern double current;
.
.
}
```

## 图 6.14 扩展全局变量的作用域

包含关键字 `extern` 的声明语句与其他声明语句不同，它不会通过为变量保留新的存储空间来创建新变量。extern 声明语句只是告知计算机某个全局变量已经存在，现在可以使用了。该变量的实际存储空间必须在程序的其他位置通过使用一条（且仅一条）未使用关键字 `extern` 的全局声明语句来创建。当然，全局变量可以在其原始声明中进行初始化。但是，在 extern 声明语句中初始化是不允许的，会导致编译错误。

extern 存储类别的存在是仔细区分变量创建与声明的原因。包含关键字 `extern` 的声明语句不会创建新的存储区域；它们只是扩展现有全局变量的作用域。

最后一个全局存储类别 `static` 用于防止将全局变量扩展到第二个文件中。全局静态变量的声明方式与局部静态变量相同，只是声明语句放在任何函数之外。

全局静态变量的作用域不能扩展到声明它的文件之外。此规则为全局静态变量提供了一定程度的隐私性。因为它们只能在其声明所在的文件中“被知晓”和使用，其他文件无法访问或更改它们的值。因此，全局静态变量随后不能通过使用 extern 声明语句扩展到第二个文件。尝试这样做会导致编译错误。

## 信息点

### 存储类别

`auto` 和 `register` 类型的变量始终是局部变量。只有非静态的全局变量才能使用 `extern` 关键字声明。这样做会将变量的作用域扩展到另一个文件或函数。

将全局变量设为 `static` 会使该变量对其声明所在的文件保持私有。因此，静态变量不能使用 `extern` 关键字。除了静态变量之外，所有变量在每次进入其作用域时都会被初始化；静态变量只在定义时初始化一次。

## 练习 6.5

1. （练习）a. 列出可用于局部变量的存储类别。
   b. 列出可用于全局变量的存储类别。

2. （练习）描述局部 `auto` 变量和局部 `static` 变量之间的区别。

3. （练习）以下函数之间有什么区别？

```
void init1()
{
    static int yrs = 1;

    cout << "The value of yrs is " << yrs << endl;
    yrs = yrs + 2;

    return;
}
```

```
void init2()
{
    static int yrs;

    yrs = 1;
    cout << "The value of yrs is " << yrs << endl;
    yrs = yrs + 2;

    return;
}
```

## 使用函数实现模块化

4. （练习）
   a. 描述全局 `static` 变量和全局 `extern` 变量之间的区别。
   b. 如果变量使用 `extern` 存储类别声明，程序中必须存在哪些其他声明语句？

5. （练习）声明语句 `static double years;` 可用于创建局部或全局静态变量。什么决定了变量 `years` 的作用域？

6. （练习）对于图 6.15 中显示的函数和变量声明，放置一个 `extern` 声明以实现以下每个目标：
   a. 将全局变量 `choice` 的作用域扩展到 `file2`。
   b. 仅将全局变量 `flag` 的作用域扩展到 `average()` 函数。
   c. 将全局变量 `date` 的作用域扩展到 `average()` 和 `variance()`。
   d. 仅将全局变量 `date` 的作用域扩展到 `roi()`。
   e. 仅将全局变量 `coupon` 的作用域扩展到 `roi()`。
   f. 将全局变量 `bondtype` 的作用域扩展到 `file1`。
   g. 将全局变量 `maturity` 的作用域扩展到 `watts()` 和 `thrust()`。

```
file1
char choice;
int flag;
long date, time;
int main()
{
    .
    .
    .
}
double factor;
double watts()
{
    .
    .
    .
}
double thrust()
{
    .
    .
    .
}
```

```
file2
char bondtype;
double resistance;
double roi()
{
    .
    .
    .
}
double average()
{
    .
    .
    .
}
double variance()
{
    .
    .
    .
}
```

![](img/e9bf940282dfb289356f077151cc69dd_303_0.png)

## 6.6 常见编程错误

在构造和使用函数时，以下编程错误很常见：

1. 与函数相关的一个极其常见的错误是传递了不正确的数据类型。传递给函数的值必须与为函数声明的参数数据类型相对应。验证是否接收到正确值的一种方法是在进行任何计算之前，在函数体内显示所有传递的值。完成此验证后，您可以不再显示这些值。¹⁷

2. 另一个常见错误可能发生在调用函数和被调用函数中都局部声明了同一个变量时。即使变量名相同，对一个局部变量的更改也不会改变另一个局部变量中的值。

3. 一个相关的错误是当局部变量与全局变量同名时可能发生的错误。在声明该局部变量的函数内部，除非使用作用域解析运算符 `::`，否则使用该变量名只会影响局部变量的内容。

4. 另一个常见错误是在调用函数之前或之内省略被调用函数的原型。必须告知被调用函数要返回的值的类型，而函数原型提供了此信息。如果被调用函数在程序中位于其调用函数之前，则可以省略原型。虽然允许省略返回整数的函数的原型和返回类型，但这样做是不良的文档编写实践。可以通过在返回值之前和之后显示它来验证函数实际返回的值。

5. 最后两个常见错误是用分号终止函数头，以及忘记在函数头中包含函数参数的数据类型。

## 6.7 章节总结

1. 通过给出函数名并在名称后面的括号中传递任何数据来调用函数。如果变量是函数调用中的参数之一，则被调用函数会收到该变量值的副本。

2. 用户编写函数的常见形式如下：

```
returnDataType functionName(parameter list)
{
    Symbolic constants
    Variable declarations

    C++ statements
    return expression;
}
```

函数的第一行称为函数头。函数的左、右花括号以及这些花括号之间的所有语句构成函数体。参数列表是一个逗号分隔的参数声明列表。

