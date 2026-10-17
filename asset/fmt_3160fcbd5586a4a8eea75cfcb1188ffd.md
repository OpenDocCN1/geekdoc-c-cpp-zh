
```cpp
// 标记宝藏已找到
cout << "在 (" << colGuessed << ", " << rowGuessed << ") 找到了宝藏" << endl;
island[rowGuessed][colGuessed] = 'F';
}
else
{
    // 此处没有宝藏 - 失去一次生命
    cout << "这里什么也没有。" << endl;
    guessesLeft--;
} // if-else 结束
cout << endl; // 每次猜测后显示空行
} // while 循环结束
// 游戏结束
cout << "机会用完了!" << endl;
// 使用循环访问项目并在屏幕上显示网格
for (row = 0; row < NUM_ROWS; row++)
{
    for (col = 0; col < NUM_COLS; col++)
    {
        cout << island[row][col];
    }
    cout << endl; // 行结束时移动到新行
} // 行循环结束
return 0;
}
```

# 第10章：函数

## 什么是函数？

在计算机发展的早期，许多计算机程序比现在要短得多、简单得多。程序通常只由单个代码文件组成，正如书中的许多示例所示。现代程序变得越来越复杂，包含的功能和代码行比以前任何时候都要多。大多数程序员发现，将程序分成不同的部分以便代码更容易理解是非常关重要的。

组织程序代码常用的方法之一是使用函数。函数与数学中的函数非常相似——它们就像是为你完成某些有用工作的机器。函数是一个命名的代码块，可以由程序的任何其他部分激活以执行任务。

我们可以创建一个函数来执行程序需要完成的每个特定任务，例如对数据进行排序或将数据保存到文件中。函数在创建易于理解的程序时极其重要。它们还可以帮助你发现并修正代码中的错误，因为当程序运行不正常时，可以帮助你知道从哪里开始解决问题。

一旦创建，程序的其他部分就可以使用给定的名称来激活（或“调用”）该函数。单个函数在程序执行过程中可以激活多次，从而减少所需的代码行数。通过重复调用函数可以显著减少程序中的语句数量。

以下是一个程序可能使用的函数示例：

| 原始字符串值 | 函数 | 改变后的字符串值 |
| :--- | :--- | :--- |
| "Hello" | input makeStringUpperCase output (result) | "HELLO" |

函数总是需要一个名称，以便与程序的其它部分区分开，并允许函数代码在别处激活。在上面的示例中，函数的名称是 `makeStringUppercase`。

函数可以接受一些数据作为输入。然后它通常会对数据进行某种处理，最后返回一个结果作为输出。在上面的示例中，函数 `makeStringUppercase()` 接收一个字符串输入，值 "Hello"。

许多函数在执行完成后会产生一个结果作为输出。函数 `makeStringUppercase()` 处理输入值 "Hello" 并返回一个不同的字符串值作为结果："HELLO"。

我们可以从程序代码的其他处一次或多次激活 `makeStringUppercase()` 函数，每次给它输入不同的字符串值，以产生不同的输出结果：

| 原始字符串值 | 函数 | 改变后的字符串值 |
| :--- | :--- | :--- |
| "gnu" | input makeStringUpperCase output (result) | "GNU" |

通过这样重复使用相同的函数代码，意味着我们不必在程序中编写多份相同的代码副本。我们编写一次函数代码，然后根据需要多次调用它。这通常会导致 C++ 程序更短且错误更少。

## 在 C++ 中创建函数

我们如何在 C++ 中实际创建这样的函数呢？

首先，在创建函数时，我们需要考虑以下每一点：

- 函数名称，它将用于从代码的其他部分调用它。
- 函数所需的任何输入，包括每个输入的数据类型和每个输入的名称。
- 输出 - 将返回给调用代码的何种类型的数据（如果有的话）。最多情况下，一个函数一次只能返回一个值。

我们还需要为函数创建一个函数体。这是一块 C++ 语句，在每次调用该函数时都会执行。

下面是函数的一些示例，以及它们接受的参数和每个函数返回的数据类型。每个函数都包含一组 `{` 大括号 `}` 来包含实际执行工作的函数体。在这些示例中，我目前留了每个函数的函数体为空。

```cpp
// 这个名为 main 的函数不接受任何参数。
// 它返回一个整数值作为结果。
int main()
{
```

```cpp
// 这个名为 scrambleMessage 的函数需要一个字符串，名为 originalText，
// 以及一个整数，名为 lettersToShiftBy
string scrambleMessage(string originalText, int lettersToShiftBy)
{
```

```cpp
// 这个名为 findSmallestValue 的函数需要两个整数，
// 一个名为 firstNumber，另一个名为 secondNumber
int findSmallestValue(int firstNumber, int secondNumber)
{
```

C++ 代码以返回类型开始，后面是函数名，然后是括号中的参数。函数体在大括号内。

### 函数名称

