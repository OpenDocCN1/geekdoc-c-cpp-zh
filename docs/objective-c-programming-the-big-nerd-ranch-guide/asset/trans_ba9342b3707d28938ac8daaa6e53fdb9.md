
#import "Person.h"
@class Asset;

@interface Employee : Person
{
    int employeeID;
    NSMutableArray *assets;
}
@property int employeeID;
- (void)addAssetsObject:(Asset *)a;
- (unsigned int)valueOfAssets;

@end

请注意 `@class Asset;` 这一行。当编译器读取此文件时，它会遇到类名 `Asset`。如果它不了解这个类，就会抛出错误。`@class Asset;` 这行代码告诉编译器：“有一个名为 `Asset` 的类。当你在该文件中看到它时不要惊慌。目前你只需要知道这些。”

使用 `@class` 代替 `#import` 会使编译器获得较少的信息，但会加快处理该特定文件的速度。你可以在 `Employee.h` 和其他头文件中使用 `@class`，因为编译器在处理声明文件时不需要知道很多信息。

现在请关注 `Employee.m`。对于“多对一”关系，你需要在将任何内容放入其中之前创建集合对象（在我们的情况下是数组）。你可以在原始对象（员工）最初创建时这样做，或者你可以懒一点，等到需要集合时再创建。让我们懒一点。

```objc
#import "Employee.h"
#import "Asset.h"

@implementation Employee

@synthesize employeeID;

- (void)addAssetsObject:(Asset *)a
{
    // assets 是否为 nil？
    if (!assets) {
        // 创建数组
        assets = [NSMutableArray alloc] init];
    }
    [assets addObject:a];
}

- (unsigned int)valueOfAssets
{
    // 累加资产的转售价值
    unsigned int sum = 0;
    for (Asset *a in assets) {
        sum += [a resaleValue];
    }
    return sum;
}

- (float)bodyMassIndex
{
    float normalBMI = [super bodyMassIndex];
    return normalBMI * 0.9;
}

- (NSString *)description
{
    return [NSString stringWithFormat:@"<Employee %d: $%d in assets>",
           [self employeeID], [self valueOfAssets]];
}

- (void)dealloc
{
    NSLog(@"deallocating %@", self);
}

@end
```

为了处理 `Employee.m` 文件，编译器需要了解关于 **Asset** 类的许多信息。因此，你导入了 `Asset.h` 而不是使用 `@class`。

还要注意，你重写了 **description** 和 **dealloc** 方法来跟踪 **Employee** 实例的释放。

构建项目以检查你是否有错误。

现在你需要创建一些资产并将它们分配给员工。编辑 `main.m`：

```objc
#import <Foundation/Foundation.h>
#import "Employee.h"
#import "Asset.h"

int main(int argc, const char * argv[])
{
    @autoreleasepool {
        // 创建 Employee 对象的数组
        NSMutableArray *employees = [[NSMutableArray alloc] init];
        
        for (int i = 0; i < 10; i++) {
            // 创建 Employee 实例
            Employee *person = [[Employee alloc] init];
            
            // 给实例变量赋予有趣的值
            [person setWeightInKilos:90 + i];
            [person setHeightInMeters:1.8 - i/10.0];
            [person setEmployeeID:i];
            
            // 将员工放入 employees 数组
            [employees addObject:person];
        }
        
        // 创建 10 个资产
        for (int i = 0; i < 10; i++) {
            // 创建一个资产
            Asset *asset = [[Asset alloc] init];
            
            // 给它一个有趣的标签
            NSString *currentLabel = [NSString stringWithFormat:@"Laptop %d", i];
            [asset setLabel:currentLabel];
            [asset setResaleValue: i * 17];
            
            // 获取 0 到 9 之间的随机数（包含 9）
            NSUInteger randomIndex = random() % [employees count];
            
            // 找到该员工
            Employee *randomEmployee = [employees objectAtIndex:randomIndex];
            
            // 将资产分配给员工
            [randomEmployee addAssetsObject:asset];
        }

        NSLog(@"Employees: %@", employees);
        
        NSLog(@"放弃对一名员工的所有权");
        [employees removeObjectAtIndex:5];
        
        NSLog(@"放弃对数组的所有权");
        employees = nil;
    }
    return 0;
}
```

构建并运行程序。你应该看到类似以下内容：

```text
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
放弃对一名员工的所有权
deallocating <Employee 5: $136 in assets>
deallocating <Laptop 3: $51 >
deallocating <Laptop 5: $85 >
放弃对数组的所有权
deallocating <Employee 0: $0 in assets>
deallocating <Employee 1: $153 in assets>
deallocating <Laptop 9: $153 >
deallocating <Employee 9: $136 in assets>
deallocating <Laptop 8: $136 >
```

当员工 #5 从数组中移除时，由于它没有所有者，因此被释放。然后，由于它们的资产没有所有者，这些资产也被释放。（你必须相信我这一点：被释放资产的标签（`NSString` 的实例）在失去所有者后也会被释放。）

当 **employees** 被设置为 **nil** 时，数组不再拥有所有者。因此，数组被释放，这引发了一连串更大规模的内存清理和释放连锁反应，因为突然间，没有 **employees** 拥有所有者了。

很整洁，对吧？当对象变得不再需要时，它们被释放。这是好的。当不必要的对象没有被释放时，我们就说你存在*内存泄漏*。通常，内存泄漏会导致越来越多的对象不必要地长时间存在。你的应用的内存占用只会越来越大。在 iOS 上，操作系统最终会强制结束你的应用。在 Mac OS X 上，由于机器花费越来越多的时间将数据从内存交换到磁盘上，整个系统的性能都会受到影响。

## 挑战

使用之前挑战中的 **StockHolding** 类，创建一个工具，该工具创建 **Portfolio** 类的实例，并用股票持有填充它。投资组合可以告诉你它的当前价值。

*此页故意留白*

具有双向关系是很常见的。例如，也许资产应该知道当前持有它的是哪位员工。让我们添加这种关系。新的对象图看起来像这样：

### 图 20.1 添加 holder 关系

![](img/5f9368899ebf8d92fc145f8def1e89f8_135_0.png)

从设计角度来看，你会说我们是从子对象（**Asset** 的实例）添加了一个指向其父对象（持有它的 **Employee** 实例）的指针。

在 *Asset.h* 中，添加一个指针实例变量来持有持有该资产的员工：

```objc
#import <Foundation/Foundation.h>
@class Employee;

@interface Asset : NSObject
{
    NSString *label;
    Employee *holder;
    unsigned int resaleValue;
}
@property (strong) NSString *label;
@property (strong) Employee *holder;
@property unsigned int resaleValue;
@end
```

在 *Asset.m* 中，综合访问器并扩展 description 方法以显示持有者：

```objc
#import "Asset.h"
#import "Employee.h"

@implementation Asset

@synthesize label, resaleValue, holder;

- (NSString *)description
{
    // holder 是否非 nil？
    if ([self holder]) {
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

这带来了一个风格问题：当人们一起使用 Asset 类和 Employee 类时，我们如何确保这两种关系是一致的？也就是说，当且仅当员工是资产的持有者时，资产才应该出现在员工的资产数组中。有三种选择：

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

