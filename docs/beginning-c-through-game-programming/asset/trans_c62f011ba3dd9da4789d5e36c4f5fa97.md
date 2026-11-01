
```
func();

cout << "Back in main() var is: " << var << "\n\n";

{
    cout << "In main() in a new scope var is: " << var << "\n\n";
    
    cout << "Creating new var in new scope.\n";
    int var = 10;  // variable in new scope, hides other variable named var
    cout << "In main() in a new scope var is: " << var << "\n\n";
}

cout << "At end of main() var created in new scope no longer exists.\n";
cout << "At end of main() var is: " << var << "\n";

    return 0;
}

void func()
{
    int var = -5;  // local variable in func()
    cout << "In func() var is: " << var << "\n\n";
}
```

## 使用独立作用域

每次使用大括号创建代码块时，你就创建了一个作用域。函数就是一个例子。在一个作用域中声明的变量在该作用域之外不可见。这意味着在函数中声明的变量在该函数之外不可见。

在函数内部声明的变量被视为局部变量——它们是局部的，仅属于该函数。这就是函数封装的原因。

你已经见过许多局部变量的实际应用。我在 main() 中再定义一个局部变量：

```
int var = 5;  // local variable in main()
```

这行代码声明并初始化了一个名为 var 的局部变量。我在下一行代码中将该变量发送到 cout：

```
cout << "In main() var is: " << var << "\n\n";
```

这正如你所预期的那样——显示出 5。

接下来我调用 func()。一旦进入该函数，我就进入了一个独立于 main() 定义的作用域之外的作用域。因此，我无法访问我在 main() 中定义的变量 var。这意味着当我用下面这行代码在 func() 中再次定义一个名为 var 的变量时，这个新变量与 main() 中的名为 var 的变量完全分开。

```
int var = -5; // local variable in func()
```

两者互不影响，这就是作用域的美妙之处。当你编写函数时，就不必担心另一个函数是否使用了相同的变量名。

然后，当我用下面这行代码在 func() 中显示 var 的值时，计算机显示 −5。

```
cout << "In func() var is: " << var << "\n\n";
```

这是因为在当前作用域中，计算机所能看到的只有一个名为 var 的变量——就是我在该函数中声明的局部变量。

一旦作用域结束，该作用域中声明的所有变量都将不复存在。它们被称为超出作用域。所以接下来，当 func() 结束时，其作用域也结束。这意味着 func() 中声明的所有变量都被销毁。因此，我在 func() 中声明的值为 −5 的 var 被销毁。

func() 结束后，控制权返回到 main()，并从中断的地方继续执行。接下来，执行下面这行代码，将 var 发送到 cout。

```
cout << "Back in main() var is: " << var << "\n\n";
```

main() 局部的 var 的值（5）再次被显示。

你可能会想我在 func() 中时，main() 中创建的 var 发生了什么。嗯，该变量并未被销毁，因为 main() 尚未结束。（程序控制只是短暂地绕道去了 func()。）当程序暂时从一个函数退出进入另一个函数时，计算机会保存它在第一个函数中的位置，安全地保存其所有局部变量的值，并在控制权返回到第一个函数时恢复这些值。

### Hint

参数在函数中就像局部变量一样起作用。

## 使用嵌套作用域

你可以在现有作用域中使用一对大括号创建一个嵌套作用域。这就是我在 main() 中接下来做的：

```
{
    cout << "In main() in a new scope var is: " << var << "\n\n";
    
    cout << "Creating new var in new scope.\n";
    int var = 10; // variable in new scope, hides other variable named var
    cout << "In main() in a new scope var is: " << var << "\n\n";
}
```

这个新作用域是 main() 中的一个嵌套作用域。我在这个嵌套作用域中做的第一件事是显示 var。如果一个变量未在作用域中声明，计算机将逐级向上查找嵌套作用域以找到你请求的变量。在这种情况下，因为 var 未在此嵌套作用域中声明，计算机向上查找一级到定义 main() 的作用域并找到 var。因此，程序显示该变量的值——5。

