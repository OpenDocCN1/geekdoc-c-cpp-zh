
向其加气的操作是在特定的汽车上执行的，因此它比比实例方法。

# 返回值

当你声明一个新方法时，你必须告诉 Objective-C 编译器该方法是否返回值，如果返回，它返回的是什么类型的值。你通过在开头的减号或加号后面将返回类型括在括号中来实现。因此，此声明指定名为 `currentAge` 的实例方法返回一个整数值：

+ - (int) currentAge;

同样，这行代码声明了一个返回双精度值的方法。（你将在[第 4 章，“数据类型与表达式”]中学习更多关于这种数据类型的知识）

+ - (double) retrieveDoubleValue;

使用 Objective-C 的 `return` 语句从方法返回值，这与我们在之前的程序示例中从 `main` 返回值的方式相似。

如果方法不返回值，你使用 `void` 类型来指示，如下所示：

+ - (void) print;

这声明了一个名为 `print` 的不返回值的实例方法。在这种情况下，你不需要在方法的末尾执行 `return` 语句。或者，你可以执行一个不带任何指定值的 `return`，如下所示：

```
return;
```

# 方法参数

在程序 3.2 的 `@interface` 部分还声明了两个方法：

```
- (void) setNumerator:(int) n;
- (void) setDenominator:(int) d;
```

这两者都是不返回值的实例方法。每个方法接受一个整数参数，通过参数前的 `(int)` 指明。在 `setNumerator` 的情况下，参数的名字是 `n`。这个名字是任意的，它是方法用于引用该参数的名称。因此，`setNumerator` 的声明指定将一个名为 `n` 的整数参数传递给方法，并且不返回任何值。`setDenominator` 也是如此，只是它的参数名称是 `d`。

注意这些方法声明的语法。每个方法名都以冒号结尾，这告诉 Objective-C 编译器该方法期望看到一个参数。接下来，用一组括号指定了参数的类型，这与指定方法本身的返回类型的方式非常相同。最后，指定用于在方法中标识该参数的符号名称。整个声明以分号结束。图 3.1 描述了这种语法。

# 图 3.1. 声明方法

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_69_0.png)

当方法接受参数时，你在引用该方法时也在方法名后附加一个冒号。因此，`setNumerator:` 和 `setDenominator:` 是标识这两个方法的正确方式，每个方法都接受单个参数。此外，不带尾随冒号的 `print` 方法表示该方法不接受任何参数。在第 7 章“类的更多内容”中，你将看到如何标识接受多个参数的方法。

# @implementation 部分

如所述，`@implementation` 部分包含了你在 `@interface` 部分中声明的方法的实际代码。你必须指定要在此类的对象中存储什么类型的数据的数据。也就是说，你必须描述类成员将包含的数据。这些成员被称为实例变量。从术语上来说，你说在 `@interface` 部分声明了方法，并在 `@implementation` 部分中定义了它们（即提供实际代码）。`@implementation` 部分的通用格式如下：

```
@implementation NewClassName{
  memberDeclarations;
  methodDefinitions;
}
@end
```

`NewClassName` 是在 `@interface` 部分使用的类相同的名称。你可以使用尾随冒号后跟父类名，就像我们在 `@interface` 部分做的那样：

```
@implementation Fraction: NSObject
```

然而，这是可选的，且通常不这样做。

`memberDeclarations` 部分指定了 `Fraction` 中存储了什么类型以及它们的名称。这通过以下内容实现：

```
int numerator;
int denominator;
```

`methodDefinitions` 部分包含了方法的代码。这里是 `Fraction` 的 `@implementation`：

```
@implementation Fraction
{
int numerator;
int denominator;
}

-(void) setNumerator:(int) n {
    numerator = n;
}

-(void) setDenominator:(int) d {
    denominator = d;
}

-(void) print {
    printf("%d/%d\n", numerator, denominator);
}

@end
```

`@implementation` 部分包含了你在 `@interface` 部分中声明的方法的代码。你必须指定要在此类的对象中存储什么类型的数据。也就是说，你必须描述类成员将包含的数据。这些成员被称为实例变量。从术语上来说，你说在 `@interface` 部分声明了方法，并在 `@implementation` 部分中定义了它们（即提供实际代码）。`@implementation` 部分的通用格式如下：

`memberDeclarations` 部分指定了 `Fraction` 中存储了什么类型以及它们的名称。这些是变量。这通过以下内容实现：

```
int numerator;
int denominator;
```

`methodDefinitions` 部分包含了方法的代码。这里是 `Fraction` 的 `@implementation`：

```
@implementation Fraction
{
int numerator;
int denominator;
}

-(void) setNumerator:(int) n {
    numerator = n;
}

-(void) setDenominator:(int) d {
    denominator = d;
}

-(void) print {
    printf("%d/%d\n", numerator, denominator);
}

@end
```某处必须有一个名为 `main` 的程序，正如我们之前提到的。这里是 3.2 的程序：

```
int main (int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *myFraction;

        // 创建 Fraction 的实例并对其初始化

        myFraction = [Fraction alloc];
        myFraction = [myFraction init];

        // 将分数设置为 1/3

        [myFraction setNumerator:1];
        [myFraction setDenominator:3];

        // 使用 print 方法显示分数
        NSLog("The value of myFraction is:");
        [myFraction print];
    }
    return 0;
}
```

在 `main` 中，你通过以下行定义了一个名为 `myFraction` 的变量：

```
Fraction *myFraction;
```

该行表示 `myFraction` 是 `Fraction` 类型的对象；也就是说，`myFraction` 用于存储来自你新类的值。变量前的星号在下文中有详细描述。

现在你有了用于存储 `Fraction` 的对象，你需要创建一个，就像你要求工厂制造一辆汽车一样。这通过以下行实现：

```
myFraction = [Fraction alloc];
```

`alloc` 是 allocate 的缩写。你想为一个新的分数分配内存存储空间。这个表达式向你新创建的类发送消息：

```
[Fraction alloc]
```

你请求 `Fraction` 类应用 `alloc` 方法，但你从未定义过 `alloc` 方法，那么它是从哪里来的呢？该方法继承自父类。第 8 章“继承”详细讨论了这一主题。

当你向类发送 `alloc` 消息时，你会得到该类的实例。在程序 3.2 中，返回值存储在你的变量 `myFraction` 中。`alloc` 方法保证将对象的所有实例变量置零。然而，这并不意味着对象已经为使用做好了初始化。你需要在分配后对其进行初始化。

这是通过程序 3.2 中的下一语句实现的，内容如下：

```
myFraction = [myFraction init];
```

再次，你正在使用一个你自己没有编写的方法。`init` 方法初始化类的实例。注意你正在向 `myFraction` 发送 `init` 消息。也就是说，你想

