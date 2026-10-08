
然后，当你想要显示姓名时，你通过 Driver 实例的 `firstName` 方法获取它：

```objective-c
- (NSString *)firstName;
```

`@end` 标志着 Driver 类声明的结束。

## 实现类

点击 `Driver.m` 文件以查看其代码。向该文件中添加以下代码：

```objective-c
@implementation Driver

- (int)go:(BOOL)distance {
    if (distance)
        return 10;
    else
        return 5;
}

- (NSString *)firstName {
    return firstName;
}

- (void)setFirstName:(NSString *)name {
    [name retain];
    [firstName release];
    firstName = name;
}

- (void)dealloc {
    [firstName release];
    [super dealloc];
}

@end
```

以下是该代码的工作方式：

- 该代码首先导入 `Driver.h` 接口，你的 Driver 类声明就在那里。
- 然后，代码定义该类的的方法。所有方法都位于 `@implementation` 和 `@end` 行之间。
- 正如你从头文件中知道的那样，这个类有三个方法。`go` 方法根据 `distance` 参数返回 5 或 10。

`firstName` 方法返回属于实例的 `firstName` 变量的值。
给同一类的变量和方法起相同的名字是完全合法的。

`Driver.m` 文件定义了 `setFirstName` 方法。
这里有点复杂。对于 Cocoa 的新手来说，你可能会认为可以像这样给 `firstName` 赋值：

```objective-c
firstName = name;
```

不幸的是，事情并不那么简单。因为 `name` 参数（它是 `setFirstName` 方法的一部分）指向一个 `NSString` 对象，所以必须小心清理内存。（“辞旧迎新。”）如果 `name` 的值与 `firstName` 的值不同，你必须释放 `firstName` 指针并保留 `name` 指针。这与 Objective-C 中的内存管理有关，正如我在本章前面所描述的那样。

因为 `firstName` 和 `setFirstName` 方法允许你访问 Driver 类的 `firstName` 变量，程序员将这些方法称为访问器方法。当你想要访问类内部的变量时，最好提供访问器方法，而不是让用户在你的类内部随意翻找。

`Driver.m` 文件中的最后一个方法是 `dealloc` 方法，它负责释放 `firstName` 指针并解除分配父类。

```objective-c
[firstName release];
[super dealloc];
```

## 使用类

既然你已经定义了一个 Driver 类，你可能想知道如何使用它。

在 Xcode 中点击 `MyController.m` 文件，并将代码更改为以下列表中的样子：

```objective-c
#import "MyController.h"
#import "Driver.h"

@implementation MyController

- (IBAction)calculateFare: (id)sender {
    NSString *name = @"Frederick";
    Driver *driver = [[Driver alloc] init];
    
    int fare;

    [driver setFirstName:name];
    [driver setIntegerValue:[driver firstName]];

    fare = [driver go:[distanceCheckbox state]];
    [fareDisplay setIntValue:fare];

    [driver release];
}

@end
```

以下是该代码的工作方式：

- 它声明并给一个 `NSString` 赋值。你的出租车公司很小；它只有一名司机，Frederick：

  ```objective-c
  NSString *name = @"Frederick";
  ```

  在 C 中处理字符串可能会很麻烦。为了解决这个问题，Objective-C 提供了一个方便的方法来分配字面量。只需将 `@` 字符放在字符串前面即可。`@` 字符标志着 Objective-C 中字符串字面量的开始。

- 该代码使用 `alloc` 和 `init` 方法创建一个 driver 对象：

  ```objective-c
  Driver *driver = [[Driver alloc] init];
  
  // code here
  
  [driver release];
  ```

  当你使用 `alloc` 和 `init` 方法创建对象时，务必在使用完它们之后释放它们。如果不这样做，就会泄漏内存。

  注意对象名称（`driver`）是小写拼写，而类（`Driver`）是大写拼写。请参阅“Objective-C 中的命名”侧边栏以了解如何做到这一点。

- 创建 driver 对象后，你可以开始使用它的方法。代码给 driver 对象分配一个名字：

  ```objective-c
  [driver setFirstName:name];
  ```

