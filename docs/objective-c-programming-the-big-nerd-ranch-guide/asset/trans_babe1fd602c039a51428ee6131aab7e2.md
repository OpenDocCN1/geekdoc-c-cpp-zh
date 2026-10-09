

## 图 17.2 一个 StockHolding 对象数组

![](img/5f9368899ebf8d92fc145f8def1e89f8_117_0.png)

*此页有意留空*

当你创建 **Person** 类时，你将其声明为 **NSObject** 的子类。这意味着 **Person** 的每个实例都将拥有在 **NSObject** 中定义的实例变量和方法，同时也拥有在 **Person** 中定义的实例变量和方法。我们说 **Person** 从 **NSObject** *继承* 了实例变量和方法。在本节中，我们将深入探讨继承。

打开 BMITime 项目并创建一个新文件：一个 Objective-C 类。将其命名为 Employee，并创建为 **NSObject** 的子类。很快，我们将把 **Employee** 类更改为 **Person** 的子类。这说得通，对吧？员工都是人。他们也有身高和体重。然而，并非所有人都是员工。我们还将为一个类添加一个员工特有的实例变量——员工 ID。

![](img/5f9368899ebf8d92fc145f8def1e89f8_119_0.png)

打开 Employee.h。导入 Person.h，将父类更改为 **Person**，并添加一个实例变量来保存员工的 ID 号：

```objectivec
#import "Person.h"

@interface Employee : Person
{
    int employeeID;
}
@property int employeeID;
@end
```

打开 Employee.m 并综合访问器：

```objectivec
#import "Employee.h"
@implementation Employee

@synthesize employeeID;

@end
```

现在，你拥有了一个包含 **Person** 所有实例变量和一个名为 employeeID 的新实例变量的新 **Employee** 类。**Employee** 的实例将响应与 **Person** 的实例相同的消息。**Employee** 的实例还将响应 setEmployeeID: 和 employeeID 消息。

而且，由于 **Person** 继承自 **NSObject**，**Employee** 也继承了 **NSObject** 中的所有实例变量和方法。所有对象都（直接或间接地）继承自 **NSObject**。

**NSObject** 有很多方法，但只有一个实例变量：isa 指针。每个对象的 isa 指针都指向创建它的类。

## 图 18.2 BMITime 的对象图

![](img/5f9368899ebf8d92fc145f8def1e89f8_120_0.png)

假设你向某个对象发送了名为 fido 的消息。为了响应这个消息，对象使用 isa 指针找到其类，并询问：“你有一个名为 fido 的实例方法吗？”如果该类有一个名为 fido 的方法，它就会执行。如果该类没有 fido 方法，它会向父类询问：“你有一个名为 fido 的实例方法吗？”它沿着链条一路向上寻找名为 fido 的方法。当找到该方法或到达链条顶端时，搜索停止。在链条顶端，**NSObject** 说：“不，没有 fido 方法。”然后你会收到一条错误消息，内容大致为“此 **Employee** 实例不响应 fido 选择器。”

试一试。打开 main.m，向 **Person** 的实例发送一条它无法理解的消息：

```objectivec
int main(int argc, const char * argv[])
{
    @autoreleasepool {
        
        // 创建一个 Person 的实例
        id person = [[Person alloc] init];
        
        // 给实例变量赋予有趣的值
        [person setWeightInKilos:96];
        [person setHeightInMeters:1.8];
        
        // 调用 bodyMassIndex 方法
        float bmi = [person bodyMassIndex];
        NSLog(@"person (%d, %f) has a BMI of %f",
              [person weightInKilos], [person heightInMeters], bmi);

        [person count];
        
    }
    return 0;
}
```

构建并运行程序。（忽略编译器的警告，因为你这是故意这样做的。在大多数情况下，如果你看到这个警告，你应该注意它！）你应该会在控制台中看到记录的运行时异常：

```text
*** Terminating app due to uncaught exception 'NSInvalidArgumentException',
reason: '-[Person count]: unrecognized selector sent to instance 0x00108de0'
```

检查完异常后，在继续之前删除有问题的行。

