

```cpp
)} while (choice != 'Q');
return 0;
}
void printMessage(void)
{
    static int times = 0;
    times++;
    cout << "This function called " << times << " times\n";
}
```

这里有一些输入和输出示例：

- 输入 Q 退出，输入其他字符继续：X
- This function called 1 times
- 输入 Q 退出，输入其他字符继续：Y
- This function called 2 times
- 输入 Q 退出，输入其他字符继续：Z
- This function called 3 times
- 输入 Q 退出，输入其他字符继续：Q
- 输入停止

此输出也是正确的。现在我们来分析一下程序是如何运行的。

当第一次调用 `printMessage` 函数时，通过语句声明变量 `times` 并初始化为零：
`static int times = 0;`

随后变量 `times` 增加了 1 并输出，结果输出为：
`This function called 1 times`

到目前为止，这与 `times` 作为自动局部变量而非静态局部变量是一样的。区别在于，当 `printMessage` 函数结束时，`times` 作为静态局部变量，**不会**被销毁。它的值保留在内存中。
下一次（第二次）调用 `printMessage` 函数时，声明并初始化 `times` 的语句不会执行，因为它是静态的，它从第一次调用 `printMessage` 函数开始就一直存在。此外，在 `printMessage` 函数第一次调用结束时 `times` 的值保留在内存中。该值被增加到 2 并输出，因此第二次调用 `printMessage` 函数的输出为：
`This function called 2 times`

因此，通过将变量 `times` 设为全局变量或静态局部变量，我们能够在函数调用之间持久该值。区别在于，作为静态局部变量，`times` 的作用范围仍然局限于 `printMessage` 函数，而不是像全局变量那样在整个程序中都有作用域。如果代码中某处 `times` 变量的值不正确，这种作用范围将使你更容易修复程序。

# 向函数发送信息

Hello World 程序中的 `printMessage` 函数输出 "Hello world!"，不需要任何额外信息即可完成工作。

让我们让 `printMessage` 函数变得更有用，这样它不再总是输出 "Hello world"，而是输出我们要求它输出任何内容。当然，`printMessage` 函数并不是读心术；我们需要告诉它我们想要输出的消息。

让我们尝试编写一个程序，让用户在 `main` 中输入要输出的内容，将用户输入存储在变量 `str` 中，并让 `printMessage` 函数尝试输出 `str` 的值。一种方法是将变量设为全局，这样在 `main` 和 `printMessage` 函数中都可以访问它：

```cpp
#include <iostream>
#include <string>
using namespace std;
void printMessage();
string str;

int main ()
{
    cout << "Enter a string: ";
    cin >> str;
    printMessage();
    return 0;
}
void printMessage ()
{
    cout << "You inputted " << str;
}
```

- 注意使用字符串时，`cin` 语句包含 `<string>` 标准库。此外，`cin` 对象和流插入运算符（`>>`）只接受到第一个嵌入空格之前的字符串变量输入。如果用户输入 "Jeff Kent,"，输出将只有 "Jeff"。在第 10 章中，我们将介绍 `getline` 函数，它可以处理带有嵌入空格的字符串。

这里是一些示例输入和输出：

Enter a string: Jeff
You inputted Jeff

尽管如此，正如上一节讨论的，全局变量可能会让修复程序问题变得更加困难。这里有一个更好的替代方案，涉及传递参数。

正如本章前面讨论的，函数头中函数名后的括号内包含了函数的参数。参数是提供给函数的信息，以便其执行相应的任务。

正如前面讨论的，某些函数如 Hello World 程序中的 `printMessage` 函数，它简单地输出 "Hello world"，它不需要任何额外信息即可完成工作。

然而，当我们修改 `printMessage` 函数，使其不再总是输出 "Hello world!" 而是输出我们要求输出的任何消息时，我们需要告诉它我们想要输出的消息。我们可以通过向函数传递指定消息的参数来实现。

本章将讨论传递参数的两种方法：按值传递和按引用传递。第三种方法按地址传递参数将在我们在第 11 章讨论指针后介绍。

# 按值传递参数

以下是使用 `printMessage` 函数输出消息的程序修改。这次，将消息的内容作为参数传递给 `printMessage`：

