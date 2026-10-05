

注意：使用作用域解析操作符可以在作用域函数处设置断点，例如：

```
gdb> b account : :balance
```

我们可以通过以下命令删除所有断点：

```
gdb> delete
or
gdb> d
```

可以使用以下命令删除特定的断点：

- gdb> clear [line number]
- gdb> clear [function_name]

我们可以通过以下命令获取所有断点的信息：

```
gdb> info
```

注意：GDB 调试器可以用于调试线程。

# 在多次调试会话之间保存断点

如果你正正在进行一个复杂的调试会话，你很可能在多个源文件中设置了多个断点。此外，定位错误可能需要超过一个调试会话。在这种情况下，每次启动新会话时都要重新设置断点，这既令人沮丧又耗时。GDB 提供了一种避免此问题的方法。

首先，按照常规方式设置断点。然后将断点保存到文件中：

```
gdb> save breakpoints breakpoints.txt
```

现在，当你启动一个新的调试会话时，加载保存的断点：

```
gdb> source breakpoints.txt
```

# 单步执行程序

当我们停在断点处时，可以逐行步执行程序。

`next` 和 `step` 命令都告诉 gdb 执行程序的下一行，然后再次暂停。如果该行是一个函数调用，那么 `next` 和 `step` 将产生不同的结果。如果我们使用 `step`，程序将在函数的第一行暂停；如果我们使用 `next`，程序将在函数调用之后的一行暂停。

```
gdb> next      // gdb n
or:
gdb> s       // gdb s
```

# 跳出函数

如果我们已经使用 `step` 进入了某个函数，可以使用 `gdb> finish`（或 `gdb fin`）跳出该函数。

# 列出程序语句

当我们停在断点处时，可以列出我们停止位置的程序行以及周围的几行：

```
gdb> l
```

我们可以通过以下命令查看不同源文件中的程序行：

```
gdb> l filename:line_number
```

我们可以通过以下命令列出函数的几行：

```
gdb> l function_name
```

# 继续调试会话

在我们检查完断点处的代码后，可以使用以下命令继续调试会话：

```
gdb> continue          (or gdb> c)
or
gdb> continue repeat count
```

如果只是单独按回车键，gdb 将重复上一个命令。

# 重启调试会话

我们可以通过以下命令重启整个调试会话：

```
gdb > restart
```

# 检查和设置变量

当我们停在断点处时，可以使用以下命令检查如 `foo` 的变量：

```
gdb> print foo
or
gdb> p foo
```

我们可以显示当前执行函数的所有参数值：

```
gdb> info args
```

可以通过以下命令显示所有局部变量的当前值：

```
gdb> info locals
```

我们可以如下所示设置变量的值：

```
gdb> set var foo = 5
or:
gdb> p foo = 5
```

# 观察变量

在调试会话开始之前或停在断点处时，我们可以如下所示对变量设置观察点：

```
gdb> watch balance
gdb> run or continue
```

调试器将在 `balance` 的值变化的地方停止。

# 退出调试会话

```
gdb> quit
or:
gdb> control-d (control-d 是文件结束符)
```

# .gdbinit 文件

每当启动 GDB 调试器时，它都会搜索 `.gdbinit` 文件，首先在用户的家目录中，然后在当前工作目录中。如果找到了该文件，将执行文件中列出的命令。文件中每行放置一个命令。

例如，如果我们希望调试器始终停在 `main()` 处，可以在 `.gdbinit` 中插入以下 GDB 命令：

```
gdb> b main.cpp
```

# 跟踪程序执行

假设我们在程序执行过程中遇到了导致程序崩溃的严重错误。我们可以通过 `backtrace` 命令定位发生该错误的程序语句。在调试器提示符下，输入：

```
gdb> bt
```

`bt` 会跟踪导致严重错误的函数调用。

# 调试核心转储 (Core Dump)

严重错误（如段错误）会终止程序执行并导致调试器输出核心转储。核心转储文件包含了创建程序中止点状态所需的所有信息。我们可以通过将核心转储文件作为第二个参数传递给 gdb 来访问核心转储中的信息：

```
gdb> hello core.file
```

# 调试段错误

考虑以下程序：

```cpp
// foo.cpp

#include <iostream>
using namespace std;

int main()
{
    int x = 7;
    int *p = 0;
    cout << "x = " << x;
    cout << "The pointer points to the value " << *p;
}
```

（注：第 553-557 页的 OCR 文本包含大量的损坏/乱码字符，已根据提供的 GDB 和 C++ 编程上下文进行了清理。）