然而，我在这个嵌套作用域中接下来做的事是声明一个名为 var 的新变量并将其初始化为 10。现在当我将 var 发送到 cout 时，显示的是 10。这次计算机不必向上查找任何嵌套作用域级别来查找 var；该作用域中有一个局部的 var。并且不用担心，我最初在 main() 中声明的 var 仍然存在；它只是被这个嵌套作用域中的新 var 隐藏了。

### Trap

> 虽然你可以在一系列嵌套作用域中声明同名变量，但这并不是一个好主意，因为它可能导致混淆。

接下来，当嵌套作用域结束时，等于 10 的 var 超出作用域并不再存在。然而，我创建的第一个 var 仍然存在，所以当我用下面这行代码在 main() 中最后一次显示 var 时，程序显示 5。

```
cout << "At end of main() var is: " << var << "\n";
```

### Hint

当你在 for 循环、while 循环、if 语句和 switch 语句内部定义变量时，这些变量在其结构之外不存在。它们的行为就像在嵌套作用域中声明的变量。例如，在下面的代码中，变量 i 在循环之外不存在。

```
for(int i = 0; i < 10; ++i)
{
    cout << i;
}
// i doesn't exist outside the loop
```

但请注意——一些旧编译器并未正确实现标准 C++ 的这一功能。我建议你使用带有现代编译器的 IDE，例如 Microsoft Visual C++ 2010 Express Edition。有关如何使用此 IDE 创建第一个项目的逐步说明，请参阅附录 A。

## 使用全局变量

通过封装的魔力，你所见过的函数都完全封闭且彼此独立。将信息传入它们的唯一方式是通过参数，从它们中获取信息的唯一方式是通过返回值。嗯，这并不完全正确。还有另一种在程序各部分之间共享信息的方式——通过全局变量（可在程序任何部分访问的变量）。

## 介绍 Global Reach 程序

Global Reach 程序演示了全局变量。该程序展示了如何从程序的任何地方访问全局变量。它还展示了如何在作用域中隐藏全局变量。最后，它展示了你可以从程序的任何地方更改全局变量。图 5.4 显示了该程序的结果。

你可以从 Course Technology 网站 (www.courseptr.com/downloads) 下载此程序的代码。该程序位于第 5 章文件夹中；文件名是 global_reach.cpp。

```
// Global Reach
// Demonstrates global variables

#include <iostream>
```

![](img/c7e8651578bccd573227f684823b8754_189_0.png)

### Figure 5.4

你可以从程序的任何地方访问和更改全局变量——但它们也可以在作用域中被隐藏。

```
using namespace std;

int glob = 10;  // global variable

void access_global();
void hide_global();
void change_global();

int main()
{
    cout << "In main() glob is: " << glob << "\n\n";
    access_global();

    hide_global();
    cout << "In main() glob is: " << glob << "\n\n";

    change_global();
    cout << "In main() glob is: " << glob << "\n\n";

    return 0;
}
```

```
void access_global()
{
    cout << "In access_global() glob is: " << glob << "\n\n";
}
```

```
void hide_global()
{
    int glob =0;  // hide global variable glob
    cout << "In hide_global() glob is:" << glob << "\n\n";
}
```

```
void change_global()
{
    glob = -10;  // change global variable glob
    cout << "In change_global() glob is:" << glob << "\n\n";
}
```

## 声明全局变量

你在程序文件中的任何函数之外声明全局变量。这就是我在下面这行代码中所做的，它创建了一个名为 glob 并初始化为 10 的全局变量。

```
int glob =10;  // global variable
```

## 访问全局变量

你可以从程序的任何地方访问全局变量。为了证明这一点，我在 main() 中用以下代码显示 glob：

```
cout << "In main() glob is: " << glob << "\n\n";
```

程序显示 10，因为作为全局变量，glob 可用于程序的任何部分。为了再次证明这一点，我接下来调用 access_global()，计算机在该函数中执行以下代码：

```
cout << "In access_global() glob is: " << glob << "\n\n";
```

再次显示 10。这是有道理的，因为我在每个函数中显示的是完全相同的变量。