- 你使用 `go` 方法计算车费：

  ```objective-c
  fare = [driver go:[distanceCheckbox state]];
  [fareDisplay setIntValue:fare];
  ```

- 代码传递第二个参数，基于 `distanceCheckbox` 的当前状态。`go` 方法返回你传递给它的参数的值，你可以使用 `fareDisplay` 出口在界面中显示它。

![](img/ea40cad434a338535474e82c1a6ace20_148_0.png)

## 测试

按 Command+R 测试你的作品。你会看到类似图 6-8 的内容。

![](img/ea40cad434a338535474e82c1a6ace20_149_0.png)

当用户点击界面中的按钮时，`MyViewController` 类的 `calculateFare` 方法创建 driver 对象，使用它的方法，并释放它。因此，每次用户点击按钮时，代码都会创建一个新对象，处理它，并释放它。

## Objective-C 中的命名

大多数编程语言都有命名约定，Objective-C 也不例外。虽然这些所谓的规则并非强制要求，但它们具有以下好处：

- 提高代码质量。
- 提供关于代码功能的提示。
- 使你的代码能很好地与键值编码（KVC）和绑定配合使用（第 18 章）。
- 使其他人更容易解读你的代码。

| 类名 | 内置名称 |
| :--- | :--- |
| Objective-C 中的类名以大写字母开头。使用本章前面介绍的类，`Driver` 是类的大写名称。 | `NSString` |
| 这些类中的每一个都以大写字母开头。此外，它们以相同的大写字母 N 和 S 开头。这些类之所以采用这种命名系统，是因为它们是 NEXTSTEP 操作系统的遗留产物，Apple 基于此开发了 Mac OS X。通过这个小小的命名约定，你可以立即分辨出代码中的哪些类是你自己的，哪些来自 Cocoa 框架。 | `NSNumber` |
| Xcode 和 Interface Builder 试图帮助你记住将类名大写。每次你用这两个应用程序中的任何一个创建新类时，它们都会提供一个默认的大写类名。 | `NSArray` |
| 当你使用小写名称表示你的实例时，很容易区分实例和类。当类和实例名称相同时，这特别有用。 | `NSImage` |

**实例名称：** 与类名相反，实例以小写字母开头。例如，在本章早些时候，你像这样创建了一个 Driver 类的实例：

```objective-c
Driver *driver = [[Driver alloc] init];
```

实例的名称是 `driver`。你同样创建了一个 `NSString` 的实例：

**文件名：** Cocoa 源代码文件必须遵循规定的命名方案。你已经见证了 Objective-C 类由两个文件组成。例如，`Driver` 类有以下两个文件：

- `Driver.m`：实现文件
- `Driver.h`：接口（或头）文件

# 第 7 章

# MVC 设计

## 本章内容

- 熟悉模型-视图-控制器（MVC）设计模式
- 使用 MVC 构建项目
- 添加视图和控制器

在第 6 章中，你查看了使用 Cocoa 进行面向对象编程的一些基础知识。你研究了如何定义类以及如何用该类创建对象。在此过程中，我承诺这会使编程更简单，更重要的是，更可重用。

当然，你可以整天制作类和对象，但它们实际上是如何组合在一起制作应用程序的？本章将面向对象编程提升到下一个水平，并在抽象层面上展示如何使用所有这些类来设计应用程序。深思熟虑的 Cocoa 程序员不会把一堆类扔在一起，然后指望在另一边得到杰作。相反，Cocoa 程序员会思考应用程序的各个部分如何工作，然后使用著名的模型-视图-控制器（MVC）设计模式来设计应用程序。

![](img/ea40cad434a338535474e82c1a6ace20_152_0.png)

通过遵循这种设计模式，你可以构建模块化的应用程序，更容易阅读，并且包含可以在其他应用程序中重用的组件。面向对象编程的一大好处是能够重用代码。通过重用代码，你可以减少编程所需花费的时间，减少代码中的 bug 数量，并最终创建更好的软件。然而，当谈到代码重用时，情况并不总是那么美好。你必须严格调试你的代码并维护单一版本。如果不这样做，你可能会注入一个 bug，该 bug 会在你使用代码的所有应用程序中传播。

