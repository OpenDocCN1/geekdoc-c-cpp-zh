

`@interface` 部分定义在 `NSObject.h` 文件中，每当你导入 `Foundation.h`，它会自动包含在你的程序中。

## 实例变量

`memberDeclarations` 部分指定了 `Fraction` 中存储的数据类型以及这些数据类型的名称。如你所见，该部分被包含在自己的括号内。对于 `Fraction` 类，这些声明表示 `Fraction` 对象具有两个整数成员，分别称为 `numerator`（分子）和 `denominator`（分母）：

```
int numerator;
int denominator;
```

在该部分中声明的成员被称为实例变量。你会发现，每当你创建一个新对象时，都会创建一个新的且唯一的实例变量集合。因此，如果你名为 `fracA` 和 `fracB` 的 `Fraction`，它们每个都拥有自己独立的分子和分母。Objective-C 系统会自动为你跟踪这些，这是使用对象时很棒特性之一。

## 类方法和实例方法

你必须定义方法来处理你的 `Fraction`。你将能够将分数的的值设置为特定的值。由于你无法直接访问分数的内部表示（换句话说，无法直接访问其实例变量），必须编写方法来设置分子和分母。你还会编写一个名为 `print` 的方法来显示分数的的值。这里是 `print` 方法在接口中的声明形式：

```
(void) print;
```

开头的减号 (`-`) 通知 Objective-C 编译器该方法是一个实例方法。另一个选项是加号 (`+`)，它表示类方法。类方法是在类本身上执行某些操作的方法，例如创建该类的新实例。

实例方法是在类的特定实例上执行某些操作，例如设置其值、获取其值、显示其值等。参考汽车的例子，在你制造好汽车后，你可能需要给它加油。加油的操作是在特定的汽车上进行的，因此它类比于实例方法。

第 3 章 类、对象和方法

## 返回值

当你声明一个新方法时，必须告诉 Objective-C 编译器该方法是否返回一个值，如果返回，它返回的是什么类型的值。你通过在开头的减号或加号之后将返回类型括在括号内来实现。此声明指定名为 `currentAge` 的实例返回一个整数：

- - (int) currentAge;

同样，这行代码声明了一个返回双精度值的方法。（你将在第 4 章“数据类型和表达式”中学习更多关于这种类型的内容。）

- - (double) retrieveDoubleValue;

使用 Objective-C 的 `return` 语句从方法返回值，类似于我们在之前的程序示例中从 `main` 返回值的方式。如果方法不返回任何值，你使用 `void` 类型来指示：

- - (void) print;

这声明了一个名为 `print` 的不返回值的方法。在某些情况下，你不需要在方法的末尾执行 `return` 语句。或者，你可以执行不带任何指定值的 `return`，如下：

return;

## 方法参数

在程序 3.2 的 `@interface` 部分中声明了另外两个方法：

- - (void) setNumerator:(int) n;
- (void) setDenominator:(int) d;

这些是不返回返回值的实例方法。每个方法都接收一个整数参数，通过参数名称前的 `(int)` 指明。在 `setNumerator` 的情况下，参数的名称是 `n`。这个名称是任意的，是方法用于引用该参数的名称。因此，`setNumerator` 的声明指定将传递一个整数参数 `n` 给方法，且不返回任何值。`setDenominator` 类似，只是其参数的值是 `d`。

注意这些方法声明的语法。每个方法都以冒号结尾，这告诉 Objective-C 编译器该方法期望看到一个参数。接下来，指定参数的类型，并括在括号内，方式与方法本身指定返回类型相同。最后，指定用于在方法中标识该参数的符号名称。整个声明以分号结束。图 3.1 描述了这种语法。

## @implementation 部分 37

![](img/9a03a17dbf1900dce936c9665ab15c26_49_0.png)

图 3.1 声明方法

当一个方法接收参数时，当你引用该方法时，要在方法名后附加冒号。因此，`setNumerator:` 和 `setDenominator:` 是标识这两个方法的正确方式，它们每个都接收单个参数。同样，在不带末尾冒号的情况下标识 `print` 方法，表示该方法不接收任何参数。在第 7 章“更多关于类”中，你将看到如何标识接收多个参数的方法。

## @implementation 部分

如所述，`@implementation` 部分包含了在 `@interface` 部分中声明方法的实际代码。从术语上来说，你说在 `@interface` 部分中**声明**方法，并在 `@implementation` 部分中**定义**（即提供实际代码）它们。

`@implementation` 部分的标准格式如下：

```
@implementation NewClassName
methodDefinitions;
end
```

`NewClassName` 是在 `@interface` 部分用于类的相同名称。你可以使用冒号跟随父类名，就像我们在 `@interface` 部分中做的那样：

```
@implementation Fraction: NSObject
```

然而，这是可选的，通常不这样做。`@implementation` 部分的 `methodDefinitions` 包含了 `@interface` 部分指定的每个方法的代码。与 `@interface` 部分类似，每个方法的定义都从标识方法类型（类或实例）、其返回类型以及参数和类型开始。不是以分号结尾，而是紧随括在大括号内的方法代码。考虑程序 3.2 的 `@implementation` 部分：

```
//---- @implementation -----
@implementation Fraction
-(void)print
{
    NSLog("%d/%d", numerator, denominator);
}
```

```
(void) setNumerator: (int) n
{
  numerator = n;
}
```

```
(void) setDenominator: (int) d
{
  denominator = d;
}

```

@end
`print` 方法使用 `NSLog` 记录实例变量 `numerator` 和 `denominator` 的值。但该方法指的是哪个 `numerator` 和 `denominator` 呢？它指的是对象包含的变量。也就是说，你想初始化一个特定的 `Fraction` 对象。`setNumerator:` 将整数参数 `n` 存储在实例变量中。同样，`setDenominator:` 将其参数的值 `d`存储。

程序部分包含了解决问题的代码。这是你的程序开始的地方。这里是程序 3.2 的程序部分：

```
//---- program section ----
int main (int argc, char *argv[])
{
  NSAutleasePool *pool = [NSAutleasePool alloc] init];

  Fraction *myFraction;

  // 创建 Fraction 实例
  myFraction = [Fraction alloc];
  myFraction = [myFraction init];

  // 将分数设置为 1/3
  [myFraction setNumerator:1];
  [myFraction setDenominator:3];

  // 使用 print 方法显示分数
  NSLog("@The value of myFraction is:");
  [myFraction print];

  [myFraction release];
  [pool drain];

  return 0;
}
```

