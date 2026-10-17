
```objc
return [NSString stringWithFormat:@"<%@: $%d, assigned to %@>",

       [self label], [self resaleValue], [self holder]];

} else {

    return [NSString stringWithFormat:@"<%@: $%d, unassigned>",

           [self label], [self resaleValue]];

}

}

- (void)dealloc

{

    NSLog(@"deallocating %@", self);

}

@end
```

这带来了一个风格问题：当人们一起使用 `Asset` 类和 `Employee` 类时，我们如何确保这两种关系是一致的？也就是说，当且仅当员工是资产的持有者时，资产才应该出现在员工的资产数组中。有三种选择：

- 显式设置两种关系：
  ```objc
  [vicePresident addAssetsObject:townCar];
  [townCar setHolder:vicePresident];
  ```
- 在设置子对象指针的方法中，将子对象添加到父对象的集合中。
  ```objc
  - (void)setHolder:(Employee *)e
  {
      holder = e;
      [e addAssetsObject:self];
  }
  ```
  这种方法并不常见。
- 在将子对象添加到父对象集合的方法中，设置子对象的指针。

在这个练习中，你将采用最后一种选择。在 *Employee.m* 中，扩展 `addAssetsObject:` 方法，同时也设置 `holder`。

## 循环引用

```objc
- (void)addAssetsObject:(Asset *)a
{
    // Is assets nil?
    if (!assets) {
        // Create the array
        assets = [NSMutableArray alloc] init];
    }
    [assets addObject:a];
    [a setHolder:self];
}
```

（我最喜欢的一个 Bug 之一：让两个访问器互相自动调用。这会创建一个无限循环：**addAssetsObject**: 调用 **setHolder**:，而 **setHolder**: 又调用 **addAssetsObject**:，如此往复...）

构建并运行程序。你应该会看到类似这样的输出：

Employees: (
"<Employee 0: $0 in assets>",
"<Employee 1: $153 in assets>",
"<Employee 2: $119 in assets>",
"<Employee 3: $68 in assets>",
"<Employee 4: $0 in assets>",
"<Employee 5: $136 in assets>",
"<Employee 6: $119 in assets>",
"<Employee 7: $34 in assets>",
"<Employee 8: $0 in assets>",
"<Employee 9: $136 in assets>"
)
Giving up ownership of one employee
Giving up ownership of array
deallocating <Employee 0: $0 in assets>
deallocating <Employee 4: $0 in assets>
deallocating <Employee 8: $0 in assets>

注意，现在那些拥有资产的员工都没有被正确释放。同样，资产对象也没有被释放。为什么？

资产拥有员工，员工拥有资产数组，而资产数组又拥有资产。这就是由这种所有权循环创建的一个垃圾孤岛。这些对象本应被释放以释放内存，但实际上并没有。这就被称为*循环引用*（retain cycle）。循环引用是内存泄漏的一个非常常见的来源。

要在程序中查找循环引用，可以使用 Apple 的性能分析工具 Instruments。在对程序进行性能分析时，你会在程序运行期间监控它，以查看代码和系统幕后发生的情况。但是，你的程序运行并退出得非常、非常快。为了给你留出进行性能分析的时间，请在 `main()` 函数末尾添加 100 秒的 `sleep()`：

... }
sleep(100);
return 0;
}

在 Xcode 中，在菜单中选择 **Product → Profile**。Instruments 将启动。当出现可能的性能分析工具列表时，选择 *Leaks*（内存泄漏检测）：

### 图 20.2 选择性能分析器

![](img/5f9368899ebf8d92fc145f8def1e89f8_138_0.png)

随着程序运行，你可以查看当前状态。在窗口的左侧有两个可供选择的工具（图 20.3）。点击 Allocations 工具，你可以看到一个柱状图，显示堆中已分配的所有内容：

### 图 20.3 Allocations 工具

![](img/5f9368899ebf8d92fc145f8def1e89f8_138_1.png)

例如，你可以看到，堆中仍有 10 个 *Asset* 实例存活。

为了查找循环引用，切换到 Leaks 工具，并从表格上方的菜单栏中选择 Cycles 视图。选择一个特定的循环以查看其对象图：

### 图 20.4 Leaks 工具

![](img/5f9368899ebf8d92fc145f8def1e89f8_139_0.png)

## 弱引用

你如何修复循环引用？使用弱引用。*弱引用*是一个*不*表示所有权的指针。为了修复我们的循环引用，资产不应拥有其持有者：编辑 `Asset.h` 以将 holder 改为弱引用：

```c
#import <Foundation/Foundation.h>
@class Employee;
@interface Asset : NSObject
{
    NSString *label;
    __weak Employee *holder;
    unsigned int resaleValue;
}
@property (strong) NSString *label;
@property (weak) Employee *holder;
@property unsigned int resaleValue;
@end
```

构建并运行程序。注意，现在所有对象都被正确释放了。

在父子关系中，防止此类循环引用的一般规则是：父对象拥有子对象，但子对象不应拥有父对象。

## 弱引用的置零

为了查看弱引用的实际效果，让我们向混合添加另一个数组。如果我们想要一个包含所有资产（甚至包括那些未分配给特定员工的资产）的数组会怎样？我们可以随资产创建时将其添加到数组中。在 `main.m` 中添加几行代码：

