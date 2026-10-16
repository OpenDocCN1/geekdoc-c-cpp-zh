
You can download the code for this program from the Course Technology website (`www.courseptr.com/downloads`). The program is in the Chapter 7 folder; the filename is `pointing.cpp`.

![](img/34f09be0ed6217c465debc4490197d4f_246_0.png)

Figure 7.1

The pointer `pScore` first points to the variable `score` and then to the variable `newScore`, while the pointer `pStr` points to the variable `str`.

// Pointing

// Demonstrates using pointers

```
#include <iostream>

#include <string>

using namespace std;

int main()

{

    int* pAPointer;    //declare a pointer

    int* pScore = 0;    //declare and initialize a pointer

    int score = 1000;

    pScore = &score;    //assign pointer pScore address of variable score

    cout << "Assigning &score to pScore\n";

    cout << "&score is: " << &score << "\n";    //address of score variable

    cout << "pScore is: " << pScore << "\n";    //address stored in pointer

    cout << "score is: " << score << "\n";

    cout << "*pScore is: " << *pScore << "\n\n"; //value pointed to by pointer

    cout << "Adding 500 to score\n";

    score += 500;

    cout << "score is: " << score << "\n";

    cout << "*pScore is: " << *pScore << "\n\n";

    cout << "Adding 500 to *pScore\n";

    *pScore += 500;

    cout << "score is: " << score << "\n";

    cout << "*pScore is: " << *pScore << "\n\n";

    cout << "Assigning &newScore to pScore\n";

    int newScore = 5000;

    pScore = &newScore;

    cout << "&newScore is: " << &newScore << "\n";

    cout << "pScore is: " << pScore << "\n";

    cout << "newScore is: " << newScore << "\n";

    cout << "*pScore is: " << *pScore << "\n\n";

cout << "Assigning &str to pStr\n";

string str = "score";

string* pStr = &str;    //pointer to string object

cout << "str is: " << str << "\n";

cout << "*pStr is: " << *pStr << "\n";

cout << "(*pStr).size() is: " << (*pStr).size() << "\n";

cout << "pStr->size() is: " << pStr->size() << "\n";

return 0;

}
```

## 声明指针

在 `main()` 中的第一条语句中，我声明了一个名为 `pAPointer` 的指针。

```
int* pAPointer;    //declare a pointer
```

由于指针的工作方式非常独特，程序员经常在指针变量名前面加上字母“p”，以提醒他们该变量确实是一个指针。

就像迭代器一样，指针被声明为指向特定类型的值。`pAPointer` 是一个指向 `int` 的指针，这意味着它只能指向一个 `int` 值。例如，`pAPointer` 不能指向一个 `float` 或一个 `char`。另一种说法是，`pAPointer` 只能存储一个 `int` 的地址。

要声明自己的指针，请从指针将要指向的对象的类型开始，然后跟一个星号，然后是指针名称。当你声明指针时，可以在星号的两侧放置空白。所以 `int* pAPointer;`、`int *pAPointer;` 和 `int * pAPointer;` 都声明了一个名为 `pAPointer` 的指针。

### 陷阱

当你声明一个指针时，星号仅适用于紧随其后的单个变量名。因此，以下语句将 `pScore` 声明为指向 `int` 的指针，而 `score` 声明为 `int`。

```
int* pScore, score;
```

`score` 不是指针！它是一个类型为 `int` 的变量。一种使其更清晰的方法是调整空白并将语句重写为：

```
int *pScore, score;
```

然而，最清晰的声明指针的方法是在其自己的语句中声明它，如以下几行所示。

```
int* pScore;
int score;
```

## 初始化指针

与其他变量一样，你可以在声明指针的同一语句中初始化它。这就是我接下来用以下行所做的，它将 `0` 分配给 `pScore`。

```
int* pScore = 0; //declare and initialize a pointer
```

将 `0` 分配给指针具有特殊含义。松散地翻译，它的意思是：“指向 nothing。” 程序员称值为零的指针为空指针。你应该在声明指针时始终为其初始化一些值，即使该值为零。

## 提示

许多程序员将 `NULL` 分配给指针而不是 `0`，以使指针成为空指针。`NULL` 是一个在多个库文件中定义的常量，包括 `iostream`。

## 为指针分配地址

由于指针存储对象的地址，你需要一种方法将地址放入指针中。一种方法是获取现有变量的内存地址并将其分配给指针。这就是我在以下行中所做的，它获取变量 `score` 的地址并将其分配给 `pScore`。

```
pScore = &score; //assign pointer address of variable score
```

我通过在变量名前面加上 `&`、取地址运算符来获取 `score` 的地址。（是的，你以前见过 `&` 符号，当它用作引用运算符时。然而，在这种上下文中，`&` 符号获取对象的地址。）