你创建了这个新的 **Employee** 类，但还没有使用它。更改 main.m 以使用 **Employee**：

```objectivec
#import <Foundation/Foundation.h>
#import "Employee.h"

int main(int argc, const char * argv[])
{
    @autoreleasepool {
        
        // 创建一个 Person 的实例
        Person * person = [[Employee alloc] init];
        
        // 给实例变量赋予有趣的值
        [person setWeightInKilos:96];
        [person setHeightInMeters:1.8];
        
        // 调用 bodyMassIndex 方法
        float bmi = [person bodyMassIndex];
        NSLog(@"person (%d, %f) has a BMI of %f",
              [person weightInKilos], [person heightInMeters], bmi);
        
    }
    return 0;
}
```

请注意，你的 person 变量仍然被声明为指向 **Person** 的指针。你认为这会造成问题吗？构建并运行程序，你会发现程序仍然运行良好。这是因为员工是一种人——它可以做一个人能做的任何事。也就是说，我们可以在程序期望使用 **Person** 实例的任何地方使用 **Employee** 的实例。

然而，现在你要使用 **Employee** 独有的方法，因此必须更改指针变量的类型：

```objectivec
#import <Foundation/Foundation.h>
#import "Employee.h"

int main(int argc, const char * argv[])
{
    @autoreleasepool {

        // 创建一个 Person 的实例
        Employee *person = [[Employee alloc] init];

        // 给实例变量赋予有趣的值
        [person setWeightInKilos:96];
        [person setHeightInMeters:1.8];
        [person setEmployeeID:15];

        // 调用 bodyMassIndex 方法
        float bmi = [person bodyMassIndex];
        NSLog(@"Employee %d has a BMI of %f", [person employeeID], bmi);

    }
    return 0;
}
```

# 第 18 章 继承

## 重写方法

回顾一下，当发送消息时，对该名称方法的搜索从对象的类开始，并沿着继承层次结构向上移动。找到的第一个实现将被执行。因此，你可以用自定义实现来*重写*继承的方法。例如，假设你决定员工的身体质量指数（BMI）始终为 19。在这种情况下，你可能会在 **Employee** 中重写 **bodyMassIndex** 方法。打开 *Employee.m* 并这样做：

```objectivec
#import "Employee.h"
@implementation Employee

@synthesize employeeID;

- (float)bodyMassIndex
{
    return 19.0;
}
@end
```

构建并运行程序，注意你的新 **bodyMassIndex** 实现被执行了——而不是来自 *Person* 的实现。

请注意，你在 *Employee.m* 中实现了 **bodyMassIndex**，但没有在 *Employee.h* 中声明它。在头文件中声明方法是为了宣传该方法，以便其他类的实例可以调用它。但是，由于 **Employee** 继承自 *Person*，每个人都知道 **Employee** 的实例都有 **bodyMassIndex** 方法。没有必要再次宣传它。

## super

如果你决定所有员工的 BMI 都能自动比 Person 实现中计算出的结果减少 10% 呢？当然，你可以在 Employee 实现中重新输入代码，但调用 Person 版本的 bodyMassIndex 并在返回前将结果乘以 0.9 会方便得多。为此，你使用 super 指令。在 Employee.m 中试一试：

```objectivec
#import "Employee.h"
@implementation Employee

@synthesize employeeID;

- (float)bodyMassIndex
{
    float normalBMI = [super bodyMassIndex];
    return normalBMI * 0.9;
}

@end
```

构建并运行程序。

精确地说，super 指令表示“运行这个方法，但从我的父类开始搜索其实现。”

## 挑战

此挑战基于上一章的挑战。

- 创建一个名为 ForeignStockHolding 的 StockHolding 子类。给 ForeignStockHolding 添加一个额外的实例变量：conversionRate，它将是一个 float。（汇率是你需要将当地价格乘以它才能得到美元价格。假设 purchasePrice 和 currentPrice 是当地货币。）重写 costInDollars 和 valueInDollars 以做正确的事。
- 在 main() 中，向数组中添加几个 ForeignStockHolding 的实例。