每个函数在程序中必须有一个唯一的名称，以避免混淆。名称标识了函数的功能。在选择名称时，请遵循这些指南：

- 使用指示函数用途的描述性名称。
- 使用驼峰法或下划线（例如 `calculateTotal` 或 `calculate_total`）。
- 避免使用 C++ 保留作为函数名。
- 保持名称较短，但长到足以意义。

### 函数的输入值

在创建新函数时，你必须告诉编译器函数是否期望某些输入。

正如前面描述，许多函数在激活时会接收一个或多个数据值。这些输入值通常被称为“参数”。函数通常会使用这些输入值并对其进行某些处理。

因为输入到函数的通常有多个输入值，所以每个输入值也必须有一个参数名称，以便函数可以使用它而不会与其他输入值混淆。函数内部的代码可以使用参数名称在处理数据时引用每个单独的值。

我们还必须告诉编译器函数期望处理每个参数的何种类型的数据（例如 `string`、`int` 或 `float` 值）。

让编译器用正确类型的输入值检查每个函数调用是非常关重要的，否则函数可能无法正确处理数据。想象一下，如果函数 `makeStringUppercase()` 在被告知期望 `string` 值时，却被给出了一个 `float` 值。将一个 `float` 值转换为大写是没有意义的，因此编译器会给出一个错误。

| 字符串值名 originalText | input | 函数 scrambleMessage output | 字符串值 result (混乱后的文本) |
| :--- | :--- | :--- | :--- |
| int 值名 lettersToShiftBy | input | | |

上面的图表显示了函数如何使用凯撒密码来混乱消息。它将接受两个参数作为输入：一个消息 `originalText` 和一个告诉消息中每个字母需要位移多少位的数字 `lettersToShiftBy`。它将产生一个结果作为输出——一个包含混乱消息的 `string` 值。

### 不接受任何输入参数的函数

某些函数在执行时完全不需要任何数据。它们不接受任何参数作为输入，我们只需要使用它们的名称来调用它们，而无需向它们提供任何值。

例如，一个函数可能会在屏幕上显示文本列表，但实际上并不处理数据值。请注意，调用此类函数时始终需要一对空的圆括号 `()`，即使它不需要任何参数。

```cpp
displayMenu();
```

另一个不接受任何输入值的函数示例是 C++ 函数 `random()`，我们在之前的程序中已经用过它：

| 无传递给函数的输入值 | 函数 random | 输出（结果） | 生成一个 int 值（例如 2374） |
| :--- | --- | --- | --- |

我们可以像这样调用 `random()` 函数：

```cpp
int chosenNumber = random();
```

你可以看到，它被用作赋值语句的一部分。整数变量 `chosenNumber` 被设置为 `random()` 函数调用的结果。

### 函数的函数体和返回值

一旦函数完成执行，它可能会向调用它的代码返回某些内容。这个被“返回”的结果可以被程序用于进一步处理。函数在完成后给出的数据值被称为“返回值”。但这是如何实现的呢？

首先，在创建函数时，我们必须定义函数在执行完成后返回什么种类型的数据（如果有）。我们还必须给函数起一个名称，并定义它作为输入所需的任何数据——即函数的参数。

现在我们可以告诉函数实际上应该做什么了。这被称为函数的“函数体”。它是一组一个或多个语句，当函数被你程序的其他部分调用时，它将执行这些语句。语句被放置在花括号 `{ }` 内部，并带有一个或多个 `return` 语句，将结果传回调用代码。

下面是一个程序的标准 `main()` 函数，在这种情况下，它不接受任何参数作为输入，但在函数完成后会返回一个单一的 `int`：

```cpp
int main() {
  // 此函数命名为 main。它不接受任何参数作为输入。
  // 函数体包含执行某些操作的语句。
  // 它在执行完成后返回整数值零。
  return 0;
}
```

下面的函数接受不同的值作为参数：一个字符串和一个 `int` 值。它会打乱字符串的原始内容。完成后，它返回打乱后的结果：

```cpp
string scrambleMessage( string originalText, int lettersToShiftBy )
{
  // 此函数命名为 scrambleMessage。
  // 它接受两个输入值：一个名为 originalText 的字符串
  // 和一个名为 lettersToShiftBy 的整数。
  // 它在执行完成后返回一个字符串。
  string scrambledResult = "";
  for ( unsigned int pos = 0; pos < originalText.length(); pos++)
    scrambledResult += originalText( pos ) + lettersToShiftBy;
  // 返回一个字符串值
  return scrambledResult;
}
```

最后一个函数接受两个 `int` 值作为输入。它决定两个输入中哪一个最小，并将这个最小值作为 `int` 结果返回：

```cpp
int findSmallestValue( int firstNumber, int secondNumber )
{
  // 此函数命名为 findSmallestValue。
  // 它接受两个输入值 firstNumber 和 secondNumber，
  // 这两个都是整数。
  // 它在执行完成后返回一个整数值。
  // 返回一个 int 值，取决于哪一个是最小的输入值
  return ( firstNumber < secondNumber ) ? firstNumber : secondNumber;
}
```

