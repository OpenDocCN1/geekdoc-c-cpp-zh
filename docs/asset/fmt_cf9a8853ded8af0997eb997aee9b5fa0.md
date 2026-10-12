
## 保留计数规则

有一套内存管理惯例，所有 `Objective-C` 程序员都遵循这些惯例。如果你在使用 ARC（自动引用计数），它在幕后会自动为你遵循这些惯例。

在这些规则中，我使用“你”这个词来指代“你当前正在处理的某个类的实例”。这是一种很有用的共情方式：你想象自己就是那个正在编写的对象。因此，例如，“如果你保留（retain）了这个字符串，它就不会被释放。” 实际上是指“如果你当前正在工作的类的实例保留了这个字符串，它就不会被释放。”

以下是这些规则。（实现细节在括号中说明。）

- 如果你使用以 `alloc` 或 `new` 开头，或者包含 `copy` 的方法创建一个对象，那么你就拥有了它的所有权。（也就是说，假设新对象的保留计数为 1，并且 *不* 在自动释放池中。）你有责任在不再需要该对象时释放它。以下是一些常见的传递所有权的方法：`alloc`（后面总是跟随一个 `init` 方法）、`copy` 和 `mutableCopy`。
- 通过 *任何* 其他方式创建的对象都 *不* 属于你所有。（也就是说，假设它的保留计数为 1，并且已经在自动释放池中，因此，如果在自动释放池排空之前没有保留它，它注定会被释放。）
- 如果你不拥有一个对象，但希望确保其持续存在，请通过发送 `retain` 消息来获取所有权。（这会增加对象的保留计数。）
- 当你拥有一个对象且不再需要它时，请发送 `release` 或 `autorelease` 消息。（`release` 会立即减少保留计数。`autorelease` 会在自动释放池排空时发送 `release` 消息。）
- 只要一个对象至少有一个所有者，它就会继续存在。（当它的保留计数变为零时，它会收到 `dealloc` 消息。）

理解内存管理的一个技巧是局部思考。`Asset` 类不需要知道其他同样关心其 `label` 的对象。只要 `Asset` 实例保留（retain）了它想要保留的对象，你就不会遇到任何问题。刚接触这门语言的程序员有时会犯试图跟踪整个应用程序中所有对象的状态的错误。不要这样做。如果你遵循这些规则，并始终对类进行局部思考，你就不必担心应用程序的其他部分正在如何使用某个对象。

根据所有权这一概念，现在你明白了为什么需要在你的 `description` 方法中自动释放（autorelease）字符串：员工对象创建了该字符串，但它并不想拥有它。它想把它送出去。

## 21 集合类

你 already 使用过两个集合类：`NSArray` 及其子类 `NSMutableArray`。你知道，数组保存的是指向其他对象的指针的集合。这些指针是有序的，因此你使用索引（整数）来访问集合中的对象。在本章中，我们将更深入地探讨数组，并查看一些其他的集合类：`NSSet`/`NSMutableSet` 和 `NSDictionary`/`NSMutableDictionary`。

### NSArray/NSMutableArray

当你向数组中添加一个对象时，数组会声称拥有它。当你从数组中移除该对象时，数组会放弃对其的所有权。打开 `BMITime`，看看你是如何使用员工数组的。如果我们忽略其他所有内容，你会看到类似这样的代码：

```objectivec

// Create an array of Employee objects

NSMutableArray *employees = [[NSMutableArray alloc] init];

for (int i = 0; i < 10; i++) {

    // Create an instance of Employee

    Employee *person = [[Employee alloc] init];

    // Put the employee in the employees array

    [employees addObject:person];

}

[employees removeObjectAtIndex:5];

employees = nil;

```

你通常使用 `alloc/init` 或类方法 `array` 创建一个空的可变数组。例如，你可以这样创建可变数组：

```objectivec

NSMutableArray *employees = [NSMutableArray array];

```

请注意，`addObject:` 方法将对象添加到列表的末尾。随着对象被添加，数组会增长到足以容纳它们的大小。

### 不可变对象

当你创建 `NSArray` 的实例时，你必须在创建时为其分配所有对象。这通常看起来像这样：

```objectivec

NSArray *colors = [NSArray arrayWithObjects:@"Orange", @"Yellow", @"Green", nil];

```

末尾的 nil 是你告诉方法停止的方式。因此，这个 colors 数组将只包含三个字符串。（如果你忘记了 nil，你的程序很可能会崩溃。）

大多数初学程序员会对 *NSArray* 的存在感到惊讶。为什么有人想要一个不能被修改的列表呢？有两个原因：