```objectivec
#import <Foundation/Foundation.h>
#import "Employee.h"
#import "Asset.h"
int main(int argc, const char * argv[])
{
    @autoreleasepool {
        // Create an array of Employee objects
        NSMutableArray *employees = [[NSMutableArray alloc] init];
        for (int i = 0; i < 10; i++) {
            // Create an instance of Employee
            Employee *person = [[Employee alloc] init];
            // Give the instance variables interesting values
            [person setWeightInKilos:90 + i];
            [person setHeightInMeters:1.8 - i/10.0];
            [person setEmployeeID:i];
            // Put the employee in the employees array
            [employees addObject:person];
        }
        NSMutableArray *allAssets = [[NSMutableArray alloc] init];
        // Create 10 assets
        for (int i = 0; i < 10; i++) {
            // Create an asset
            Asset *asset = [[Asset alloc] init];
            // Give it an interesting label
            NSString *currentLabel= [NSString stringWithFormat:@"Laptop %d", i];
            [asset setLabel:currentLabel];
            [asset setResaleValue:1 * 17];
            // Get a random number between 0 and 9 inclusive
            NSUInteger randomIndex = random() % [employees count];
            // Find that employee
            Employee *randomEmployee = [employees objectAtIndex:randomIndex];
            // Assign the asset to the employee
            [randomEmployee addAssetsObject:asset];
            [allAssets addObject:asset];
        }
        NSLog(@"Employees: %@", employees);
        NSLog(@"Giving up ownership of one employee");
[employees removeObjectAtIndex:5];
NSLog(@"allAssets: %@", allAssets);
NSLog(@"Giving up ownership of arrays");
allAssets = nil;
employees = nil;
}
select(100);
return 0;
}
```

在构建并运行程序之前，想想你期望输出是什么样的。你会看到 `allAssets` 数组的内容——在 Employee #5 被释放之后。此时 Employee #5 的资产状态会怎样？这些资产失去了一个所有者（Employee #5），但它们仍由 `allAssets` 拥有，所以它们不会被释放。

那么之前由 Employee #5 拥有的资产的 `holder` 呢？当弱引用指向的对象被释放时，指针变量会被置零，即设置为 `nil`。因此，Employee #5 的资产不会被释放，而它们的 `holder` 变量将自动设置为 `nil`。

现在构建并运行程序并检查你的输出：

Employees: (
    "<Employee 0: $0 in assets>",
    ...
    "<Employee 9: $136 in assets>"
)
Giving up ownership of one employee
deallocating <Employee 5: $136 in assets>
allAssets: {
    "<Laptop 0: $0, assigned to <Employee 3: $68 in assets>>",
    "<Laptop 1: $17, assigned to <Employee 6: $119 in assets>>",
    "<Laptop 2: $34, assigned to <Employee 7: $34 in assets>>",
    "<Laptop 3: $51 unassigned>",
    "<Laptop 4: $68, assigned to <Employee 3: $68 in assets>>",
    "<Laptop 5: $85 unassigned>",
    "<Laptop 6: $102, assigned to <Employee 6: $119 in assets>>",
    "<Laptop 7: $119, assigned to <Employee 2: $119 in assets>>",
    "<Laptop 8: $136, assigned to <Employee 9: $136 in assets>>",
    "<Laptop 9: $153, assigned to <Employee 1: $153 in assets>>"
}
Giving up ownership of arrays
deallocating <Laptop 3: $51 unassigned>
...
deallocating <Laptop 8: $136 unassigned>

## 供好奇者参考：手动引用计数与 ARC 历史

如第 19 章开头所述，在 Objective-C 中加入自动引用计数（ARC）之前，我们使用*手动引用计数*，它使用*引用计数*。在使用手动引用计数时，所有权的变更仅当你向对象发送显式消息来递减或递增引用计数时才会发生。

```objectivec
[anObject release]; // anObject 失去一个所有者
[anObject retain]; // anObject 获得一个所有者
```

你会主要在这些调用中看到访问器方法（其中新值被保留，旧值被释放）以及 `dealloc` 方法（其中之前保留的所有对象都被释放）。`Asset` 的 `setHolder:` 方法看起来会像这样：

```objectivec
- (void)setHolder:(Employee *)newEmp
{
    [newEmp retain];
    [holder release];
    holder = newEmp;
}
```

`dealloc` 方法看起来会像这样：

```objectivec
- (void) dealloc
{
    [label release];
    [holder release];
    [super dealloc];
}
```

那么 `description` 方法呢？它创建并返回一个字符串。`Asset` 应该声称拥有它吗？那没有意义；资产正在赠送它创建的字符串。当你自动释放（autorelease）一个对象时，你正在标记它以便在未来发送 `release` 消息。在 ARC 出现之前，`Asset` 的 `description` 方法看起来像这样：

```objectivec
- (NSString *)description
{
    NSString *result = [[NSString alloc] initWithFormat:@"<%@: $%d >",
                     [self label], [self resaleValue]];
    [result autorelease];
    return result;
}
```

何时会发送 `release`？当当前的自动释放池被排空时：

```objectivec
// Create the autorelease pool
NSAutoreleasePool *arp = [[NSAutoreleasePool alloc] init];
Asset *asset = [[Asset alloc] init];
NSString *d = [asset description];
// The string that d points to is in the autorelease pool
[arp drain]; // The string is sent the message release
```

ARC 自动使用自动释放池，但你必须创建和排空池。当 ARC 被创建时，我们也获得了一种创建自动释放池的新语法。上面的代码现在看起来像这样：

```objectivec
// Create the autorelease pool
@autoreleasepool {
    Asset *asset = [[Asset alloc] init];
    NSString *d = [asset description];
    // The string that d points to is in the autorelease pool
}
// The pool is drained
```
