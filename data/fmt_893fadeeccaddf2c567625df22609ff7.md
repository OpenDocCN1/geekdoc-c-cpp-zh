
然而，如果你将这些对象放入集合中，可能会导致性能问题，因为哈希值被用作集合所使用的哈希表中的索引。集合的实现可能会使用哈希将对象分桶到不同的数组中。当一个对象被添加到集合时，会枚举与其哈希值对应的数组，以检查该数组中的对象是否相等。如果该对象已经在集合中。因此，如果你为每个对象返回相同的哈希值，并向集合中添加了 1,000,000 个对象，那么向集合的后续每次添加都必须扫描这 1,000,000 个对象中的每一个。

哈希方法的另一种实现可能是：

```objc
(NSUInteger)hash {
    NSString *stringHash = [NSString stringWithFormat:@"%@:%@:%i", _firstName, _lastName, _age];
    return [stringHash hash];
}
```

这一次，`NSString` 的 `hash` 方法算法是通过创建一个字符串并返回该字符串的哈希值来实现的。这样做符合约定，因为两个相等的 `ECOPerson` 对象将始终返回相同的哈希值。然而，这种方法的缺点是它比返回单个值慢得多，因为你有创建字符串的开销。在将对象添加到集合时，这会再次引起性能问题，因为必须为要添加到集合的对象计算哈希值。

第三也是最后一种方法是创建如下所示哈希：

```objc
(NSUInteger)hash {
    NSUInteger firstNameHash = [_firstName];
    NSUInteger lastNameHash = [_lastName];
    NSUInteger ageHash = _age;
    return firstNameHash ^ lastNameHash ^ ageHash;
}
```

### 项目 8：理解对象相等性

这种方法在效率和创建一定范围哈希值之间是一个折中方案。当然，使用此算法创建的哈希会发生冲突，但至少可以返回多个值。冲突频率与计算密集型哈希方法之间的权衡是你应该实验并观察哪种方法适用于你的对象。

### 类特定的相等性方法

除了前面提到的 `NSString` 之外，提供特定相等方法的类还包括 `NSArray:(isEqualToArray:)` 和 `NSDictionary:(isEqualToDictionary:)`，如果被比较的对象不是数组或字典，这两个方法都将抛出异常。Objective-C 在编译时没有强类型检查，因此你很容易无意中传递一个错误类型的对象。因此，你需要确保你传递的对象确实是正确的类型。

如果相等性可能会被频繁检查，你可能决定创建自己的相等性方法；因此，由于不需要检查类型而带来的额外速度是显著的。提供特定方法的另一个原因纯粹是为了视觉效果，如果你认为它看起来更好且更具可读性，这可能是 `NSString` `EqualTo:` 方法的动机之一。使用该方法的代码更易读，因为你不需要寻找两个被比较对象的类型。

如果你创建了一个特定方法，那么你也应该重写 `isEqual:` 方法，如果被比较对象的类与接收者的类相同，则通过该方法进行传递。如果不是，将其传递给父类实现是常见的做法。例如，`EOCPerson` 类可以实现以下内容：

```objc
(BOOL)isEqualTo:(EOCPerson*)otherPerson {
    if (self == object) return YES;

    if (_firstName isEqualToString:otherPerson.firstName)
        return NO;
    if (_lastName isEqualToString:otherPerson.lastName)
        return NO;
    if (_age != otherPerson.age)
        return NO;
    return YES;
}
```

## 第 2 章：对象、消息、运行时

```objc
(BOOL)isEqualTo:(EOCPerson*)otherPerson {
    if (self == object) return YES;

    if (_firstName isEqualToString:otherPerson.firstName)
        return NO;
    if (_lastName isEqualToString:otherPerson.lastName)
        return NO;
    if (_age != otherPerson.age)
        return NO;
    return YES;
}
```

## 第 9 项：使用类簇模式隐藏实现细节

```objc
- (void)drawRect:(CGRect)rect {
  if (_type == TypeA) {
    // 绘制 TypeA 按钮
  } else if (_type == TypeB) {
    // 绘制 TypeB 按钮
  }
} /* ... */
```