注意，每个函数体内部的 `return` 语句实际上是将结果返回给它调用的代码。

我们在许多程序中已经遇到过 C++ 关键字 `return`。事实上，到目前为止我们几乎所有的 C++ 程序都由一个名为 `main()` 的函数组成，该函数不接受数据值作为输入，并向 Linux 操作系统返回一个 `int` 值“错误”代码。通过这种方式，你实际上可以将 C++ 程序本身视为一种函数。

`return` 语句通常但并不总是函数体中的最后一个语句。某些函数甚至可能包含多个 `return` 语句，也许作为决策过程的结果。

记住，一旦执行了 `return` 语句，程序的执行流就会从函数传回调用它的代码，并带有返回的结果。

### 调用函数

一旦创建了函数，就可以从程序的其他部分激活它。我们可以使用它的名称调用函数。

例如：

```cpp
displayRandomWords( 10 );
```

这可能会调用名为 `displayRandomWords()` 的函数，告诉它从字典中随机选取10个单词。在这种情况下，这是一个 `void` 函数，不产生任何结果——没有返回任何值，值只是显示在屏幕上。

同一个函数可以根据你提供的提供的输入值执行不同的事情。可以再次调用该函数，但这次告诉它只显示3个随机单词，因此提供给函数的输入值会影响它的行为：

```cpp
displayRandomWords( 3 );
```

下面的程序调用了一个名为 `factorial()` 的函数。该函数接受一个正整数作为参数，然后返回该数的阶乘作为结果。

如果你不熟悉数学中的阶乘，这里有一个示例：

```cpp
int factorial(int n) {
    int result = 1;
    for(int i = 1; i <= n; i++) {
        result *= i;
    }
    return result;
}
```

当程序运行时，你可以看到执行流是如何受到调用 `rollSingle()` 函数的影响的：

```
Started in main function
In rollSingle function
Finishing rollSingle function
I rolled 9
In rollSingle function
Finishing rollSingle function
Then I rolled 50
In rollSingle function
Finishing rollSingle function
Finally I rolled 2
Finishing main function
```

## 使用函数调用返回的结果

正如我们所见，调用函数时，你的程序通常期望返回某种对代码其他部分有用的结果。

返回的值有多种使用方式。

为了激活之前示例中调用的 `makeUpperCase()` 函数并获取结果，我们可以写道：

```
makeUpperCase("Hello"); // 调用函数，以 "Hello" 为输入
```

这本身并没有对返回的字符串值（对于输入 "Hello"，结果为 "HELLO"）进行任何操作。它实际上并没有真正使用函数返回给调用代码的结果。如果你尝试编译一个包含此类调用的程序，编译器会发出警告。它会警告你，函数返回的值从未被获取，并且实际上它被丢弃了。

返回值的一种可能用途将其显示在屏幕上。我们可以将函数的返回值重定向到 `channel-out`（屏幕）：

```
cout << makeUpperCase("Hello"); // 调用函数，显示结果
```

这会将值 "Hello" 作为输入，将其更改为大写，并在屏幕上显示结果 "HELLO"。

我们可以再次调用同一个函数，赋予它不同的输入数据并获得不同的结果：

```
cout << makeUpperCase("gnu");
```

对于原始字符串值 `gnu`，这将在屏幕上显示结果 `GNU`。

节省努力！在循环中重复调用函数

很多时候，在费力创建了一个函数之后，我们可能想在程序中使用它多次。
下面的示例显示了该函数的精简版本。注意，我删除了之前用于帮助我们追踪运行程序中执行流的 `cout` 语句。

该程序包含一个简单的循环，该循环使用控制变量 `number` 从 1 计数到 10。
循环的每次迭代都会调用 `factorial()` 函数，并将 `number` 的值传递给它。函数返回的结果将作为 `cout` 语句的一部分显示出来。

### 示例 10.3–function_factorial.cpp

```
#include <iostream>      // 程序将使用屏幕
using namespace std;              // 将使用标准标识符 cout 和 endl
//-------------------------------------------------
unsigned int factorial(unsigned int num)
{
    unsigned int result = 1;
    for (unsigned int index = 1; index <= num; index++)
        result = result * index;
    return result;
}
//-------------------------------------------------
int main() {
    // 重复调用 factorial() 函数来显示 1 到 10 之间
    // 数字的阶乘
    for (unsigned int number = 1; number <= 10; number++)
        cout << number << "! " << factorial(number) << endl;
    return 0;
}
```

执行时，你应该看到以下结果：

![](img/0c86cf81300257fe2415e40f8fb03508_332_0.png)

第 10 章：函数 331

下面的另一个函数将接收一个整数并将其自身相乘

```cpp
int squareMyNumber( int startingNumber ) {
```
