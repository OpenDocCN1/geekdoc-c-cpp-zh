
- 名称：每个函数都必须有一个名称。通常情况下，适用于变量名的规则也适用于函数名。

- 参数列表：调用函数的程序模块可以向其发送数据。参数列表是存储传递给函数的变量列表。它被包含在括号中。如果没有向函数传递任何值，则其参数列表为空。

- 函数体：函数体是执行该函数正在执行的任务的语句集合。这些语句被包含在大括号中。

- 返回类型：函数可以将一个值传回调用它的程序模块。返回类型是所传值的数据类型。

图 6-2 显示了带有各个部分的简单函数的定义。

图 6-2

![](img/1c095ef63c71a34f9802f104f947be57_359_0.png)

定义中的第一行被称为函数头。让我们仔细观察它的三个部分。首先是它的返回类型。然后是它的名称。头部以一组括号结束。如果函数有任何参数，它们将列在这些括号内部。然而，即使参数列表为空，也必须包含括号，如图 6-2 所示。

### Void 函数

你已经知道函数可以返回一个值。你在本书中所看到的所有程序中，`main` 函数都声明为向操作系统返回一个 `int` 类型的值。`return 0;` 语句会导致 `main` 函数执行完毕时返回值 0。

并不是所有函数都需要返回值，某些函数只需执行一个或多个语句并返回。在 C++ 中，这些被称为 void 函数。这里显示的 `displayMessage` 函数就是一个示例：

```cpp
void displayMessage() { cout << "Hello from the function displayMessage\n"; }
```

函数的名为 `displayMessage`。这个名称具有描述性，函数应当如此。它指示了函数的功能：它显示一条消息。因为函数执行工作不需要接收任何信息，所以括号内没有列出参数。返回类型是 `void`。这意味着函数在执行完毕并返回到调用它的程序部分时，不会发送回值。由于没有发送回值，因此不需要返回语句。当函数中的语句执行完毕并遇到右括号结束函数时，程序会自动返回。

### 调用函数

函数在被调用时执行。`main` 函数在程序启动时被自动调用，但其他函数必须通过函数调用语句来执行。当函数被调用时，程序会跳转到该函数并执行其体中的语句。让我们程序 6-1，它包含了两个函数：`main` 和 `displayMessage`。

### 程序 6-1

```cpp
// 此程序有两个函数：main 和 displayMessage。
#include <iostream>
using namespace std;

// 函数原型声明
void displayMessage();

**********************
* main
**********************
int main() {
    cout << "Hello from main.\n";
    displayMessage(); // Call displayMessage
    cout << "Now we are back in main again.\n";
    return 0;
}

**********************
* displayMessage
**********************
void displayMessage() {
    cout << "Hello from displayMessage.\n";
}
```

### 程序输出

Hello from main.

Hello from displayMessage.

Now we are back in main again.

### 程序 6-2

```cpp
// 此程序在循环内部调用 displayMessage。
#include <iostream>
using namespace std;

// 函数原型声明
void displayMessage();

**********************
* main
**********************
int main() {
    cout << "Hello from main.\n";
    for(int count = 0; count < 3; count++) {
        displayMessage(); // Call displayMessage
    }
    cout << "\nNow we are back in main again.\n";
    return 0;
}

**********************
* displayMessage
**********************
void displayMessage() {
    cout << "Hello from displayMessage.\n";
}
```

### 程序输出

Hello from main.

Hello from displayMessage function.

Hello from displayMessage function.

Hello from displayMessage function.

Now we are back in main again.

### 程序 6-3

```cpp
// 此程序有三个函数：main,first 和 second。
#include <iostream>
using namespace std;

// 函数原型声明
void first();
void second();

**********************
* main
**********************
int main() {
    cout << "I am starting in function main.\n";
    first();    // Call function first
    second();  // Call function second
    cout << "Now I am back in function main again.\n";
    return 0;
}

**********************
* first
**********************
void first() {
    cout << "I am now inside the function first.\n";
}
```

# 程序 6-3 (续)

```
29
30 /**************************
31 * second
32 * 此函数显示一条消息。
33 **************************/
34 void second()
35 {
36     cout << "I am now inside the function second.\n";
37 }
```

### 程序输出

I starting in function main.

I am inside the function first.

I am now inside the function second.

Now I am back in function main again.

在程序 6-3 的第 15 行和第 16 行，函数 `main` 包含了对 `first` 和 `second` 的调用：

```
first();
second();
```

每个调用语句都会导致程序跳转到一个函数，并在函数完成后返回 `main`。图 6-4 展示了程序所经过的路径。

# 图 6-4

![](img/1c095ef63c71a34f9802f104f947be57_363_0.png)

# 第 6 章 函数

函数也可以以分级或分层的方式被调用。程序 6-4 证明了这一点，它有三个函数：`main`、`deep` 和 `deeper`。

# 程序 6-4

```
1 // 此程序有三个函数：main, deep 和 deeper。
2 #include <iostream>
3 using namespace std;
4
5 // 函数原型
6 void deep()
7 void deeper();
8
9 /* **************************
10                main                *
11 **********************************/
12 int main()
13 {
14     cout << "I am starting in function main.\n";
15     deep();      // 调用函数 deep
16     cout << "Now I am back in function main again.\n";
17     return 0;
18 }
19
20 /* **************************
21                deep                *
22     * 此函数显示一条消息。
23 **********************************/
24 void deep()
25 {
26     cout << "I am now inside the function deep.\n";
27     deeper();      // 调用函数 deeper
28     cout << "Now I am back in deep.\n";
29 }
30
31 /* **************************
32                deeper                *
33     * 此函数显示一条消息。
34 **********************************/
35 void deeper()
36 {
37     cout << "I am now inside the function deeper.\n";
38 }
```