然而，如果许多方法都需要根据类型进行切换，这种做法就显而易见。此时，一个优秀的程序员可能会进行重构，使其拥有多个子类来处理每个按钮类型所需的专门工作。这样做需要用户了解所有不同的子类。这正是类簇（Class Cluster）模式大显身场的地方，它通过在抽象基类之后隐藏多个子类提供了灵活性，同时保持了接口的简洁。你不需要创建子类的实例；让基类为你创建它们即可。

### 创建类簇

作为一个创建类簇的示例，考虑一个处理员工的类，所有员工都有名字和薪水，并且可以被指示完成一天的工作。然而，当每位员工完成一天的工作时，不同类型的员工的情况是不同的。雇这些员工的业务经理并不关心每个人执行工作时的具体情况，只需告诉员工们去执行即可。

首先，你需要定义抽象基类：

```objc
typedef NS_ENUM(NSInteger, EOCEmployeeType) {
  EOCEmployeeTypeDeveloper,
  EOCEmployeeTypeDesigner,
  EOCEmployeeTypeFinance,
};

@interface EOCEmployee : NSObject

@property (copy) NSString *name;
@property NSInteger salary;

// 创建 Employee 对象的辅助方法
+ (EOCEmployee*)employeeWithType:(EOCEmployeeType)type;

// 让员工完成各自当天的工作
- (void)doDaysWork;

@end
```

```objc
@implementation EOCEmployee

+ (EOCEmployee*)employeeWithType:(EOCEmployeeType)type {

    switch (type) {

        case EOCEmployeeTypeDeveloper:

            return [EOCEmployeeDeveloper new];

            break;

        case EOCEmployeeTypeDesigner:

            return [EOCEmployeeDesigner new];

            break;

        case EOCEmployeeTypeFinance:

            return [EOCEmployeeFinance new];

            break;

    }

}

- (void)doDaysWork {

    // 由子类实现。

}

@end
```

每个具体的子类都继承自基类。例如：

```objc
@interface EOCEmployeeDeveloper : EOCEmployee

@end
```

```objc
@implementation EOCEmployeeDeveloper

- (void)doDaysWork {
    [self writeCode];
}

@end
```

在这个示例中，基类实现了一个声明为类方法的方法，该方法根据正在创建的员工类型进行切换，并分配所需类的一个实例。这种工厂模式（Factory pattern）是创建类簇的一种方式。

遗憾的是，Objective-C 并没有提供语言特性来指定基类是抽象的。相反，应该在文档中规定如何使用该类的约定。在这种情况下，接口中没有定义 `init` 系列方法，这表明可能不应该直接创建其实实例。另一种确保不使用基类实例的方法是在基类的 `doDaysWork` 中抛出异常。然而，这是相当极端的，而且通常没有必要。

在内省（introspection）期间使用作为类簇成员的对象时，需要小心（见第 14 项）。这是因为，尽管你认为自己创建了一个类的实例，但实际上你创建的是子类的实例。在员工的示例中，你可能认为调用 `[employeeMemberOfClass: [Employee class]]` 会返回 `YES`，但返回的实际上并不是 `Employee`，所以此调用将返回 `NO`。

### Cocoa 中的类簇

系统框架中有许多类簇。大多数集合类都是类簇。

### 第 2 章：对象、消息与运行时

```objc
void objc_removeAssociatedObjects(id object)
```

移除对象上所有的关联对象。

访问关联对象在功能上类似于想象该对象是一个 `NSDictionary` 并调用 `[object setObject:value forKey:key]` 和 `[object objectForKey:key]`。不过，一个需要注意的重要区别是，键（key）被纯视为一个不透明指针。在字典中，如果两个键通过 `isEqual` 比较则被视为相等；而关联对象的键必须是完全相同的指针才能匹配。出于这个原因，通常使用静态全局变量作为键。

## 使用关联对象的示例

在 iOS 开发中，使用 `UIAlert` 类非常常见，它提供了一个向用户显示警框的标准视图。它有一个代理协议（delegate protocol）来处理用户点击按钮关闭警框的情况；然而，使用委托模式（delegation）会将创建警框和处理任务的代码拆分开。这使得阅读起来稍微别扭，因为代码分散在两个地方。以下是正常使用 `UIAlertView` 的示例：

