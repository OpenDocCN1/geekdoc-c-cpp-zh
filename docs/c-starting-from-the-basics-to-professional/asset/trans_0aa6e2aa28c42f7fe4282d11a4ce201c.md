

```cpp
std::cout << "\nNow try successive exclusive OR operations:\n";
unsigned int mask{ red ^ white };
std::cout << std::format("mask = red ^ white = {:08X}\n", mask);
std::cout << std::format("        mask ^ red = {:08X}\n", mask ^ red);
std::cout << std::format("        mask ^ white = {:08X}\n", mask ^ white);

unsigned flags{ 0xFF };          // Flags
unsigned int bit1mask{ 0x1 };    // Selects bit 1
unsigned int bit6mask{ 0b100000 }; // Selects bit 6
unsigned int bit20mask{ 1u << 19 }; // Selects bit 20

std::cout << "Use masks to select or set a particular flag bit:\n";
std::cout << std::format("Select bit 1 from flags : {:08X}\n", flags & bit1mask);
std::cout << std::format("Select bit 6 from flags : {:08X}\n", flags & bit6mask);
std::cout << std::format("Switch off bit 6 in flags: {:08X}\n", flags &= ~bit6mask);
std::cout << std::format("Switch on bit 20 in flags: {:08X}\n", flags |= bit20mask);
}
```

如果你正确输入了代码，输出如下：

```
Try out bitwise complement, AND and OR operators:
Initial value:        red = 00FF0000
Complement:            ~red = FF00FFFF
Initial value:       white = 00FFFFFF
Complement:          ~white = FF000000
Bitwise AND: red & white = 00F00000
Bitwise OR: red | white = 00FFFFFF

Now try successive exclusive OR operations:
       mask = red ^ white = 000FFFFF
             mask ^ red = 00FFFFFF
           mask ^ white = 00F00000
Use masks to select or set a particular flag bit:
Select bit 1 from flags : 00000001
Select bit 6 from flags : 00000020
Switch off bit 6 in flags: 000000DF
Switch on bit 20 in flags: 000800DF
```

对于 `<format>` 模块有一个重要的声明，因为代码使用 `std::format()` 来方便地将所有值显示为十六进制形式。为了更容易比较输出值，我们还在整个程序中使用 `{:08X}` 替换字段，使它们具有相同的位数和前导零。`0` 前缀将填充字符设置为 `'0'`，`8` 设置字段宽度，`X` 后缀使整数使用大写字母的十六进制表示法格式化。如果你使用 `x` 而不是 `X`，整数将使用小写十六进制数字格式化。

要查看 `{:08X}` 替换字段中 `0` 和 `X` 组成部分的效果，例如，你可以按如下方式替换 `"Initial value"` 输出语句中的替换字段：

```cpp
std::cout << std::format("Initial value:    red = {:8x}\n", red);  // {:08X} --> {:8x}
```

格式化后的 red 字符串将使用小写字母，并且不再以前导零序列开头（默认填充字符是空格）：

```
Initial value:        red =    ff0000
Complement:           ~red = FF00FFFF
...
```

关于字符串格式化的讨论已经够多了——让我们回到当前的主题：位运算符。在 Ex3_01 中，你首先将常量 red 和 white 定义为无符号整数，并用十六进制颜色值初始化它们。在一些初始输出语句之后，你用下面两条语句将 red 和 white 按位与和按位或运算组合起来：

```cpp
std::cout << std::format("Bitwise AND: red & white = {:08X}\n", red & white);
std::cout << std::format("Bitwise OR: red | white = {:08X}\n", red | white);
```

如果你检查输出，你会发现结果与讨论的完全一致。两个位进行 AND 运算时，如果两个位都是 1，结果为 1；否则，结果为 0。当你对两个位进行按位 OR 运算时，除非两个位都是 0，否则结果为 1。