作为前一行代码的结果，`pScore` 包含 `score` 的地址。就好像 `pScore` 精确知道 `score` 在计算机内存中的位置。这意味着你可以使用 `pScore` 访问 `score` 并操作存储在 `score` 中的值。图 7.2 作为 `pScore` 和 `score` 之间关系的视觉说明。

![](img/34f09be0ed6217c465debc4490197d4f_250_0.png)

图 7.2

指针 `pScore` 指向 `score`，`score` 存储值 `1000`。

为了证明 `pScore` 包含 `score` 的地址，我使用以下行显示变量的地址和指针的值。

```
cout << "&score is: " << &score << "\n";    //address of score variable
cout << "pScore is: " << pScore << "\n";    //address stored in pointer
```

`pScore` 包含 `0x22ff5c`，这是 `score` 的地址。（`Pointing` 程序在你的系统上显示的具体地址可能不同。重要的是 `pScore` 和 `&score` 的值是相同的。）

## 解引用指针

就像你解引用迭代器以访问它所引用的对象一样，你解引用指针以访问它所指向的对象。你以同样的方式完成解引用——使用 `*`，解引用运算符。我将解引用运算符用于以下行，该行显示 `1000`，因为 `*pScore` 访问存储在 `score` 中的值。

```
cout << "*pScore is: " << *pScore << "\n\n"; //value pointed to by pointer
```

记住，`*pScore` 的意思是，“`pScore` 所指向的对象。”

### 陷阱

> 不要解引用空指针，因为它可能导致灾难性的结果。

接下来，我用以下行将 `500` 加到 `score`。

```
score += 500;
```

当我将 `score` 发送到 `cout` 时，会显示 `1500`，就像你期望的那样。当我将 `*pScore` 发送到 `cout` 时，`score` 的内容再次被发送到 `cout`，并且再次显示 `1500`。

接下来，我用以下行将 `500` 加到 `pScore` 所指向的值。

```
*pScore += 500;
```

由于 `pScore` 指向 `score`，前一行代码将 `500` 加到 `score`。因此，当我接下来将 `score` 发送到 `cout` 时，会显示 `2000`。然后，当我将 `*pScore` 发送到 `cout`...你猜对了，会再次显示 `2000`。

### 陷阱

当你想更改指针所指向对象的数值时，不要更改指针的值。例如，如果我想将 `pScore` 所指向的 `int` 加 `500`，那么以下行将是一个大错误。

```
pScore += 500;
```

前面的代码将 `500` 加到存储在 `pScore` 中的地址，而不是加到 `pScore` 原本指向的值。因此，`pScore` 现在指向可能包含任何内容的某个地址。像这样解引用指针可能导致灾难性的结果。

## 重新分配指针

与引用不同，指针可以在程序生命周期的不同时间指向不同的对象。重新分配指针的工作方式与重新分配任何其他变量一样。接下来，我用以下行重新分配 `pScore`。

```
pScore = &newScore;
```

作为结果，`pScore` 现在指向 `newScore`。为了证明这一点，我通过将 `&newScore` 发送到 `cout` 来显示 `newScore` 的地址，然后是存储在 `pScore` 中的地址。两个语句都显示相同的地址。然后我将 `newScore` 和 `*pScore` 发送到 `cout`。两者都显示 `5000`，因为它们都访问存储此值的同一块内存。

### 陷阱

当你想更改指针本身时，不要更改指针所指向的值。例如，如果我想更改 `pScore` 以指向 `newScore`，那么以下行将是一个大错误。

```
*pScore = newScore;
```

此代码只是更改 `pScore` 当前指向的值；它不会更改 `pScore` 本身。如果 `newScore` 等于 `5000`，则前面的代码等同于 `*pScore = 5000;` 而 `pScore` 仍然指向分配前相同的变量。

## 使用对象指针

到目前为止，`Pointing` 程序只处理内置类型 `int` 的值。但你也可以像使用值一样轻松地使用对象指针。我接下来用以下几行来演示这一点，这些行创建了 `str`，一个等于 `"score"` 的字符串对象，以及 `pStr`，一个指向该对象的指针。

```
string str = "score";
string* pStr = &str;    //pointer to string object
```

`pStr` 是指向 `string` 的指针，意味着它可以指向任何字符串对象。另一种说法是 `pStr` 可以存储任何字符串对象的地址。

你可以使用解引用运算符通过指针访问对象。这就是我接下来用以下这一行所做的。

```
cout << "*pStr is: " << *pStr << "\n";
```

通过使用解引用运算符 `*pStr`，我将 `pStr` 指向的对象 `str` 发送到 `cout`。结果，文本 `score` 被显示出来。

你可以通过指针调用对象的成员函数，就像你可以通过迭代器调用对象的成员函数一样。一种方法是使用解引用运算符和成员访问运算符，这就是我接下来用以下几行所做的。