```objc
(void)askUserAQuestion {
    UIAlert *alert = [[UIAlert alloc] 
        initWithTitle:@"Question"
        message:@"what do you want to do?"
        delegate:self
        cancelButtonTitle:@"Cancel"
        otherButtonTitles:@"Continue", nil];

    [alert show];
}
```

```objc
// UIAlertDelegate 协议方法
-(void)alertView:(UIAlert *)alertView cancelButton:(NSInteger)buttonIndex {
    if (buttonIndex == 0) {
        [self doCancel];
    } else {
        [self doContinue];
    }
}
```

如果你想在同一个类中展示多个警框，这种模式会变得更加复杂，因为你必须检查传递给代理方法的警框并根据此进行切换。如果每个按钮被点击时的处理逻辑在警框创建时时就决定了，将会简单得多。这正是可以使用关联对象的地方。一种解决方案是在创建警框时为它设置一个 block，然后读取该 block。实现起来如下所示：

## 项目 10：使用关联对象为现有类附加自定义数据

```objc
#import <objc/runtime.h>

static void *const MyViewControllerKey = "MyViewControllerKey";

(void)askUserAQuestion {
    UIAlert *alert = [[UIAlert alloc] 
        initWithTitle:@"Question"
        message:@"what do you want to do?"
        delegate:self
        cancelButtonTitle:@"Cancel"
        otherButtonTitles:@"Continue", nil];

    void (^block)(NSInteger) = ^(NSInteger buttonIndex) {
        if (buttonIndex == 0) {
            [self doCancel];
        } else {
            [self doContinue];
        };
    objc_setAssociatedObject(alert, MyViewControllerKey, block, OBJC_ASSOCIATION_COPY);

    [alert show];
}

// UIAlertDelegate 协议方法
-(void)alertView:(UIAlert *)alert cancelButton:(NSInteger)buttonIndex {
    void (^block)(NSInteger) = objc_getAssociatedObject(alert, MyViewControllerKey);
    block(buttonIndex);
}
```

通过这种方法，创建警框和处理结果的代码都在同一个地方，使其比以前更具读性，因为你不需要在两部分代码之间来切换来理解为什么要使用该警框。然而，你需要对这种方法非常小心，因为很容易引入循环引用（retain cycles）。如果警框被使用多次，我建议使用这种方法而非关联对象。

## 注意事项

- 关联对象提供了将两个对象链接在一起的手段。
- 关联对象的内存管理语义可以定义，以模拟拥有或非拥有的关系。
- 只有在无法使用其他方法时才使用关联对象，因为它们很容易引入难以发现的 bug。

## 项目 11：理解 objcmsgSend 的作用

在 Objective-C 中你最常用的操作之一就是调用对象。在 Objective-C 术语中，这被称为传递消息（passing a message）。消息有名称、选择器（selectors）、参数，并可能返回值。

由于 Objective-C 是 C 语言的超集，最好先开始理解在 C 中调用函数被称为静态绑定（static binding），这意味着被调用的函数在编译时是已知的。例如，考虑以下代码：

```objc
#import <stdio.h>

void printHello() {
    printf("Hello, world!\n");
}
```

```objc
void printGoodbye() {
    printf("Goodbye, world!\n");
}

void doTheThing(int type) {
    if (type == 0) {
        printHello();
    } else {
        printGoodbye();
    }
    return 0;
}
```

忽略内联（inlining），当这些被编译时，`printHello` 和 `printGoodbye` 是已知的，编译器发出直接调用函数的指令。函数的地址实际上被硬编码在指令中。现在考虑一下如果它写成这样：

```objc
#import <stdio.h>

void printHello() {
    printf("Hello, world!\n");
}
void printGoodbye() {
    printf("Goodbye, world!\n");
}
```

```objc
void doTheThing(int type) {
    void (*fnc)();
    if (type == 0) {
        fnc = printHello;
    } else {
        fnc = printGoodbye;
    }
    fnc();
    return 0;
}
```

在这里，使用了动态绑定（dynamic binding），因为被调用的函数在运行时是未知的。编译器发射的指令的区别在于，在第一个例子中，`if` 和 `else` 语句内部都进行了函数调用；而在第二个例子中，只进行了一次函数调用，代价是必须读取要调用函数的地址。
