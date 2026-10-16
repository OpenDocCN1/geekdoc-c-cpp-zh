
// Pointing
// Demonstrates using pointers

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

## 声明指针

在 main() 中的第一条语句中，我声明了一个名为 pAPointer 的指针。

```
int* pAPointer;    //declare a pointer
```

由于指针的工作方式非常独特，程序员经常在指针变量名前面加上字母“p”，以提醒他们该变量确实是一个指针。

就像迭代器一样，指针被声明为指向特定类型的值。pAPointer 是一个指向 int 的指针，这意味着它只能指向一个 int 值。例如，pAPointer 不能指向一个 float 或一个 char。另一种说法是，pAPointer 只能存储一个 int 的地址。

要声明自己的指针，请从指针将要指向的对象的类型开始，然后跟一个星号，然后是指针名称。当你声明指针时，可以在星号的两侧放置空白。所以 int* pAPointer;、int *pAPointer; 和 int * pAPointer; 都声明了一个名为 pAPointer 的指针。

### 陷阱

当你声明一个指针时，星号仅适用于紧随其后的单个变量名。因此，以下语句将 pScore 声明为指向 int 的指针，而 score 声明为 int。

```
int* pScore, score;
```

score 不是指针！它是一个类型为 int 的变量。一种使其更清晰的方法是调整空白并将语句重写为：

```
int *pScore, score;
```

然而，最清晰的声明指针的方法是在其自己的语句中声明它，如以下几行所示。

```
int* pScore;
int score;
```

## 初始化指针

与其他变量一样，你可以在声明指针的同一语句中初始化它。这就是我接下来用以下行所做的，它将 0 分配给 pScore。

```
int* pScore = 0; //declare and initialize a pointer
```

将 0 分配给指针具有特殊含义。松散地翻译，它的意思是：“指向 nothing。” 程序员称值为零的指针为空指针。你应该在声明指针时始终为其初始化一些值，即使该值为零。

### 提示

许多程序员将 NULL 分配给指针而不是 0，以使指针成为空指针。NULL 是一个在多个库文件中定义的常量，包括 iostream。

## 为指针分配地址

由于指针存储对象的地址，你需要一种方法将地址放入指针中。一种方法是获取现有变量的内存地址并将其分配给指针。这就是我在以下行中所做的，它获取变量 score 的地址并将其分配给 pScore。

```
pScore = &score; //assign pointer address of variable score
```

我通过在变量名前面加上 &、取地址运算符来获取 score 的地址。（是的，你以前见过 & 符号，当它用作引用运算符时。然而，在这种上下文中，& 符号获取对象的地址。）

作为前一行代码的结果，pScore 包含 score 的地址。就好像 pScore 精确知道 score 在计算机内存中的位置。这意味着你可以使用 pScore 访问 score 并操作存储在 score 中的值。图 7.2 作为 pScore 和 score 之间关系的视觉说明。

![](img/34f09be0ed6217c465debc4490197d4f_250_0.png)

图 7.2
指针 pScore 指向 score，score 存储值 1000。

为了证明 pScore 包含 score 的地址，我使用以下行显示变量的地址和指针的值。

```
cout << "&score is: " << &score << "\n";    //address of score variable
cout << "pScore is: " << pScore << "\n";    //address stored in pointer
```

pScore 包含 0x22ff5c，这是 score 的地址。（Pointing 程序在你的系统上显示的具体地址可能不同。重要的是 pScore 和 &score 的值是相同的。）

## 解引用指针

就像你解引用迭代器以访问它所引用的对象一样，你解引用指针以访问它所指向的对象。你以同样的方式完成解引用——使用 *，解引用运算符。我将解引用运算符用于以下行，该行显示 1000，因为 *pScore 访问存储在 score 中的值。

```
cout << "*pScore is: " << *pScore << "\n\n"; //value pointed to by pointer
```

记住，*pScore 的意思是，“pScore 所指向的对象。”

### 陷阱

> 不要解引用空指针，因为它可能导致灾难性的结果。

接下来，我用以下行将 500 加到 score。

```
score += 500;
```

当我将 score 发送到 cout 时，会显示 1500，就像你期望的那样。当我将 *pScore 发送到 cout 时，score 的内容再次被发送到 cout，并且再次显示 1500。

接下来，我用以下行将 500 加到 pScore 所指向的值。

```
*pScore += 500;
```

由于 pScore 指向 score，前一行代码将 500 加到 score。因此，当我接下来将 score 发送到 cout 时，会显示 2000。然后，当我将 *pScore 发送到 cout...你猜对了，会再次显示 2000。

### 陷阱

当你想更改指针所指向对象的数值时，不要更改指针的值。例如，如果我想将 pScore 所指向的 int 加 500，那么以下行将是一个大错误。

```
pScore += 500;
```

前面的代码将 500 加到存储在 pScore 中的地址，而不是加到 pScore 原本指向的值。因此，pScore 现在指向可能包含任何内容的某个地址。像这样解引用指针可能导致灾难性的结果。

## 重新分配指针

与引用不同，指针可以在程序生命周期的不同时间指向不同的对象。重新分配指针的工作方式与重新分配任何其他变量一样。接下来，我用以下行重新分配 pScore。

```
pScore = &newScore;
```

作为结果，pScore 现在指向 newScore。为了证明这一点，我通过将 &newScore 发送到 cout 来显示 newScore 的地址，然后是存储在 pScore 中的地址。两个语句都显示相同的地址。然后我将 newScore 和 *pScore 发送到 cout。两者都显示 5000，因为它们都访问存储此值的同一块内存。

### 陷阱

当你想更改指针本身时，不要更改指针所指向的值。例如，如果我想更改 pScore 以指向 newScore，那么以下行将是一个大错误。

```
*pScore = newScore;
```

此代码只是更改 pScore 当前指向的值；它不会更改 pScore 本身。如果 newScore 等于 5000，则前面的代码等同于 *pScore = 5000; 而 pScore 仍然指向分配前相同的变量。

