

## 第 3 章 类、对象与方法

[mainWindow erase]; 清空窗口

theArea = [my area]; 计算矩形的面积

[userText spellCheck]; 对某些文本进行拼写检查

[deskCalculator clearEntry]; 清空上一次输入

[favoritePlaylist showSongs]; 显示收藏播放列表中的歌曲

[phoneNumber dial]; 拨打电话

[table reloadData]; 显示更新后的表格数据

n = [Touch tapCount]; 存储 days 被点击的次数

## 用于处理分数的 Objective-C 类

现在是时候在 Objective-C 中定义一个实际类，并学习如何操作该类的实例了。

再次，你将首先学习过程。因此，实际的程序示例可能看起来并不实用。我们稍后会介绍更实用的内容。

假设你需要编写一个程序来处理分数。可能你需要处理加法、减法、乘法等。如果你不知道类，你可能会从一个类似简单的程序开始：

### 程序 3.1

```objc
// 处理分数的简单程序

#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    NSAutleasePool *pool = [[AutoreleasePool alloc] init];
    int numerator = 1;
    int denominator = 3;
    NSLog("The fraction is %i/%i", numerator, denominator);

    [pool drain];
    return 0;
}
```

### 程序 3.1 输出

分数是 1/3

在程序 3.1 中，分数根据分子和分母被创建。在创建自动释放池后，main 函数中的两行将变量 `numerator` 和 `denominator` 声明为整数，并分别为它们赋值了初始值 1 和 3。这等同于以下代码：

```objc
numerator = 1;
denominator = 3;
```

## 用于处理分数的 Objective-C 类

我们通过在变量 `numerator` 中存储 1，在变量 `denominator` 中存储 3 来表示分数 1/3。如果你需要在程序中存储许多分数，这可能会非常繁琐。每当你引用该分数时，都必须引用对应的分子和分母。对这些分数进行操作也会同样笨拙。

如果将分数定义为一个单一实体，并用一个名称（如 `myFraction`）统一引用其分子和分母，将会更好。你可以在 Objective-C 中这样做，这从定义一个新类开始。

程序 3.2 使用名为 `Fraction` 的新类复制了程序 3.1 的功能。下面是该程序，随后是对其工作原理的详细解释。

### 程序 3.2

```objc
// 处理分数的程序 - 类版本

#import <Foundation/Foundation.h>
//--接口部分 ---

@interface Fraction: NSObject
{
    int numerator;
    int denominator;
}

-(void) print;
-(void)setNumerator:(int) n;
-(void)setDenominator:(int) d;

@end

//---@实现部分 ---

@implementation Fraction
-(void) print;
{
    NSLog("%d/%d", numerator, denominator);
}

-(void)setNumerator:(int) n
{
    numerator = n;
}

-(void)setDenominator:(int) d
{
    denominator = d;
}

@end

//---程序部分 ---
```

## 第 3 章 类、对象与方法

```objc
int main (int argc, char *argv[]) {
    NSAutleasePool *pool = [[NSAutleasePool alloc] init];
    Fraction *myFraction;

    // 创建一个 Fraction 实例
    myFraction = [[Fraction alloc] init];
    myFraction = [myFraction init];

    // 设置分数为 1/3
    [myFraction setNumerator:1];
    [myFraction setDenominator:3];

    // 使用 print 方法显示分数
    NSLog(@"The value of myFraction is %@",
          [myFraction print]);

    [pool drain];
    return 0;
}
```

### 程序 3.2 输出

分数的值是:1/3

从程序 3.2 的注释可以看出，程序逻辑上分为三个部分：

- 接口部分 (interface)
- 实现部分 (implementation)
- 程序部分 (program)

接口部分描述类，实现部分包含实际代码，而程序部分包含主函数。当你定义一个新类时，必须做几件事：首先，命名类；其次，指定类包含的数据；最后，定义方法。

## 接口部分

通用格式如下：

```objc
@interface NewClassName: ParentClassName
{
    memberDeclarations;
}
methodDeclarations;
@end
```

按照约定，命名类时以大写字母开头。实例变量、对象和方法名通常以小写字母开头。为了提高可读性，名称内部使用大写字母指示新单词，例如：

- AddressBook—这可能是一个类名。
- currentEntry—这可能是一个对象。
- current_entry—有些程序员使用下划线作为分隔符。
- addNewEntry—这可能是一个方法名。

## 选择命名

规则非常简单：必须以字母或下划线 (_) 开头，后面可以跟任意组合的字母（大小写）、下划线或数字 0–9。以下是有效名称：

- sum
- pieceFlag
- i
- myLocation
- numberOfOfMoves
- sysFlag
- ChessBoard

另一方面，以下无效：

- sumvalue—包含了非法字符。
- piece flag—不允许空格。
- 3Spencer—不能以数字开头。
- int—这是一个保留字。

int 不能作为变量名，因为它对 Objective-C 编译器有特殊意义。通常，任何对 Objective-C 编译器有特殊意义的名称都不能作为变量名。这个词被称为保留名或保留字。始终记住，大小写字母在 Objective-C 中是区分的。在这里，变量名 sum、Sum 和 SUM 分指不同的变量。

在决定名称时，请记住一点建议：不要偷懒。选择反映变量或对象意图的名称。理由显而易见。正如注释一样，有意义的命名可以极大提高程序的可读性，并在调试和文档阶段获得回报。事实上，文档任务可能会变得简单得多，因为程序变得更加自明了。

这里再次是程序 3.2 的接口部分：

```objc
//@interface section ---

@interface Fraction: NSObject
{
    int numerator;
    int denominator;
}

-(void) print;
-(void)setNumerator:(int) n;
-(void)setDenominator:(int) d;

@end
```

NSObject 类是