```cpp
#include <iostream>
#include <string>
using namespace std;
void printMessage(string);

int main () {
    string str;
    cout << "Enter a string: ";
    cin >> str;
    printMessage(str);
    return 0;
}
void printMessage(string s) {
    cout << "You inputted " << s;
}
```

这里是一些示例输入和输出：
nEnter a string: Jeff
You inputted Jeff

# 函数原型和函数头

函数原型和函数头都包含一个参数，数据类型为 `string`。然而，函数原型的参数只有参数的数据类型（`string`），而函数头同时包含数据类型和参数名称（`string`）。

函数原型也可以包含参数名称以及数据类型，例如：
`void printMessage(string someArg);`

然而，该参数被称为哑参数，因为它没有作用。

相比之下，函数头的参数必须包含参数名称和数据类型。函数头参数中该参数名称的目的将在将在文中解释。

# 使用函数参数

以下代码调用了 `printMessage` 函数：

```cpp
printMessage(str);
```

字符串变量 `str` 的值之前由用户输入赋值，现在作为参数传递给 `printMessage` 函数。`str` 的值随后传递给字符串变量 `s`，`s` 是 `printMessage` 函数头中的参数名称：

```cpp
void printMessage (string s)
```

随后，字符串变量 `s` 在 `printMessage` 函数体中使用用于输出消息：

```cpp
cout << "You inputted " << s;
```

**图 9-2** 显示了函数调用参数的值如何传递给函数头中的参数，然后在被调用的函数体中使用。

```cpp
int main()
{
    printMessage(str);
    return 0;
}

void printMessage (string s)
{
    cout<<"You inputted"<<s;
}
```

![](img/59a3417a6d5906fae6d8000d4c2cff76_170_0.png)

函数头必须包含参数名称和数据类型，这样函数调用参数的值才能传递给函数头中的参数，并在被调用的函数体中使用。

函数头必须包含参数名称和数据类型，这样 `main` 中的 `str` 变量的值才能传递给 `printMessage` 函数的参数。`str` 的值随后传递到 `printMessage` 函数头中的参数名 `s`：

```cpp
printMessage(str);
void printMessage (string s)
```

即使如此，`main` 中的 `str` 与 `printMessage` 函数中的参数是不同的变量。尽管，我建议在 `main` 中使用不同的名称以避免混淆。

# 使用多个参数

我们讨论的程序使用了一个参数。然而，一个函数可以有两个或多个参数。
以下 `printMessage` 函数的修改版本使用了两个参数，一个用于名字，一个用于姓：

```cpp
#include <iostream>
#include <string>
using namespace std;
void printMessage(string, string);
```

```cpp
int main() {
  string namel, name2;
  cout << "Enter first name: ";
  cin >> namel;
  cout << "Enter last name: ";
  cin >> name2;
  printMessage(namel, name2);
  return 0;
}

 printMessage(string firstName, string lastName) {
  cout << "Your name is " << firstName << " " << lastName << endl;
}
```

这里的示例输入和输出：

Enter first name: Jeff
Enter last name: Kent
Your name is Jeff Kent

函数调用中的参数顺序必须与函数头中的参数顺序对应。这里的函数调用和函数头是：

```cpp
printMessage(first, last);
vprintMessage(string firstName, string lastName)
```

函数调用中的变量是 `name1`。`main` 中 `first` 的值被复制到 `printMessage` 函数头的第一个变量 `firstName`。同样，函数调用中的第二个变量是 `name2`，`main` 中 `name2` 的值被复制到 `printMessage` 函数头的第二个变量 `lastName`。

如果函数调用中的参数反反，例如：

```cpp
printMessage(last, first);
```

那么示例输入和输出将变为

Enter first name: Jeff
Enter last name: Kent
Your name is Kent Jeff

在这个例子中，仔细注意函数调用参数顺序与函数头参数之间的对应关系导致了我的名字输出倒置。当多个函数参数具有不同数据类型时，函数调用参数顺序与函数头参数顺序之间不对应的后果将更加严重。

在以下程序中，第一个参数（人的名字）是 `string`，而第二个参数（人的年龄）是不同的类型，整数。

```cpp
#include <iostream>
#include <string>
using namespace std;
void printMessage(string firstName, int);
```

