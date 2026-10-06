

```
// 用于处理分数的简单程序

#import <Foundation/Foundation.h>

int main (int argc, char * argv[])
{
    @autoreleasepool {
        int numerator = 1;
        int denominator = 3;
        NSLog (@"The fraction is %i/%i",
        numerator, denominator);
    }
    return 0;
}
```

## 程序 3.1. 输出

The fraction is 1/3

在程序 3.1 中，分数是以分子和分母的形式表示的。在 @autoreleasepool 指令之后，main 中的两行代码都将变量 numerator 和 denominator 声明为整数（int），并分别为它们赋值了初始值 1 和 3。这等同于以下代码：

```
int numerator, denominator;
```

numerator = 1;
denominator = 3;

我们通过将 1 存储在变量 numerator 中，将 3 存储在变量 denominator 中，用此表示了分数 1/3。如果你需要在程序中存储大量的分子，这可能会非常麻烦。

每当你想要引用这个分数时，都必须引用相应的分子和分母。对这些分数进行操作也将同样笨拙。

如果能将分数定义为一个单一实体，并用一个名称（如 myFraction）统一引用它的分子和分母，将会更好。你可以在 Objective-C 中实现这一点，这从定义一个新类开始。

程序 3.2 使用一个名为 Fraction 的新类复制了程序 3.1 的功能。下面是该程序，随后是关于其工作原理的详细解释。

## 程序 3.2

```
// 处理分数的程序 - 类版本
#import <Foundation/Foundation.h>
//---- @interface 区域 ----
@interface Fraction: NSObject

-(void) print;
-(void) setNumerator:(int) n;
-(void) setDenominator:(int) d;
@end

//---- @implementation 部分 ----

@implementation Fraction
```

```
{
  int numerator;
  int denominator;
}
-(void) print {
  NSLog("%d/%d", numerator, denominator);
}
```

```
-(void) setNumerator:(int) n {
  numerator = n;
}
```

```
-(void) setDenominator:(int) d {
  denominator = d;
}
```

@end
//--- 程序部分 ----

```
int main (int argc, char * argv[]) {
  @autoreleasepool {
    Fraction *myFraction;
    // 创建 Fraction 的实例
    myFraction = [Fraction alloc];
    myFraction = [myFraction init];
    // 将分数设置为 1/3
```

```
[myFraction setNumerator: 1];
[myFraction setDenominator: 3];

// 使用 print 方法显示分数

NSLog("The value of myFraction is:");
[myFraction print];
}
return 0;
}
```

## 程序 3.2. 输出

The value of myFraction is:
1/3

正如你从程序 3.2 的注释所示，该程序在逻辑上被分为三个部分：

- @interface 区域
- @implementation 区域
- program部分

@interface 区域描述了类及其它的方法，而 @implementation 区域描述了数据（来自该类的对象将存储的实例变量），并包含了实现接口区域中声明的方法的实际代码。最后，程序部分包含了执行程序预期目的的程序代码。

## 注意

你还可以在 interface 区域声明类的实例变量。在 implementation 区域执行此操作是从 Xcode 4.2 开始添加的，并被认为是定义类的更好方法。你将在后面的章节中学习更多关于原因的内容。

这些部分中的每一个都是每个 Objective-C 程序的一部分，尽管你可能不需要自己编写每个部分。正如你所看到的，每个部分通常被放在自己的文件中。不过，目前我们把它们都放在一个文件中。

## @interface 区域

当你定义一个新类时，你必须告诉 Objective-C 编译器该类来自哪里。也就是说，你必须为它的父类命名。接下来，你需要定义在处理来自此类的对象时可以使用的操作类型（或方法）。正如你将在后面的章节中学习到的那样，你在程序中名为 @interface 区域的特殊部分中列出称为属性的项。该部分的通用格式如下：

```
@interface NewClassName:ParentClassName
propertyAndMethodDeclarations;
@end
```

按照惯例，类名以大写字母开头，尽管这不是强制要求的。这使得阅读你程序的人只需查看名称的第一个字母就能区分类名与其他类型的变量。让我们稍作休息，聊聊 Objective-C 中的命名。

## 选择命名

在第 2 章“在 Objective-C 中编程”中，你使用了几个变量来存储整数值。例如，你在程序 2.4 中使用了变量 sum。

Objective-C 语言允许你存储整数以外的数据类型，字符，甚至是引用。命名的规则非常简单：它们必须以字母开头，后面可以跟数字或下划线。以下是有效的名称示例：

- sum
- pieceFlag
- i
- locationLocation
- numberOfMoves
- ChessBoard

在决定名称时，请记住一点建议：不要偷懒。选择反映变量意图的名称。原因是显而易见的。正如注释语句一样，有意义的命名可以极大提高程序的可读性，并在调试和文档阶段获得回报。

始终记住，在 Objective-C 中大小写字母是不同的。因此，在命名类时，要以大写字母开头。实例变量和方法名，另一方面，通常以小写字母开头。为了辅助可读性，以下是合法的名称示例：

- AddressBook
- currentEntry
- current_entry
- addNewEntry

正如你所看到的，在 3.2 程序的注释中，程序在逻辑上分为三个部分：

- @interface 区域
- @implementation 区域
- program部分

这里，再次是程序 3.2 中的 @interface 区域：

```
//--- @interface 部分 ---

@interface Fraction: NSObject

-(void) print;
```

```
- (void) setNumerator:(int) n;
- (void) setDenominator:(int) d;

@end
```

类的名称是 Fraction，它的父类是 NSObject。（我们将在第 8 章“继承”中详细讨论父类）。NSObject 类定义在 NSObject.h 中，每当你导入 Foundation.h 时，它都会被包含。

## 类方法和实例方法

你必须定义方法来处理你的分数。你需要能够将分数的值设置为特定值。由于你无法直接访问分数的内部表示（换说，直接访问实例变量），你必须编写方法来设置分子和分母。你还将编写一个名为 print 的方法来显示分数的值。该方法在接口文件中的声明如下：

```
- (void) print;
```

前面的减号 (-) 告诉 Objective-C 编译器该方法是一个实例方法。唯一的其他选项是加号 (+)，它表示类方法。类方法是针对类本身执行某些操作的方法，例如创建类实例。

实例方法是对类的特定实例执行某些操作，例如设置其值、检索其值、显示其值等。参考汽车的例子，在制造出汽车后，你可能需要为它加油。

