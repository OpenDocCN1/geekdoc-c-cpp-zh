

```objc
-(NSString *) substringToIndex:i
-(NSComparator *) caseInsensitiveCompare:nsstring
-(NSComparator *) compare:nsstring
-(BOOL) hasPrefix:nsstring
-(BOOL) hasSuffix:nsstring
-(BOOL) isEqualToString:nsstring
-(NSString *) capitalizedString
-(NSString *) lowercaseString
-(NSString *) uppercaseString
-(const char *) UTF8String
-(double) doubleValue
-(float) floatValue
-(NSInteger) integerValue
-(int) intValue
```

返回从字符串开始到索引 i 处字符的子字符串
比较两个字符串，忽略大小写
比较两个字符串
测试字符串是否以 nsstring 开头
测试字符串是否以 nsstring 结尾
测试两个字符串是否相等
返回一个每个单词首字母大写（且每个转换后的单词剩余字母均转换为小写）的字符串
返回一个转换为小写的字符串
返回一个转换为大写的字符串
返回一个转换为 UTF-8 C 风格字符串的字符串
返回字符串的双精度精度（double）浮点数表示
返回字符串的浮点数表示
返回字符串的 NSInteger 表示
返回字符串的整数表示

在表 15.2 和 15.3 中，url 是一个 NSURL 对象，path 是指定文件路径的 NSString 对象，nsstring 是一个 NSString 对象，i 是一个代表字符串中有效字符数量的 NSInteger 值，enc 是一个指定字符编码的 NSStringEncoding 对象，err 是一个在发生错误时描述错误的 NSError 对象，size 和 opts 是 NSInteger 类型，range 是一个指示字符串内有效字符范围的 NSRange 结构。

表 15.3 中的方法用于创建或修改 NSMutableString 对象。

## 表 15.3. 常用 NSMutableString 方法

| 方法 | 描述 |
| --- | --- |
| +(id) stringWithCapacity: size | 创建一个初始包含 size 个字符的字符串。 |
| -(id) initWithCapacity: size | 初始化一个初始容量为 size 个字符的字符串。 |
| -(void) setString: nsstring | 将字符串设置为 nsstring。 |
| -(void) appendString: nsstring | 在接收者的末尾追加 nsstring。 |
| -(void) deleteCharactersInRange: range | 删除指定范围内的字符。 |
| -(void) insertStringAtIndex: i | 从索引 i 开始在接收者中插入 nsstring。 |
| -(void) replaceCharactersInRange: range: nsstring | 用 nsstring 替换指定范围内的字符。 |

NSString 对象在本文的后续部分被广泛使用。如果你需要将字符串解析为标记（tokens），可以查看 Foundation 的 NSCanner 类。

## 数组对象

Foundation 数组是对象的有序集合。大多数情况下，数组中的元素是同一种类型的，但并非如此。就像可变和不可变字符串一样，也有可变和不可变数组。不可变数组由 NSArray 类处理，而可变数组由 NSMutableArray 处理。后者是前者的子类，这意味着它继承了它们的方法。

程序 15.6 设置了一个数组来存储月份并打印它们。

## 程序 15.6

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[])
{
    int i;
    @autoreleasepool {
        // 创建一个包含月份名称的数组
        NSArray *monthNames = [NSArray arrayWithObjects:
            "@January", "@February", "@March",
            "@April", "@May", "@June", "@July", "@August",
            "@September", "@October", "@November", "@December",
            nil];

        // 现在列出数组中的所有元素
        NSLog("@@Month Name: =====");

        for (i = 0; i < 12; i++) {
            NSLog("@%2i %@", i + 1, [monthNames objectAtIndex: i]);
        }
    }
    return 0;
}
```

## 程序 15.6. 输出

| 月份名称 | |
|---|---|
| 1 | January |
| 2 | February |
| 3 | March |
| 4 | April |
| 5 | May |
| 6 | June |
| 7 | July |
| 8 | August |
| 9 | September |
| 10 | October |
| 11 | November |
| 12 | December |

你可以使用 `arrayWithObjects:` 类创建一个以对象列表作为元素的数组。在这种情况下，对象按顺序列出并用逗号分隔。这是可以接受可数量参数的方法使用的特殊语法。为了标记列表的结束，必须将 `nil` 指定为列表中的最后一个值——它实际上并没有存储在数组内部。

在 `Program 15.6` 中，`monthNames` 被设置为 `arrayWithObjects:` 参数指定的 12 个字符串值。

数组中的元素通过它们的索引号识别。与 `NSString` 对象类似，索引从 0 开始。因此，一个包含 12 个元素的数组具有有效的索引号 0–11。要使用索引号检索数组的元素，可以使用 `objectAtIndex:` 方法。

程序简单地执行一个 `for` 循环，使用 `objectAtIndex:` 方法从数组提取每个元素。每个检索到的元素都通过 `NSLog` 显示。

## 程序 15.7

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[])
{
    int i;
    @autoreleasepool {
        NSMutableArray *numbers = [NSMutableArray array];
        NSNumber *myNumber;

        // 创建数组并添加数字对象
        for (i = 0; i < 10; i++) {
            myNumber = [NSNumber numberCreated:i];
            [numbers addObject:myNumber];
        }

        // 遍历数组并显示每个元素
        for (i = 0; i < numbers.count; i++) {
            NSLog("%@", [numbers objectAtIndex:i]);
        }

        // 一次显示整个数组
        NSLog("==== a single");
        NSLog("%%@", numbers);
    }
    return 0;
}
```

## 程序 15.7. 输出

| 月份名称 | |
|---|---|
| 1 | 0 |
| 2 | 1 |
| 3 | 2 |
| 4 | 3 |
| 5 | 4 |
| 6 | 5 |
| 7 | 6 |
| 8 | 7 |
| 9 | 8 |
| 10 | 9 |
| ==== a single | [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] |

## 注意

NSLog 如何知道如何显示存储在数组中的对象？对于数组中的每个元素，NSLog 都将使用该元素所属类的 `description` 方法。如果是继承自 NSObject 的默认方法，如之前所述，你只会得到对象的类和地址。但在这种情况下，你得到了一个有意义的显示——表明 Number 类中实现了一个自定义的 `description` 方法。

