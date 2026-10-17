
```objc
double d = [laterDate timeIntervalSinceDate:earlierDate];
```

## 嵌套消息发送

有一个类方法 `alloc`，它返回一个指向新对象的指针，该对象需要初始化。然后该指针被用于向新对象发送消息 `init`。使用 `alloc` 和 `init` 是 Objective-C 中创建对象最常用的方式。通过嵌套消息发送，在一行代码中发送这两个消息是一个良好的习惯（也是 Apple 认可的唯一方法）：

```
[[NSDate alloc] init];
```

系统会先执行内部的消息，然后执行包含这些内部消息的消息。因此，`alloc` 被发送给 `NSDate` 类，而该操作的结果（即一个指向新创建的实例的指针）随后被发送了 `init` 消息。`init` 返回一个指向该新对象的指针（这几乎总是来自 `alloc` 返回的那个指针），因此我们可以使用 `init` 的返回值进行赋值。尝试通过修改这一行，在你的代码中测试这些嵌套消息：

```
NSDate *now = [[NSDate date];
```

to

```
NSDate *now = [[NSDate alloc] init];
```

## 多参数

某些方法接受多个参数。例如，一个 `NSDate` 对象并不知道现在是哪一天。如果你需要这些信息，将使用 `NSCalendar` 对象。告诉你是几号的方法有三个参数。创建 `NSCalendar` 对象并在 `main` 中使用它：

```objc
#import <Foundation/Foundation.h>
int main(int argc, const char *argv[]) {
    @autoreleasepool {
        NSDate *now = [[NSDate alloc] init];
        NSLog(@"The date is %@", now);
        double seconds = [now timeIntervalSince1970];
        NSLog(@"It is %f seconds since the start of 1970.", seconds);
        NSDate *later = [now dateByTimeInterval:100000];
        NSLog(@"In 100,000 seconds it will be %@", later);

        NSCalendar *cal = [NSCalendar currentCalendar];
        NSInteger day = [cal component:NSDayUnit
                            in:NSMonthUnit
                            for:now];
        NSLog(@"This is day %ld of the month", day);
    }
    return 0;
}
```

该方法的名为 `component:in:for:`，它接受三个参数。你可以看出消息被拆分成了三行。这没关系；编译器并不介意额外的空格。Objective-C 程序员通常使用冒号，这样很容易将方法名的部分与参数区分开。（Xcode 应该为你完成这一点：每当你开始新的一行时，前一行应该正确缩进。）该方法的第一个和第二个参数是常量 `NSDayUnit` 和 `NSMonthUnit`。这些常量定义在 `NSCalendar` 类中。它们告诉方法你想知道该月份内是哪一天。第三个参数是你想要查询的日期。如果你想知道一年的第几小时而不是月份的某一天，你会使用这些常量：

```
NSInteger hour = [cal component:NSHourUnit in:NSYearUnit for:now];
```

## 向 nil 发送消息

几乎所有的面向对象的语言都有 nil 的概念，即指向无对象的指针。在 Objective-C 中，nil 是零指针（与 `NULL` 相同，这在第 8 章中讨论过）。在大多数面向对象的语言中，向 nil 发送消息是不允许的。因此，你必须在访问对象之前检查它是否为 nil。所以你会经常看到这样的代码：

```
if (fido != nil) {
  [fido speak];
}
```

在设计 Objective-C 时，人们决定向 nil 发送消息是可以接受的；它只是什么都不做。因此，这段代码是完全合法的：

```
Dog *fido = nil;
[fido speak];
```

重要事项 #1：如果你正在发送消息但什么都没有发生，请确保你没有向一个已被设置为 nil 的指针发送消息。

重要事项 #2：如果你向 nil 发送消息，返回值没有任何意义。

```
Dog *fido = nil;
NSString *daily = [fido speak];
```

在这种情况下，`daily` 将是 0。（通常情况下，如果你期望结果是数字或指针，向 nil 发送消息将返回 0。然而，对于结构体等类型，你将得到奇怪且意外的返回值。）

## 挑战

在你的 Mac 上，有一个类 `NSTimeZone`。在它的许多方法中，有一个类方法 `systemTimeZone`，返回你电脑的时区（作为 `NSTimeZone` 的实例），以及一个实例方法 `isDaylightSavingTime`，如果时区当前处于夏令时间，它返回 YES。

编写一个 Foundation 命令行工具，用来告诉你现在是否是夏令时间。

## NSString

`NSString` 是另一个 Objective-C 程序员经常使用的类。`NSString` 的实例持有字符字符串。在代码中，你可以创建一个 `NSString` 的字面量实例：

```
NSString *lament = @"Why me!";
```

在 Time 项目中，你输入：

```
NSLog(@"The date is %@", now);
```

`NSLog` 是一个 Objective-C 函数（而不是方法！）它的工作原理类似于 `printf()`。在 `NSLog()` 中，格式字符串是 `NSString` 的实例。`NSString` 的实例可以使用 `stringWithFormat:` 类方法创建：

```
NSString *x = [NSString stringWithFormat:@"The number is %d", 5];
```

获取字符串中的字符数量，可以使用 `length` 方法：

```
NSInteger charCount = [x length];
```

你可以使用 `isEqual:` 方法检查两个字符串是否相等：

```
if ([lament isEqual:x])
    NSLog(@"%@ and are equal", x);
```

C 语言也有字符串构造。这里是 C 语言的示例：

```c
char *lament = "Why me!";
char *x;
printf("The number is %lu\n", strlen(lament));
if (strcmp(lament, x) == 0)
    printf("%s and %s are equal\n", lament, x);
```

## 挑战