接下来，你创建了一个掩码，通过将两个值与 XOR 运算符组合来在 red 和 white 之间切换。mask 的值表明，当两个位不同时，两个位的异或结果为 1；当它们相同时，结果为 0。通过使用异或运算将 mask 与任一颜色值组合，你可以得到另一个颜色值。这意味着通过反复使用精心选择的掩码进行异或运算，你可以在两种不同颜色之间切换。应用一次掩码得到一种颜色，再应用一次则恢复为原始颜色。在计算机图形学中，使用所谓的 XOR 模式进行绘制或渲染时，经常会利用这一特性。

最后一组语句演示了如何使用掩码从一组标志位中选择单个位。选择特定位的掩码必须将该位设为 1，其他所有位设为 0。要从 flags 中选择一个位，你只需将适当的掩码与 flags 的值进行按位 AND 运算。要关闭一个位，你将 flags 与一个掩码进行按位 AND 运算，该掩码中要关闭的位为 0，其他所有位为 1。你可以通过对一个设置了相应位的掩码应用取反运算符来轻松生成这样的掩码，而 bit6mask 正是这样一个掩码。当然，如果要关闭的位已经是 0，它将保持为 0。

## 变量的生存期

所有变量都有有限的生存期。它们从你定义它们的那一刻起开始存在，并在某个时刻被销毁——最迟在你的程序结束时。特定变量能存在多久由其存储期决定。存储期有四种不同类型：

- 在块内定义的变量具有**自动存储期**。它们从定义点开始存在，直到块结束，也就是右花括号 `}`。它们被称为**自动变量**或**局部变量**。自动变量具有局部作用域或块作用域。到目前为止，你创建的所有变量都是自动变量。
- 使用 `static` 关键字定义的变量具有**静态存储期**。它们被称为**静态变量**。静态变量从定义点开始存在，并一直持续到程序结束。你将在第8章和第12章了解静态变量。
- 在运行时为其分配内存的变量具有**动态存储期**。它们从你创建之时起存在，直到你释放其内存以销毁它们。你将在第5章学习如何动态创建变量。
- 用 `thread_local` 关键字声明的变量具有线程存储期。不过，线程局部变量是一个高级主题，因此本书不会涉及。

变量的另一个属性是*作用域*。变量的作用域是程序中变量名有效的部分。在变量的作用域内，你可以引用它、设置它的值或在表达式中使用它。在其作用域之外，你不能引用它的名字。任何这样做的尝试都会导致编译器错误消息。请注意，变量在其作用域之外可能仍然存在，即使你不能引用它。稍后当你学习具有静态和动态存储期的变量时，你会看到这种情况的例子。

> 注意 请记住，变量的*生存期*和*作用域*是不同的概念。生存期是变量存活的执行时间周期。作用域是可以使用变量名的程序代码区域。重要的是不要混淆这两个概念。

### 全局变量

在定义变量的位置方面，你有很大的灵活性。最重要的考虑因素是变量需要具有什么样的作用域。你通常应该将定义放在尽可能靠近变量首次使用的地方。这会使你的代码更容易被其他程序员理解。在本节中，我们将介绍一个不符合这种情况的例子：所谓的全局变量。

你可以在程序中所有函数之外定义变量。在所有块和类之外定义的变量也称为*全局变量*，具有*全局作用域*（也称为*全局命名空间作用域*）。这意味着它们可以在源文件中定义点之后的所有函数中访问。如果你在源文件的开头定义它们，它们将在整个文件中可访问。在第11章中，我们将展示如何声明可在多个文件中使用的变量。

全局变量默认具有*静态存储期*，因此它们从程序开始时就存在，直到程序执行结束。全局变量的初始化发生在 `main()` 执行之前，因此它们在变量作用域内的任何代码中始终可以使用。如果你没有初始化全局变量，它默认会被零初始化。这与自动变量不同，自动变量在未初始化时包含垃圾值。

图3-3显示了源文件 Example.cpp 的内容，并说明了文件中每个变量的作用域范围。

