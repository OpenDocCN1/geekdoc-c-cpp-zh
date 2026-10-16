

## NOTE

此处忽略引用 NSAutoreleasePool 的代码。你将在后面的章节学习到它。

本书中你还会遇到另一种不寻常的指针情况，围绕着指向对象的指针的使用，例如使用 NSError 对象从失败的调用中获取错误消息的情况。当我在第 10 章讨论这个问题时，我会更详细地介绍。

## 使用运算符

与数学类似，编程语言通常支持运算符。运算符是一种“操作”变量和值的函数。例如，表达式“5 + 4”包含值 5 和 4 以及运算符 +。在这种情况下，+ 运算符被称为二元运算符。因此，它操作两个值，一个在左边一个在右边，即 5 和 4。另一种类型的运算符是单目运算符。单目运算符只有一个操作的值。例如，取地址运算符 & 就是一个单目运算符。它获取其操作的值的地址。

表 2.2 显示了 Objective-C 中大多数典型的运算符。

| Operator | Purpose |
|---|---|
| Table 2.2 Typical operators |  |
| () [] -> . | Parentheses, array operations, dereference |
| ! ~ - + * & ++ -- | Not, add/subtraction (unary), dereference (unary), address-of (unary), increment (unary), decrement (unary) |
| * / % | Multiplication, Division, Modulus (binary) |
| << >> | Bitwise Shift (binary) |
| < <= > >= | Comparison Operators (binary) |
| == != | Comparison Operators (binary) |
| & | Bitwise AND (binary) |
| ^ | Bitwise XOR (binary) |
| | | Bitwise OR (binary) |
| && | AND (binary) |
| || | OR (binary) |
| = += -= *= /= %= &= |= ^= <<= >>= | Assignment Operators (binary) |

通常，运算符会返回某种结果，该结果要么被赋给一个变量，要么在控制语句中使用以影响程序流程。例如，输入清单 2.21 中的示例程序并查看输出。

### Listing 2.21

### Working with operators

```
#import <Foundation/Foundation.h>

int main(int argc, char *argv[])
{
    int a = 10;
    int b = 3;
    int c = a + b;
    int d = a - b;
    int e = a * b;
    int f = a / b;
    int g = a % b;
    
    NSLog(@"a: %ld", a);
    NSLog(@"b: %ld", b);
    NSLog(@"c: %ld", c);
    NSLog(@"d: %ld", d);
    NSLog(@"e: %ld", e);
    NSLog(@"f: %ld", f);
    NSLog(@"g: %ld", g);
    
    return 0;
}
```

在这段代码中，我们将值 3 和 7 分别赋给 a 和 b；然后我们使用 + 运算符将它们相加，使用 - 运算符将它们相减，进行乘法、除法等等。运行程序即可看到图 2.5 所示的输出。

请注意，程序打印出每个数学运算的结果。现在我在这个程序中加入了一个小麻烦。如果你注意一下，f 的值是错误的。这是因为 10 除以 3 的结果不是一个整数，而是一个分数。或者在计算机上，它是一个浮点数。通常，你可能希望将其存储到 float 或 double 中，这两者都可以表示浮点值；在这种情况下，我们将其存储到 int 值中，这意味着该值的十进制部分将被截断，只剩下整数部分

## 三元运算符

除了我已经向你展示的单目和二元运算符之外，还有一个三元运算符。这个运算符是 ? : ，可以用在 if/else 语句的位置。我不会在这里介绍这个运算符，因为它更适合放在本章的“控制程序流程”部分。因此，请在该部分查找更多信息。

## 使用函数

到目前为止，我向你展示了如何将指令提供给计算机，以便计算机按顺序执行这些指令。但是，随着程序规模和复杂性的增长，你会很快发现，在程序中将所有指令按顺序一个接一个地放置会变得极其繁琐。你希望重用代码的一部分，而复制粘贴是重用代码的非常糟糕的方法。

幸运的是，你可以使用几种机制来解决这两个问题。我将在本节中解释的第一个机制是使用函数的概念。在面向对象编程之前，过程式编程是分解程序以便更易于重用的首选方法。

当然，Objective-C 是一个完全面向对象的编程语言，在你的应用程序开发中你大部分时间会使用面向对象编程。然而，过程式编程是一个至关重要的基础构建块，你需要理解它，因为 Objective-C 中仍然有一些部分本质上是过程式的。

### 理解函数

你可能要问的第一个问题是：“什么是函数？” 答案是，函数本质上是在你的应用程序中声明子程序的方法。函数使你能够将程序指令的一部分封装成可以命名然后在应用程序的任何地方按需多次使用的东西。

看一个例子；清单 2.22 显示了一个计算 5 的阶乘的程序（它应该产生 120 的值）。它使用 for 循环进行计算，我将在下一节讨论这个概念，但现在你可以忽略它，只需理解它是在进行计算即可。

### Listing 2.22

### Calculating a factorial

```
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
```

### Listing 2.22 (continued)

```
{
    int a = 5;
    int result = 1;

    for(int i = 1; i <= a; ++i)
    {
        result = result * i;
    }

    NSLog(@"%ld", result);

    return 0;
}
```

现在，这个程序有趣的地方在于，我们在这里做了相当多的工作来完成这个计算。如果我们想改变我们计算阶乘的数字怎么办？也许最好将那段代码隔离到一个函数中，以便我们可以一次又一次地重用它。也许我们可以创建一个函数，它只接受一个 int 作为参数，然后返回该 int 的阶乘。

清单 2.23 显示了我已完全这样做的程序。

### Listing 2.23

### Extracting the calculation to a function

```
#import <Foundation/Foundation.h>

long int calculateFactorial(int value)
{
    long int result = 1;

    for(int i = 1; i <= value; ++i)
    {
        result = result * i;
    }

    return result;
}

int main (int argc, const char * argv[])
{
    int a = 5;
```

```
long int result = calculateFactorial(a);

NSLog(@"%ld", result);

return 0;
}
```

我之前在 main 函数中拥有计算阶乘的代码，现在我们调用的是我们的 calculateFactorial 函数。包含我们想要计算的值的变量在我们的 main 函数的局部作用域中声明，因此我们的 calculateFactorial 函数不知道它。为了将值从我们的 main 函数传递到我们的 calculateFactorial 函数，你必须通过函数调用将值传递给 calculateFactorial 函数。

如果你编译并运行此程序，它应该会给你与之前几乎相同的输出。现在你可以使用该代码为一堆不同的值计算阶乘。这在清单 2.24 中显示。

### Listing 2.24

### Demonstrating use of the function

```
#import <Foundation/Foundation.h>

long int calculateFactorial(int value)
{
    long int result = 1;

    for(int i = 1; i <= value; ++i)
    {
        result = result * i;
    }

    return result;
}

int main (int argc, const char * argv[])
{
    NSLog(@"5!: %ld", calculateFactorial(5));
    NSLog(@"10!: %ld", calculateFactorial(10));
    NSLog(@"15!: %ld", calculateFactorial(15));
    NSLog(@"20!: %ld", calculateFactorial(20));

    return 0;
}
```