有一个类叫 `NSHost`，包含了关于你电脑的信息。要获取 `NSHost` 的实例，可以使用 `NSHost` 类方法 `currentHost`。该方法返回一个指向 `NSHost` 对象的指针：

```
+ (NSHost *)currentHost;
```

要获取电脑的本地化名称，可以使用 `NSHost` 实例方法 `localizedName`，它返回一个指向 `NSString` 对象的指针：

```
- (NSString *)localizedName;
```

编写一个命令行工具。

## NSArray

就像 `NSString` 一样，`NSArray` 是另一个 Objective-C 程序员经常使用的类。`NSArray` 的实例持有指针的列表。例如，假设你想创建一个三个 `NSDate` 对象的列表，然后遍历列表并打印每个日期。

创建一个新项目：一个名为 DateList 的 Foundation 命令行工具。打开 `main.m` 并修改 `main()` 函数：

```objc
#import <Foundation/Foundation.h>

int main(int argc, const char *argv[]) {
    @autoreleasepool {
        // 创建三个 NSDate 对象
        NSDate *now = [NSDate date];
        NSDate *tomorrow = [now dateAddingTimeInterval:24.0 * 60.0 * 60.0];
        NSDate *yesterday = [now dateAddingTimeInterval:-24.0 * 60.0 * 60.0];

        // 创建包含这三个对象的数组（nil 终止列表）
        NSArray *dateList = [NSArray arrayWithObjects:now, tomorrow, yesterday, nil];

        // 有多少日期？
        NSLog(@"There are %lu dates", [dateList count]);

        // 打印几个
        NSLog(@"The first date is %@", [dateList objectAtIndex:0]);
        NSLog(@"The third date is %@", [dateList objectAtIndex:2]);
    }
    return 0;
}
```

`NSArray` 有两个在示例中所示的方法，你会经常使用：

- `count` 返回数组中的项目数量
- `objectAtIndex:` 返回数组在参数指定的索引处存储的指针。

数组是有序的，你通过索引访问数组中的项。数组是基于零索引的：第一个项存储在索引 0，第二个项存储在索引 1，以此类推。因此，如果 `count` 方法显示数组中有 100 个项，你可以使用 `objectAtIndex:` 来请求索引从 0 到 99 的对象。

## 图 15.1 DateList 的对象图

![](img/a694739dec801cd745c57da9e19c2cd4_136_0.png)

因此，如果你想循环并处理数组中的每个项（或“遍历数组”），你可以创建一个 `for` 循环。编辑 `main.m`：

```objc
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // Create NSDate objects
        NSDate *now = [NSDate dateAddingTimeInterval:-24.0 * 60.0];
        NSDate *tomorrow = [now dateAddingTimeInterval:24.0 * 60.0];
        NSDate *yesterday = [now dateAddingTimeInterval:-24.0 * 60.0];

        // Create an array containing all three (nil terminates the list)
        NSArray *dateList = [NSArray arrayWithObjects:now, tomorrow, yesterday, nil];

        NSInteger dateCount = [dateList count];
        for (int i = 0; i < dateCount; i++) {
            NSDate *d = [dateList objectAtIndex:i];
            NSLog(@"Here is a date: %@", d);
        }
        return 0;
    }
}
```

程序员经常进行这种操作，以至于为 `for` 循环添加了专门遍历数组的扩展。修改代码使用这种机制：

```objc
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // Create three NSDate objects
        NSDate *now = [NSDate date];
        NSDate *tomorrow = [now dateByTimeInterval:24.0 * 60.0 * 60.0];
        NSDate *yesterday = [now dateByTimeInterval:-24.0 * 60.0 * 60.0];

        // Create an array containing all three (nil terminates the list)
        NSArray *dateList = [NSArray arrayWithObjects:now, tomorrow, yesterday, nil];

        for (NSDate *date in dateList) {
            NSLog(@"Here is a date: %@", date);
        }
    }
    return 0;
}
```

这种类型的循环被称为快速枚举，它是遍历数组中项的一种极其高效的方法。有一个限制：在对数组枚举时，你不能向数组中添加或删除元素。

## NSMutableArray

数组有两种类型：

- `NSArray` 实例是通过指针列表创建的。你永远无法从该数组中添加或删除指针。
- `NSMutableArray` 实例与 `NSArray` 实例相似，但你可以添加和删除指针。(`NSMutableArray` 是 `NSArray` 的子类。更多关于子类的信息请见第 18 章。)

修改你的示例以使用 `NSMutableArray` 实例和 `NSMutableArray` 类的方法：

```objc
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // Create three Date objects
        NSDate *now = [NSDate date];
        NSDate *tomorrow = [now dateAddingTimeInterval:24.0 * 60.0 * 60.0];
        NSDate *yesterday = [now dateAddingTimeInterval:-24.0 * 60.0 * 60.0];

        // Create an empty array
        NSMutableArray *dateList = [NSMutableArray array];

        // Add the dates to the array
        [dateList addObject:now];
        [dateList addObject:tomorrow];

        // Put yesterday at the beginning of the list
        [dateList insertObject:yesterday atIndex:0];

        for (NSDate *d in dateList) {
            NSLog(@"Here is a date: %@", d);
        }

        // Remove yesterday
        [dateList removeObjectAtIndex:0];
        NSLog(@"Now the first date is %@", [dateList objectAtIndex:0]);

    }

    return 0;
}
```

## 挑战

创建一个名为 Groceries 的新 Foundation 命令行工具。从创建一个空的 `NSMutableArray` 对象开始。然后向数组中添加几个类似杂货的项（你也需要创建它们）。最后，使用快速枚举打印出你的购物列表。

下一个挑战确实更有挑战性。阅读以下程序，它会寻找包含两个相邻 A 的常用专有名词。