程序输出

Iam starting in function main.

Iam now inside the function deep.

Iam now inside the function deeper.

Now I am back in deep.

Now I am back in function main again.

在程序 6-4 中，函数 `main` 只调用函数 `deep`。反地，`deep` 调用了 `deeper`。该程序所经过的路径如图 6-5 所示。

# 6-5

```
int main() {
    cout << "I am starting in function main.\n";
    deep();
    cout << "Now I am back in function main again.\n";
    return 0;
}

void deep() {
    cout << "I am now inside the function deep.\n";
    deeper();
    cout << "Now I am back in deep.\n";
}

void deeper() {
    cout << "I am now inside the function deeper.\n";
}
```

## 检查点

使用以下信息回答问题 6.1–6.6。每个函数内部的行号已包含供参考。

一个程序包含以下函数：

+ 1 `void printHeading()`

2 {

3     `cout` << "The History of Computers \n";

4 }

程序的 `main` 函数包含以下代码段：

+ 12 `for` (`int count` = 0; `count` < 3; `count++`)
13     `printHeading();`
14     `cout` << "I called printHeading \n";
15 }

+ 6.1 第 1 行包含的是函数头还是函数调用？

+ 6.2 第 13 行包含的是函数头还是函数调用？

+ 6.3 `printHeading` 函数被调用了多少次？

+ 6.4 哪一行号的代码会导致程序离开 `printHeading` 函数并返回 `main`？

+ 6.5 当程序返回 `main` 时，执行的是哪一行的代码？

+ 6.6 当执行 `main` 的第 12–15 行时，将显示什么？

# 函数原型

> **概念：** 函数原型消除了在对函数的所有调用之前放置函数定义的需要。

在编译器遇到对某个特定函数的调用之前，它必须已经知道该函数使用的参数数量、每个参数的数据类型以及函数的返回类型。这通常通过在程序中为 `main` 以外的每个函数包含函数原型来实现。`main` 不需要原型，因为它是程序的起点。

到目前为止你在本章中看到的函数没有从调用它的函数处接收任何信息，因此它们没有参数。除了 `main` 之外，它们没有返回任何信息，因此它们的返回类型是 `void`。让我们仔细查看一下 6-1 中 `displayMessage` 函数的原型：

```
void displayMessage();
```

这个原型看起来与函数头相似，只是末尾有一个分号。该语句告诉编译器 `displayMessage` 函数不使用参数且返回类型为 `void`，意味着它不返回任何值。

注意，程序 6-1 中 `displayMessage` 函数的原型被放在 `main` 函数上方。如果没有它的原型为编译器提供所需信息，整个 `displayMessage` 函数定义必须放在 `main` 函数之前才能被调用。程序 6-5 修改了程序 6-1，以展示如果没有函数原型，它需要如何重新组织。

# 程序 6-5

```
1 // 此程序有两个函数：main 和 displayMessage。
2 // displayMessage 没有原型，因此它必须
3 // 放在 main 函数之前才能被调用。
4 #include <iostream>
5 using namespace std;
6 
7 /******************************************
8 *                               displayMessage *
9 * *
10 * 此函数显示一条问候语。 *
11 ******************************************/
12 void displayMessage()
13 {
14     cout << "Hello from the displayMessage function.\n";
15 }
16
17 /******************************************
18 *                  main                        *
19 ******************************************/
```

（程序继续）

# 程序 6-5 (续)

```
int main()
{
    cout << "Hello from main.\n";
    displayMessage(); // 调用 displayMessage
    cout << "Now we are back in the function again.\n";
    return 0;
}
```

# 程序输出与程序 6-1 的输出。

程序员倾向于使用这种组织方式并将 `main` 函数放在最后。然而，大多数程序员发现为 `main` 之外的每个函数使用原型并将 `main` 放在第一个更容易。这当程序有许多调用其他函数时特别有用。考虑程序 6-4，其 `main`、`deep` 和 `deeper` 三个函数如果没有原型，顺序应该是：

- `deeper` 应该放在第一个，以便 `deep` 调用它。

- `deep` 应该放在第二个，以便 `main` 调用它。

- `main` 函数必须放在最后。

使用原型时，实际的函数定义可以按任何顺序放置。只需将原型放在程序顶部，紧跟 `std` 语句之后，正如我们在程序 6-1 到 6-4 中做的那样。这确保了它们位于 `main` 或任何其他函数之前。

> 警告！必须在所有调用之前放置函数定义或函数原型。否则程序无法编译。

# 向函数传递数据

概念：当函数被调用时，程序可以向函数传递值。

传递到函数的值被称为参数。你已经熟悉如何在函数调用中使用参数。在以下语句中，`pow` 被调用并传递了两个参数 `2.0` 和 `3.0`：

```
result = pow(2.0, 3.0);
```

`pow` 函数使用这些信息来计算第一个参数的相对于第二个参数的幂。在这种情况下，它将计算 `2.0` 的三次幂，并将值 `8.0` 返回给 `result`。

参数是特殊的变量，用于持有作为参数传入函数的值。通过使用参数，你可以设计接受这种方式的自己的函数。

## 第6章 函数

这里是一个带参数的函数定义。参数为 `num`。

```cpp
void displayValue(int num)
{
  cout << "The value is " << num << endl;
}
```

注意，参数变量定义在括号内 (`int num`)。因为它被声明为整数，因此函数 `displayValue` 可以接受一个整数值作为参数。程序 6-6 是使用该函数的完整程序。

## 程序 6-6
