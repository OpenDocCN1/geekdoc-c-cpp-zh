

$(3.31 \times 10^{-8} + 2.01 \times 10^{-7}) / (7.16 \times 10^{-6} + 2.01 \times 10^{-8})$

6. **复数**是包含两个部分的数字：一个*实*部和一个*虚*部。如果 $a$ 是实部而 $b$ 是虚部，则使用这种记法来表示该数字：

$a + b i$

编写一个 Objective-C 程序，定义一个名为 *Complex* 的新类。遵循为 *Fraction* 类建立范式，为你的新类定义以下方法：

```
- (void) setReal:(double) a;
-(void) setImaginary:(double) b;
-(void) print; // 显示为 a + b
-(double) real;
-(double) imaginary;
```

编写一个测试程序来测试你的新类和方法。

+ 7. 假设你正在开发一个处理图形对象的例程库。首先定义一个名为 **Rectangle** 的新类。目前，跟踪矩形的宽度和高度。开发方法来设置矩形的宽度和高度、获取这些值，并计算矩形的面积和周长。假设这些矩形对象描述积分网格（如计算机屏幕）上的矩形。在这种情况下，假设矩形的宽度和高度是整数值。

以下是 Rectangle 类的 @interface 部分：

```
@interface Rectangle: NSObject

-(void) setWidth:(int) w;
-(void) setHeight:(int) h;
-(int) width;
-(int) height;
-(int) area;
-(int) perimeter;
@end
```

编写实现部分和一个测试程序来测试你的新类和方法。

+ 8. 程序 4.6 中的 add:, subtract:, multiply:, 和 divide: 方法没有返回值。修改这些方法，使其在计算后返回累加器的值。测试这些新方法。

+ 9. 在完成练习 8 后，在 Calculator 类中添加以下方法并测试它们：

```
-(double) changeSign; // 改变累加器的符号
-(double) reciprocal; // 1/累加器
-(double) xSquared; // 累加器的平方
```

+ 10. 为程序 4.6 中的 Calculator 类添加内存功能。实现以下方法声明并测试它们：

```
-(double) memoryClear; // 清除内存
-(double) memoryStore; // 将累加器存入内存
-(double) memoryRecall; // 将内存存入累加器
-(double) memoryAdd:(double) value; // 将值加入内存
-(double) memorySubtract:(double) value; // 从内存中减去值
```

# 5. 程序循环

在 Objective-C 中，你可以通过多种方式重复执行一段代码。这些循环能力是本章的主题，它们由：

- `for` 语句
- `while` 语句
- `do` 语句

我们从一个简单的例子开始：数数。如果你将 15 颗弹珠排列成三角形，你最终得到的排列可能像图 5.1 所示。

# 图 5.1. 三角形排列
![](img/6897a0c84e3cb4e5aad2fad0b121.png)

三角形的第一行包含一颗弹珠，第二行包含两颗弹珠，依此类推。通常情况下，形成包含 $n$ 行的三角形所需的弹珠数是从 1 到 $n$ 的整数之和。这个和被称为*三角形数*。如果你从 1 开始，第四个三角形数就是连续整数 $1 + 2 + 3 + 4$ 之和，即 10。假设你想写一个程序来计算并显示第八个三角形数。显然，你可以很容易在脑中算出这个数，但为了辩证，让我们假设你想用 Objective-C 写一个程序来完成这项任务。程序 5.1 展示了这样一个程序。

# 程序 5.1
```
#import <Foundation/h>

// 计算第八个三角形数的程序
int main (int argc, char * argv[]) {
    @autoreleasepool {
        int triangularNumber = 1 + 2 + 3 + 4 + 5 + 6 + 7 + 8;
        NSLog("The triangular number is %i", triangularNumber);
    }
    return 0;
}
```

# 程序 5.1. 输出
三角形数为 36

程序 5.1 的技术对于计算三角形数很好，但如果你需要找到第 200 个三角形数的值，会发生什么？修改程序 5.1 来显式添加从 1 到 200 的所有整数无疑是乏味的。幸运的是，有一种简单的方法。计算机的基本属性之一是它重复执行一组语句的能力。这些循环能力使程序员能够编写简洁的程序，否则可能需要数千甚至百万条语句。Objective-C 语言包含三种程序语句。

# for 语句

让我们来看一个使用 for 语句的程序。程序 5.2 的目的是计算第 200 个三角形数。看看你是否能确定 `for` 语句是如何工作的。

# 程序 5.2
```
// 计算第 200 个三角形数的程序
// for 语句的介绍
#import <Foundation/h>

int main (int argc, char * argv[])
{
    @autoreleasepool {
        int n, triangularNumber;

        triangularNumber = 0;

        for ( n = 1; n <= 200; n++ )
            triangularNumber += n;

        NSLog("The triangular number is %i", triangularNumber);

        return 0;
}
```

# 程序 5.2. 输出
第 200 个三角形数为 20100

程序 5.1 的技术对于计算三角形数很好，但如果你需要找到第 200 个三角形数的值，会发生什么？修改程序 5.1 来显式添加从 1 到 200 的所有整数无疑是乏味的。幸运的是，有一种简单的方法。计算机的基本属性之一是它重复执行一组语句的能力。这些循环能力使程序员能够编写简洁的程序，否则这些可能需要数千甚至百万条语句。Objective-C 语言包含三种程序语句。

