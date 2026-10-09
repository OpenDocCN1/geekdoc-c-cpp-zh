
## 29. init

在 *NSObject* 类中，有一个名为 **init** 的方法。在对象被分配（allocated）之后，你需要向新实例发送 **init** 消息，以便它将实例变量初始化为可用的值。因此，**alloc** 负责为对象创建空间，而 **init** 则使对象准备好工作。使用 **init** 的样子如下：

```objective-c
NSMutableArray *things = [[NSMutableArray alloc] init];
```

请注意，**init** 是一个实例方法，它返回已初始化对象的地址。它是 *NSObject* 的 *初始化器*。本章将介绍如何编写初始化器。

### 编写 init 方法

创建一个新的项目：一个名为 Appliance 的 Foundation 命令行工具。在这个程序中，你将创建两个类：**Appliance** 和 **OwnedAppliance**（**Appliance** 的子类）。**Appliance** 的一个实例将具有 productName 和 voltage。**OwnedAppliance** 的一个实例还将包含一个集合，其中包含其所有者的姓名。

**图 29.1 Appliance 及其子类 OwnedAppliance**

![](img/5f9368899ebf8d92fc145f8def1e89f8_217_0.png)

创建一个新文件：一个名为 **Appliance** 的 **NSObject** 子类。在 **Appliance.h** 中，为 productName 和 voltage 创建实例变量和属性声明：

```objective-c
#import <Foundation/Foundation.h>

@interface Appliance : NSObject {
NSString *productName;
int voltage;
}

@property (copy) NSString *productName;
@property int voltage;

@end
```

（我们将在第 30 章讨论 copy 属性特性。）

在 Appliance.m 中，合成这些属性以创建实例变量的访问器方法：

```objective-c
#import "Appliance.h"

@implementation Appliance

@synthesize productName, voltage;
...
```

你可以这样创建 Appliance 的实例：

```objective-c
Appliance *a = [[Appliance alloc] init];
```

请注意，由于 Appliance 没有实现 init 方法，它将执行 NSObject 中定义的 init 方法。当这种情况发生时，Appliance 特有的所有实例变量都会被清零。因此，Appliance 新实例的 productName 将是 nil，而 voltage 将为零。

### 基本的 init 方法

在某些情况下，实例变量的初始值为零可能完全没问题。然而在其他情况下，你需要你的类的实例在“出生”时就将其实例变量初始化为非零值。

假设每个 Appliance 实例在开始其“生命”时，电压都应为 120。在 Appliance.m 中，通过添加 init 的新实现来覆盖 NSObject 的 init 方法。

```objective-c
- (id)init
{
    // 调用 NSObject 的 init 方法
    self = [super init];

    // 给 voltage 一个起始值
    voltage = 120;

    // 返回指向新对象的指针
    return self;
}
```

现在，当你创建一个 Appliance 的新实例时，它默认将具有 120 的电压。（注意，这不会改变关于访问器方法的任何内容。在实例初始化之后，可以像以前一样使用 setVoltage: 进行修改。）

请注意，你调用了超类的 init 方法，该方法初始化在超类中声明的实例变量，并返回指向已初始化对象的指针。大多数时候，这都能完美运行。然而，少数类的 init 方法行为异常。以下是两种可能的异常形式：

- **init** 方法可能会找到一个巧妙的优化方案，它可以执行该优化，释放原始对象，分配一个新对象，并返回该新对象。
- **init** 方法可能会失败，释放对象，并返回 `nil`。

为了处理第一种情况，Apple 要求你将 `self` 设置为指向超类 **init** 方法返回的对象。你在 **init** 方法的第一行做了这件事。

为了处理第二种情况，Apple 建议你检查超类的初始化器是否返回了一个有效对象，而不是 `nil`。毕竟，在一个不存在的对象上执行自定义设置是没有意义的。按照 Apple 的建议修改你的 **init** 方法：

```objective-c
- (id)init
{
    // 调用 NSObject 的 init 方法
    self = [super init];

    // 它是否返回了非 nil 的值？
    if (self) {
        // 给 voltage 一个起始值
        voltage = 120;
    }
    return self;
}
```

说实话，这种检查只在少数几个非常具体的情况下是必要的。因此，在实践中，许多 Objective-C 程序员通常会跳过这些额外的检查。然而，在这本书中，我们将始终执行这些检查，因为这是 Apple 认可的实现 **init** 方法的方式。

### 使用访问器

到目前为止，你有一个非常不错的 `Appliance` 的 **init** 方法，但我想向你展示一种在其他人的代码中常见的变体。我通常在 **init** 方法中执行简单的赋值，但许多程序员会使用访问器方法。修改你的 **init** 方法以执行此操作：

```objective-c
- (id)init
{
    // 调用 NSObject 的 init 方法
    self = [super init];

    // 它是否返回了非 nil 的值？
    if (self) {
        // 给 voltage 一个起始值
        [self setVoltage:120];
    }
    return self;
}
```

在大多数情况下，选择其中一种而不是另一种的理由很少，但这往往是一个很大的争论点。争论是这样的：使用赋值的人会说：“你不能在 **init** 方法中使用访问器方法！访问器假设对象已准备好工作，而在 **init** 方法完成*之后*对象才准备好工作。”然后使用访问器方法的人会说：“哦，拜托。在现实世界中，那

