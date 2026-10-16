
### 使用属性

Objective-C 的一个最新补充是属性的概念。属性允许你以声明方式为类的成员数据定义访问方法。它们消除了以前访问这些成员数据所需的大量样板代码。它们还使你作为类的开发者能够定义对象状态的契约。它们是 Objective-C 的一个重要语法补充。

#### 理解状态与行为之间的差异

在前面的章节中，我谈到对象是封装属性和行为的机制。在本节中，我将更深入地探讨这个主题，以便解释一些概念，这些概念可以帮助你在 Objective-C 中使用属性。

Objective-C 中属性的目的在于帮助你公开代表对象状态的对象属性。内部而言，属性编译为可用于获取和设置对象数据的实际方法。这些被称为访问器。你可以选择使用编译器生成的访问器，也可以选择覆盖编译器并自行生成。

> **NOTE:** 访问器是一种方法，其定义目的专门用于允许你的对象的使用者设置和获取对象中的值。它们封装了对象的成员数据并隐藏了对象的实现细节。访问器可以允许直接访问变量，也可以只是在访问时执行计算。有时这些方法被称为 `setters` 和 `getters`。大多数人使用属性而不是手动编写访问器，但在你想要覆盖属性访问器的正常行为的情况下，你可以轻松地覆盖访问器并提供自己的实现。我将在稍后关于属性的部分向你展示如何做到这一点。

对象由状态和行为组成。状态由构成对象的组成数据。思考对象状态时，大多数开发者遵循的一个良好的设计规则指出，虽然对象的状态可以随时更改，但一旦对象的状态被设置，就应认为它将保持该状态，直到由你的应用程序另行操作。还被认为是不好的做法是在仅仅修改对象状态时发生副作用。当你想让更改对象状态的行为产生外部副作用时，你应该仔细思考导致这种结果的设计决策。

另一方面，行为可以被视为对象采取行动。行为可用于更新其他对象，从而产生副作用，也可用于更改对象的内部数据或触发对象上的其他操作。

一些面向对象设计流派指出，对象应仅向外部实体公开行为。借助 Objective-C 2.0 属性记法，Objective-C 的设计者决定公开对象的内部状态也是可以接受的。属性记法使你能够在仍提供访问器通过其进行访问的同时公开对象的状态。同样，属性也应仅用于访问和操作对象的状态。明确地说，在编写属性时，你不应创建具有广泛外部后果的属性。这类事情应限制在对象的行为上。

举个例子，考虑一个代表引擎的类。这个引擎类可能会公开一个用于指定其油门的属性。用于指定油门设置的属性应仅设置油门值。如果你还想公开导致引擎根据油门值改变行为的行为，那么你应另外公开一个方法（一个行为），例如叫做 `updateEngineSpeedFromThrottle`。这个方法不带参数，并返回一个布尔值，表示是否成功根据油门值更新引擎速度。

通过分离类的状态和行为，你可以防止潜在的副作用以及行为与对象属性之间的依赖关系。

#### 使用属性声明对象状态

为了这个示例，我希望你想象自己正在编写一个人力资源应用程序。该应用程序将用于跟踪员工福利，包括薪水、保险等。因此，你需要创建一个 `Employee` 类来封装这些数据。

我相信你可以想象员工类需要封装哪些属性和属性。通常，这些包括员工的姓名、姓氏、社会安全号码、员工编号、薪水，以及可能指向其经理的另一个员工的引用。所有这些项目都可以表示为员工类的属性。

Listing 3.12 显示了你可能如何创建员工类接口的示例。它包括我刚刚指定的数据成员的列表以及用于访问每个数据成员的属性。在我们探讨每个属性时，应该有助于你理解属性的工作方式以及属性可以具有哪些属性。

##### Listing 3.12: 员工类接口

```
#import <Cocoa/Cocoa.h>

@interface Employee : NSObject
{
    NSString *firstName;
    NSString *lastName;
    NSDate *birthDate;
    NSDate *dateOfEmployment;
    Employee *manager;
    NSString *ssn;

    double salary;
}
@property (nonatomic, retain) NSString * firstName;
@property (nonatomic, retain) NSString * lastName;
@property (nonatomic, retain) NSDate * birthDate;
@property (nonatomic, retain) NSDate * dateOfEmployment;
@property (nonatomic, assign) Employee * manager;
@property (nonatomic, retain) NSString * ssn;
@property (nonatomic, readonly) NSTimeInterval age;
@property (nonatomic) double salary;

-(id)initWithFirstName:(NSString *)inFirstName lastName:(NSString *)inLastName birthDate:(NSDate *)inBirthDate ssn:(NSString *)inSsn;
-(id)init;
-(void)giveRaise:(double)percentage;
-(double)bonus;

@end
```

首先要注意的是，这里指定的几乎所有属性都有它们映射到的成员数据。属性声明由 `@property` 指令组成，后跟影响为此属性创建的访问器类型的属性。这些属性指定在 `@property` 指令后的括号内。给定属性可以指定的不同属性如表 3.1 所示。

