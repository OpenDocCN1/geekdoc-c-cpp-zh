

# 你的第一个程序详解

main 是一个特殊的名称，精确地指示程序从这里开始执行。保留字 int 在 main 之前指定了返回值的类型。

现在你已经确定了系统，准备好精确指定此例程要执行的操作。这是通过将例程的所有程序语句封装在一对大括号 `{}` 中来实现。在最简单的情况下，一个语句就是一个以分号结尾的表达式。系统将大括号之间的所有程序语句视为 main 例程的一部分。程序 2.1 有四条语句。

程序 2.1 的第一条语句是

```
NSautoreleasePool pool = [NSautoreleasePool alloc] init;
```

它为自动释放池（autorelease pool）留出空间。我们将在第 17 章“内存管理”中详细介绍这一点。Xcode 会作为模板的一部分将此行自动放入你的程序中，所以暂时将其保留在那里即可。

下一条语句指定调用了一个名为 NSLog 的例程。传递或处理 NSLog 例程的参数是字符字符串：

```
"@Programming is fun!"
```

在这里，@ 符号紧跟在由双引号括起来的字符串之前。合称为一个常量 NSString 对象。

> 注意
如果你有 C 语言经验，可能会对开头的 @ 字符感到困惑。如果没有这个开头的 @ 字符，你写的是常量 C 风格字符串；有了它，你写的就是一个 NSString 对象。关于此主题的更多内容请见第 15 章。

NSLog 是 Objective-C 库中的一个函数，它只需显示或记录它的参数。在此，它会显示执行例程的日期、程序名称以及我们在此未描述的其他数字。在本书的其余部分，我们不再去显示 NSLog 在你的输出之前插入的这些文本。

在 Objective-C 中，你必须用分号 (;）终止所有的程序语句。这就是为什么在 NSLog 调用的右括号后面紧跟着一个分号。

在退出程序之前，你应该使用类似下面的代码释放已分配的内存池（以及与之相关的对象）：

```
[pool drain];
```

再次，Xcode 会自动为你将此行插入到程序中。同样，我们将对它的作用的详细解释推到稍后。

# 第 2 章 Objective-C 编程

main 中的程序语句看起来如下：
return 0;

它表示终止 main 的执行并返回状态值 0。
按照惯例，0 表示程序正常结束。任何非零值通常意味着发生了问题——例如，程序可能无法找到所需的文件。

如果你正在使用 Xcode 并看一眼输出窗口（参考图 2.9），你会记得在 NSLog 的输出行之后显示了以下内容：

Program exited with status value: 0.

你现在应该理解那条信息的意思了。
现在我们已经完成了你的第一个程序的调试，请修改它以也显示“And programming in Objective-C is even more fun!”这一短语。你可以通过添加另一个 NSLog 例程调用来实现，如程序 2.2 所示。记住每个 Objective-C 程序语句必须以分号终止。

# 程序 2.2

```
#import <Foundation.h>

int main (int argc, const char *argv[]) {
    NSAutleasePool *pool = [NSAutleasePool alloc];

    NSLog("Programming is fun!");
    NSLog("And programming in Objective-C is even more fun!");

    [pool drain];
    return 0;
}
```

如果你输入程序 2.2 并编译执行它，你可以预期如下输出（再次，不显示 NSLog 通常在输出前加缀的文本）：

# 程序 2.2 输出

Programming is fun!
Programming in Objective-C is even more fun!

正如你从下一个程序示例中所看到的，你不需要为每一行输出单独调用一次 NSLog 例程。
首先，我们来谈一种特殊的双字符序列。反斜杠 (\) 和字母 n 合称为换行符。换行符告诉系统精确执行其名称含义的操作：跳转到新行。换行符之后要打印的任何字符将出现在显示的下一行。事实上，换行符与打字机上的回车键非常相似（记得吗？）。

学习程序 2.3 中列出的输出，并在查看输出之前尝试预测结果（现在不准作弊了！）。

# 程序 2.3

```
#import <Foundation/Foundation.h>
int main (int argc, const char *argv[]) {
    NSAutleasePool * pool = [[NSAutleasePool alloc] init];

    NSLog(@"Testing...\n..1\n..2\n...3");
    [pool drain];

    return 0;
}
```

# 程序 2.3 输出

Testing...
..1
..2
...3

# 显示变量的值

NSLog 不仅可以显示简单的短语，计算的值和计算结果也可以显示。程序 2.4 使用 NSLog 例程显示两个数字（50 和 25）的相加结果。

# 程序 2.4

```
#import <Foundation/Foundation.h>
int main (int argc, const char *argv[]) {
    NSAutleasePool * pool = [[NSAutleasePool alloc] init];

    int sum;
    sum = 50 + 25;
    NSLog(@"The sum of 50 and 25 is %i", sum);
    [pool drain];

    return 0;
}
```

# 程序 2.4 输出

The sum of 50 and 25 is 75

main 内部在设置自动释放池之后的第一条程序语句定义了整数类型的变量 sum。在程序中使用任何变量之前，你必须先定义所有程序变量。变量的定义指定了 Objective-C 编译器程序应如何使用它。编译器需要这些信息来生成正确的指令，以便在变量中存储和检索值。定义为 int 类型的变量只能持有整数值——即没有小数位的值。整数值的示例有 3、5、-20 和 0。带有小数位的数字（如 2.14、2.455 和 27.0）被称为浮点数和实数。

整数变量 sum 存储了两个整数 50 和 25 相加的结果。我们在该变量定义之后特意留留了一个空行；这纯粹是风格问题。有时在程序中添加一个空行可以使程序更具可读性。
该程序语句读起来就像大多数语言一样：

```
sum = 50 + 25;
```

数字 50 与 25 相加（加号所示），结果（赋值运算符等号所示）存储在变量 sum 中。
程序 2.4 中的 NSLog 调用现在在括号内包含两个参数。这些参数用逗号分隔。NSLog 例程的第一个参数总是要显示的字符字符串。然而，在显示字符串的同时，你还希望显示某些程序变量的值。在这种情况下，你希望在这些字符之后显示变量 sum 的值：

The sum of 50 and 25 is

第一个参数中的百分号字符是 NSLog 函数识别的一种特殊字符。紧跟在百分号后面的后的字符指定了在该处要显示什么类型的值。在之前的程序中，NSLog 例程识别字母 i 表示要显示整数值。

每当 NSLog 例程在字符串内部发现 % 字符时，它会自动显示该例程的下一个参数的值。因为 sum 是 NSLog 的下一个参数，它的值会自动显示在“The sum of 50 and 25 is”之后。

现在尝试预测程序 2.5 的输出。

程序 2.5

```
int main (int argc, const char *argv[]) {
  NSAutleasePool *pool = [NSAutleasePool alloc init];
  int value1, value2, sum;

  value1 = 50;
  value2 = 25;
  sum = value1 + value2;

  NSLog(@"The sum of %i and %i is %i", value1, value2, sum);

  [pool drain];
  return 0;
}
```