- 你不信任与你共事的人。也就是说，你希望让他们查看数组，但不希望他们能够修改它。一种更温和的方法是给他们一个 *NSMutableArray*，但*告诉*他们这是一个 *NSArray*。例如，想象一下以下方法：

```objectivec

// Returns an array of 30 odd numbers

- (NSArray *)odds

{

    static NSMutableArray *odds = [[NSMutableArray alloc] init];

    int i = 1;

    while ([odds count] < 30) {

        [odds addObject:[NSNumber numberWithInt:i]];

        i += 2;

    }

    return odds;

}

```

调用此方法的任何人都会假设它返回的是一个不可变的 *NSArray*。如果调用者试图添加或移除返回对象中的项目，编译器将发出严厉警告——尽管，事实上，它是 *NSMutableArray* 的一个实例。

- 另一个原因是性能：不可变对象永远不需要被复制。对于可变对象，你可能会创建一个私有副本，以确保系统中没有其他代码能在你不知情的情况下修改它。对于不可变对象，这是不必要的。实际上，*NSMutableArray* 的 *copy* 方法会制作一个新的副本并返回指向新数组的指针，而 *NSArray* 的 *copy* 方法什么也不做——它只是返回指向自身的指针。

因此，不可变对象在 Objective-C 编程中相当常见。在 Foundation 框架中，有许多类创建不可变实例：*NSArray*、*NSString*、*NSAttributedString*、*NSData*、*NSCharacterSet*、*NSDictionary*、*NSSet*、*NSIndexSet* 和 *NSURLRequest*。所有这些类都有可变子类：*NSMutableArray*、*NSMutableString*、*NSMutableAttributedString* 等。*NSDate* 和 *NSNumber* 则是不可变的，但没有可变子类。

### 排序

排序数组有几种方法，但最常见的方式是使用 *排序描述符* 数组。*NSMutableArray* 具有如下方法：

```objectivec

- (void)sortUsingDescriptors: (NSArray *)sortDescriptors;

```

参数是一个 *NSSortDescriptor* 对象的数组。排序描述符包含数组中对象属性的名称，以及该属性应按升序还是降序排序。为什么我们要传递一个排序描述符数组呢？想象一下，你说：“按姓氏升序对这个医生列表进行排序。” 如果两位医生姓氏相同怎么办？你可以指定“按姓氏升序排序，如果姓氏相同，则按名字升序排序，如果名字和姓氏都相同，则按邮政编码排序。”

#### 图 21.1 按 lastName 排序，然后按 firstName，最后按 zipCode

![](img/5f9368899ebf8d92fc145f8def1e89f8_147_0.png)

用于排序的属性可以是对象中的任意实例变量或任意方法的结果。

让我们回到 BMITime 项目，看看排序在实际中的应用。在 **main()** 中，在记录员工数组之前，按 **valueOfAssets** 对其进行排序。如果两名员工持有的资产价值相同，则按 employeeID 排序。编辑 main.m：

```objectivec

    }

    NSSortDescriptor *vao = [NSSortDescriptor sortDescriptorWithKey:@"valueOfAssets"

                                                        ascending:YES];

    NSSortDescriptor *ei = [NSSortDescriptor sortDescriptorWithKey:@"employeeID"

                                                        ascending:YES];

    [employees sortUsingDescriptors:[NSArray arrayWithObjects:vao, ei, nil]];

    NSLog(@"Employees: %@", employees);

```

编译并运行程序。你应该看到员工列表正确排序：

```text

Employees: (

    "<Employee 0: $0 in assets>",

    "<Employee 4: $0 in assets>",

    "<Employee 8: $0 in assets>",

    "<Employee 7: $34 in assets>",

    "<Employee 3: $68 in assets>",

    "<Employee 2: $119 in assets>",

    "<Employee 6: $119 in assets>",

    "<Employee 5: $136 in assets>",

    "<Employee 9: $136 in assets>",

    "<Employee 1: $153 in assets>"

)

```

### 过滤

有一个名为 **NSPredicate** 的类。*谓词*（predicate）包含一个可能为真的语句，例如“employeeID 大于 75”。**NSMutableArray** 有一个方便的方法，用于丢弃所有不满足谓词的对象：

```objectivec

- (void)filterUsingPredicate: (NSPredicate *)predicate;

```

**NSArray** 有一个方法，用于创建一个包含所有满足谓词的对象的**新**数组：

```objectivec

- (NSArray *)filteredArrayUsingPredicate: (NSPredicate *)predicate;

```