```
cout << "(*pStr).size() is: " << (*pStr).size() << "\n";
```

代码 `(*pStr).size()` 的意思是：“取解引用 `pStr` 的结果并调用该对象的 `size()` 成员函数。” 因为 `pStr` 引用等于 `"score"` 的字符串对象，所以代码返回 `5`。

## 提示

每当你解引用指针以访问数据成员或成员函数时，请用一对括号将解引用的指针括起来。这可以确保点运算符会被应用于指针所指向的对象。

就像迭代器一样，你可以使用 `->` 运算符与指针，以更易读的方式访问对象成员。这就是我接下来用以下这一行演示的。

```
cout << "pStr->size() is: " << pStr->size() << "\n";
```

前面的语句再次显示了等于 `"score"` 的字符串对象中的字符数；然而，这次我可以用 `pStr->size()` 替代 `(*pStr).size()`，使代码更易读。

## 理解指针和常量

在你能在游戏程序中有效地使用指针之前，还有一些指针机制需要你理解。你可以使用 `const` 关键字来限制指针的工作方式。这些限制可以作为安全保障，并能使你的编程意图更清晰。由于指针非常灵活，限制指针的使用方式符合编程格言“只请求你需要的”。

### 使用常量指针

正如你所见，指针可以在程序的不同时间指向不同的对象。然而，通过在声明和初始化指针时使用 `const` 关键字，你可以限制指针使其只能指向它被初始化时指向的对象。这种指针称为常量指针。另一种说法是存储在常量指针中的地址永远不会改变——它是常量。以下是创建常量指针的示例：

```
int score = 100;
int* const pScore = &score;  //a constant pointer
```

前面的代码创建了一个指向 `score` 的常量指针 `pScore`。你通过在声明指针时将 `const` 放在指针名称的正前方来创建常量指针。

像所有常量一样，你必须在第一次声明常量指针时对其进行初始化。以下这一行是非法的，并且会产生一个大大的编译错误。

```
int* const pScore;  //illegal - - you must initialize a constant pointer
```

因为 `pScore` 是常量指针，所以它永远不能指向任何其他内存位置。以下代码也是相当非法的。

```
pScore = &anotherScore;  //illegal - pScore can't point to a different object
```

虽然你不能改变 `pScore` 本身，但你可以使用 `pScore` 来改变它所指向的值。以下这一行是完全合法的。

```
*pScore = 500;
```

困惑吗？不要。完全可以使用常量指针来改变它所指向的值。记住，常量指针的限制是其值——指针存储的地址——不能改变。

常量指针的工作方式应该让你想起某样东西——引用。就像引用一样，常量指针只能引用它被初始化时引用的对象。

## 提示

虽然你可以在程序中使用常量指针代替引用，但只要可能，你应该坚持使用引用。引用比指针具有更简洁的语法，并且可以使你的代码更易读。

### 使用指向常量的指针

正如你所见，你可以使用指针来改变它们所指向的值。然而，通过在声明指针时使用 `const` 关键字，你可以限制指针使其不能用于改变它所指向的值。这种指针称为指向常量的指针。以下是声明此类指针的示例：

```
const int* pNumber;  //a pointer to a constant
```

前面的代码声明了一个指向常量的指针 `pNumber`。你通过将 `const` 放在指针将要指向的值类型的正前方来声明指向常量的指针。

你按之前的方式为指向常量的指针分配地址。

```
int lives = 3;
pNumber = &lives;
```

然而，你不能使用该指针来改变它所指向的值。以下这一行是非法的。

```
*pNumber -= 1;  //illegal - - can't use pointer to a constant to change value
//that pointer points to
```

虽然你不能使用指向常量的指针来改变它所指向的值，但指针本身可以改变。这意味着指向常量的指针

可以在程序中指向不同的对象。以下代码是完全合法的。

```
const int MAX_LIVES = 5;
pNumber = &MAX_LIVES;  //pointer itself can change
```

### 使用指向常量的常量指针

指向常量的常量指针结合了常量指针和指向常量的指针的限制。这意味着指向常量的常量指针只能指向它被初始化时指向的对象。此外，它不能用于改变它所指向的对象的价值。以下是此类指针的声明和初始化：

```
const int* const pBONUS = &BONUS;  //a constant pointer to a constant
```

前面的代码创建了一个指向常量 `BONUS` 的常量指针到常量 `pBONUS`。

## 提示

像指向常量的指针一样，指向常量的常量指针可以指向非常量或常量值。

你不能重新分配指向常量的常量指针。以下这一行不合法。

```
pBONUS = &MAX_LIVES;  //illegal - - pBONUS can't point to another object
```

你不能使用指向常量的常量指针来改变它所指向的值。这意味着以下这一行是非法的。