##### Table 3.1: 属性属性

| Attribute | Purpose |
| --- | --- |
| `getter=<name>`, `setter=<name>` | 指定将用于此属性的访问器方法的名称。 |
| `readwrite` or `readonly` | 指定此属性是否可写入。默认值为 `readwrite`。 |
| `assign`, `retain`, or `copy` | 确定为此属性生成的 `setter` 的类型。`assign` 生成一个将变量简单赋值的 `setter`。`retain` 生成一个在将其分配给变量的同时保留传递给它的参数的 `setter`。`copy` 生成一个将传入值复制到成员变量的访问器。默认值为 `assign`。 |
| `nonatomic` | 指定生成的访问器为 `nonatomic`，因此不是线程安全的。默认值是 `atomic`，即线程安全。 |

在属性属性之后，你必须指定属性的数据类型。属性并不总是必须直接映射到成员数据变量，但在映射时，该成员数据的数据类型应与此处指定的属性数据类型匹配。最后，你必须指定属性的名称。可以指定一个与属性所代表的实际成员数据不同的名称的属性。大多数情况下，你不需要这样做。因此，此名称应与此属性映射到的成员数据的名称匹配。

与往常一样，在你的接口文件中声明的内容在你的实现文件中也有对应的声明。属性也不例外。要使用编译器生成的访问器方法，你的属性必须在实现文件中的实现块内有声明。实现文件中属性声明的可能类型要么是 `@synthesize` 声明，要么是 `@dynamic` 声明。`@synthesize` 指令导致编译器完全生成创建属性访问器所需的所有代码。基本上，此指令是使用属性的“免操作”方法。如果你使用 `@synthesize` 指令，则无需在实现文件中为属性编写任何额外代码。

另一方面，如果你想自己手工创建访问器，无论是在代码中还是稍后通过在运行时动态加载代码，都可以通过使用 `@dynamic` 指令来实现。使用 `@dynamic` 指令时，编译器将期望你已为属性创建了一对适当的访问器。

> **CAUTION:** 当你使用 `@dynamic` 指令创建自己的访问器时，请确保你的访问器满足你在属性属性中指定的契约。换句话说，如果你指定了 `copy` 属性，那么你必须确保在设置属性时你的访问器复制传入的值。

Listing 3.13 显示了我们的员工类实现。请注意，有不同属性以不同方式处理。

##### 上例 3.13：`Employee` 类实现

```objectivec
#import "Employee.h"

@implementation Employee
@synthesize firstName;
@synthesize lastName;
@synthesize birthDate;
@synthesize dateOfEmployment;
@synthesize manager;
@synthesize ssn;
@synthesize salary;
@dynamic age;

// parts removed to focus on properties...

-(NSTimeInterval)age;
{
    return [birthDate timeIntervalSinceNow];
}

@end
```

大多数已定义的属性都使用 `@synthesize` 指令。这意味着编译器完全负责为这些属性创建访问器。然而，员工类的某些属性是纯粹的计算属性。例如，员工的年龄可以使用员工的出生日期计算。正如你通过查看此代码所看到的那样，在这些特定情况下，属性已被指定为“只读”和“动态”。这意味着我们选择继续创建动态计算这些属性的方法，而不是将它们存储为数据成员。正如从代码中可以看到的那样，为此，我们实现了为我们执行计算的方法。

#### 理解合成属性访问器

当指定一个属性并允许编译器通过使用 `@synthesize` 指令生成合成访问器时，属性的属性会影响访问器的行为。编译器本身会根据这些属性生成不同的代码。

##### 使用 `nonatomic` 属性

作为属性声明的一部分，你可以指定的重要属性之一是属性访问器的原子性。属性的原子性与它在多线程环境中的行为有关。原子访问器确保其值在访问它的线程中完全设置或检索。因此，原子访问器被认为具有线程安全。基本上，原子访问器生成的代码看起来像上例 3.14 中的代码。

###### 上例 3.14：一个原子访问器

```objectivec
- (NSString *)firstName
{
    [threadLock lock];
    NSString *result = [[firstName retain] autorelease];
    [threadLock unlock];
    return result;
}
```

非原子的访问器不被认为具有线程安全。由 `@synthesize` 指令生成的 `nonatomic` 访问器可能看起来像上例 3.15。

###### 上例 3.15：一个 `nonatomic` 访问器

```objectivec
- (NSString *)firstName
{
    return [[firstName retain] autorelease];
}
```

你可以在确定将永远只有一个线程访问你的对象的应用程序中使用 `nonatomic` 访问器。

使用 `nonatomic` 访问器可能会带来轻微的性能提升，因为不需要像原子访问器那样锁定线程锁。

##### 使用 `assign`、`retain` 和 `copy` 属性