假设你打算收回目前持有资产总值超过 $70 的员工的所有资产。在 **main.m** 的末尾附近添加代码：

#### 第 21 章 集合类

```objectivec

[employees removeObjectAtIndex:5];

NSLog(@"allAssets: %@", allAssets);

NSPredicate *predicate = [NSPredicate predicateWithFormat:

                         @"holder.valueOfAssets > 70"];

NSArray *toBeReclaimed = [allAssets filteredArrayUsingPredicate:predicate];

NSLog(@"toBeReclaimed: %@", toBeReclaimed);

toBeReclaimed = nil;

NSLog(@"Giving up ownership of arrays");

allAssets = nil;

employees = nil;

}

return 0;

}

```

构建并运行该程序。你应该能看到一个资产列表：

```text

toBeReclaimed: (

  "<Laptop 1: $17, assigned to <Employee 6: $119 in assets>>",

  "<Laptop 3: $51, assigned to <Employee 5: $136 in assets>>",

  "<Laptop 5: $85, assigned to <Employee 5: $136 in assets>>",

  "<Laptop 6: $102, assigned to <Employee 6: $119 in assets>>",

  "<Laptop 8: $136, assigned to <Employee 9: $136 in assets>>",

  "<Laptop 9: $153, assigned to <Employee 1: $153 in assets>>"

)

```

用于创建谓词的格式字符串可以非常复杂。如果你经常对集合进行过滤，务必阅读 *Apple 的谓词编程指南*。

### NSSet/NSMutableSet

集合是一种没有顺序概念的收集，且特定对象在集合中只能出现一次。集合主要用于回答“它在那里吗？”这类问题。例如，你可能拥有一个包含不适合儿童内容的 URL 集合。在将任何网页展示给孩子之前，你可能想快速检查一下该 URL 是否在集合中。集合可以极其快速地做到这一点。

员工的资产没有固有的顺序，且同一员工的资产集合中，某项资产绝不应出现两次。请修改你的程序，在资产关系中使用 `NSMutableSet` 而不是 `NSMutableArray`。

![](img/5f9368899ebf8d92fc145f8def1e89f8_149_0.png)

在 Employee.h 中，修改变量的声明：

```objectivec

#import "Person.h"

@class Asset;

@interface Employee : Person

{

    int employeeID;

    NSMutableSet *assets;

}

@property int employeeID;

- (void)addAssetsObject:(Asset *)a;

- (unsigned int)valueOfAssets;

@end

```

在 Employee.m 中，创建正确类的实例：

```objectivec

- (void)addAssetsObject:(Asset *)a

{

    if (!assets) {

        assets = [NSMutableSet alloc] init];

    }

    [assets addObject:a];

    [a setHolder:self];

}

```

构建并运行该程序。它应该像之前一样工作。

你无法通过索引访问集合中的对象，因为集合没有顺序概念。相反，你只能询问“里面有这种对象吗？” **NSMutableSet** 拥有一个方法：

```objectivec

- (BOOL)containsObject:(id)x;

```

当你向集合发送此消息时，它会遍历其对象集合，寻找一个与 x 相等的对象。如果找到了，它返回 **YES**；否则返回 **NO**。

这就引出了一个相当深入的问题：*相等* 意味着什么？`NSObject` 类定义了一个名为 `isEqual:` 的方法。要检查两个对象是否相等，请使用 `isEqual:` 方法：

```objectivec

if ([myDoctor isEqual:yourTennisPartner]) {

    NSLog(@"my doctor is equal to your tennis partner");

}

```

`NSObject` 对 `isEqual:` 有一个简单的实现。它看起来像这样：

```objectivec

- (BOOL)isEqual: (id)other

{

    return (self == other);

}

```

因此，如果你没有重写 `isEqual:`，上面的代码片段等同于：

```objectivec

if (myDoctor == yourTennisPartner) {

    NSLog(@"my doctor is equal to your tennis partner");

}

```

某些类重写了 `isEqual:`。例如，在 `NSString` 中，`isEqual:` 被重写为比较字符串中的字符。对于这些类，*相等* 和 *同一* 之间是有区别的。假设我有两个指向字符串的指针：

```objectivec

NSString *x = ...;

NSString *y = ...;

```

如果 x 和 y 包含完全相同的地址，那么它们是 *同一* 的。如果 x 和 y 指向的字符串包含相同字母且顺序相同，那么它们是 *相等* 的。

因此，同一的对象总是相等的。相等的对象并不总是同一的。

这个区别重要吗？是的。例如，`NSMutableArray` 有两个方法：

```objectivec

- (NSUInteger)indexOfObject: (id)anObject;
```