属性属性中有一组用于指定生成的 `setter` 语义的重要属性。这三个属性是互斥的，并定义了与此属性一起使用的 `setter` 的行为。

默认值 `assign` 指定值将简单地分配给数据成员。这种 `setter` 的示例显示在上例 3.16 中。

###### 上例 3.16：一个简单的 `assign` 风格 `setter`

```objectivec
- (void)setFirstName:(NSString *)inValue
{
    firstName = inValue;
}
```

此属性通常用于标量属性、委托和其他类型的变量，其中保留它们是不合适的。

本节中使用的一些语言与 Objective-C 内存管理有关，这是我在下一章中介绍的主题。你可能需要在阅读该章节后再次参考本节。

`retain` 属性仅在处理本身就是对象的数据成员时使用。它指定传递给 `setter` 的值将被分配给成员变量，并且会向其发送 `retain` 消息。

###### 上例 3.17：一个 `retain` 风格 `setter`

```objectivec
- (void)setFirstName:(NSString *)inValue
{
    [firstName autorelease];
    firstName = [inValue retain];
}
```

最后，`copy` 属性指定生成的 `setter` 应将对象复制到成员变量。与 `retain` 属性一样，这仅用于成员变量为对象的属性。从 `copy` 属性风格属性生成的访问器的示例显示在上例 3.18 中。

###### 上例 3.18：一个 `copy` 风格 `setter`

```objectivec
-(void)setFirstName:(NSString *)inValue
{
    [firstName autorelease];
    firstName = [inValue copy];
}
```

##### 使用不同数据成员名称的属性

通常，你的属性名称将与成员变量名称匹配。在处理遗留代码等情况下，可能不希望这样。在这些情况下，可以指定属性使用不同的访问器名称。一个示例显示在上例 3.19 中。

###### 上例 3.19：为属性指定访问器名称

```objectivec
@property (nonatomic, retain, getter=getFirstName) NSString *firstName;
```

> **NOTE**

>

> Objective-C 访问器通常采用 `variableName` 作为 `getter` 和 `setVariableName` 作为 `setter` 的形式。这是 Objective-C 的标准，有助于使你的对象符合 `Key-Value-Coding`。我们将在第 6 章中更详细地讨论这一点。

##### 使用点语法

在内部，属性编译为方法调用，在设置值的情况下为 `setter`，在获取值的情况下为 `getter`。使用 Objective-C 属性时，你可以直接使用传统方法调用使用这些 `setter` 和 `getter`，例如 `[object setFoo:bar]`，或使用一种特殊语法，称为点语法。上例 3.20 显示了同时使用传统访问器和点语法的示例。

###### 上例 3.20：使用传统访问器和点语法访问属性

```objectivec
{
    // traditional method call...
    [employee setFirstName:@"John"];

    // new Objective-C dot notation
    employee.firstName = @"John";
}
```

![](img/aaee977487e7a3eefe7b1dd596e0f6fb_119_0.png)

> **CAUTION**

>

> 点语法 ONLY 可用于为其定义了属性的值。

一些语言，如 C++、Python 和 Ruby，利用点语法对所有方法进行方法调用，而不仅仅是属性。如果你有这些语言的背景，你可能会想使用点语法来访问行为而不是状态。这被认为是非常糟糕的做法。

### 应用对象

现在我向你展示了面向对象编程的所有细节，我想带你逐步创建一个简单的应用程序，该应用程序将演示面向对象编程技术的使用。

我们要创建的应用程序是一个用于管理人力资源的应用程序。这是一个非常简单的应用程序。最终结果实际上并不是一个你可以使用的过程式应用程序，但创建它的过程将演示我迄今为止向你展示的所有面向对象编程技术。

首先，创建一个新的命令行 Foundation 项目。

#### 创建 `Employee` 类

此应用程序的目的是简单地存储员工及其经理的列表。此外，`Employee` 类将使你能够给予员工奖金和加薪并计算员工的年龄。

此外，还将有一种特殊的员工类型，即经理。经理员工将有向经理汇报的员工。员工将对其经理有引用，以便你可以访问员工的经理。创建完模板中的应用程序后，创建一个新类并将其命名为 `Employee`。编辑该类的接口以匹配上例 3.21。

##### 上例 3.21：`Employee` 类接口

```objectivec
//
//  Employee.h
//  HR
//
//
//  Created by Jiva DeVoe on 4/22/10.
//  Copyright 2010 __MyCompanyName__. All rights reserved.
//

#import <Cocoa/Cocoa.h>

@interface Employee : NSObject
{
    NSString *firstName;
    NSString *lastName;
    NSDate *birthDate;
    NSDate *dateOfEmployment;
    Employee *manager;
    NSString *ssn;

    double salary;
}

@property (nonatomic, retain) NSString * firstName;
@property (nonatomic, retain) NSString * lastName;
@property (nonatomic, retain) NSDate * birthDate;
```

##### Listing 3.21 (continued)
