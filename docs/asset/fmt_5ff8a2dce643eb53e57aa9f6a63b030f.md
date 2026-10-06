
```objc
if (compareResult == NSOrderedAscending) {
    NSLog("< %@", str2);
} else if (compareResult == NSOrderedSame) {
    NSLog("==", res);
} else {
    NSLog(">", str2);
}

// 将字符串转换为大写
res = [str1 uppercaseString];
NSLog(@"Uppercase conversion: %s", [res UTF8String]);

// 将字符串转换为小写
res = [str1 lowercaseString];
NSLog(@"Lowercase conversion: %@", res);
NSLog(@"Original string: %@", str1);
}
return 0;
}
```

## 程序 15.4 输出

```
Length of str1: 16
copy: This is A
Concatenation: This is AThis is B
str1 == res
str1 < str2
Uppercase conversion: THIS IS A
Lowercase conversion: this is a
Original string: This is A
```

程序 15.4 声明了三个 `NSMutableString` 对象：`str1`、`str2` 和 `res`。前两个初始化为常量字符串对象。声明 `NSComparison compareResult;` 定义了 `compareResult` 用于存储稍后执行字符串比较的结果。

你可以使用 `length` 方法统计字符串中的字符数量。它返回一个 `NSInteger` 无符号整数值。输出验证了字符串 `@"This is A"` 包含了 16 个字符。语句 `res = [NSString stringWithString:str1];` 显示了如何根据另一个创建一个新字符串。生成的 `NSString` 对象被赋值给 `res`，然后显示以验证结果。在这里是对内容的实际复制，而不仅仅是内存中相同字符串的引用。这意味着 `str1` 和 `res` 指向两个不同的字符串对象，这与仅执行简单的赋值不同：
`res = str1;`

如之前所述，这条语句创建了内存中同一个对象的另一个引用。`stringByAppendingString:` 方法可以连接两个字符字符串。因此，表达式 `[str stringByAppendingString:str2]`

# 第 15 章 数字、字符串、集合

创建一个由字符 `str` 紧接 `str2` 组成的新字符串对象并返回结果。原始字符串对象 `str1` 和 `str2` 不受此操作的影响。（它们不会受到影响，因为它们是不可变对象。）

在下一个程序中，`isEqualTo` 方法用于测试两个字符串是否相等——即是否包含相同的字符。如果你需要确定两个字符字符串的顺序，可以使用 `compare` 方法（例如，如果你想对这些字符串数组进行排序）。与你之前比较 `NSNumber` 对象时使用的 `compare` 方法类似，如果第一个字符串小于第二个字符串，比较结果为 `NSOrderedAscending`；如果两者相等，结果为 `NSOrderedSame`；如果第一个字符串大于第二个字符串，结果为 `NSOrderedDescending`。如果你不想进行区分大小写比较，请使用 `caseInsensitiveCompare` 方法代替 `compare`：比较两个字符串。在这种情况下，两个字符串对象 `@Gregory` 和 `@gregory` 使用 `caseInsensitiveCompare` 比较时是相等的。

`uppercaseString` 和 `lowercaseString` 是程序 15.3 中最后两个将字符串转换为大写和小写的 `NSString` 方法。同样，转换不会影响原始字符串，正如最后一行输出所验证的那样。

确保你将 `str1` 和 `str2` 为不可变字符串对象，这意味着它们所引用的字符串中的字符不能更改。然而，引用 `str1` 和 `str2` 是可以更改的。也就是说，这两个变量可以重新赋值以引用不同的不可变对象。这是一个非常重要的点。让我们通过图表再次查看这一点。图 15.1 显示了变量 `res` 和 `str1` 在声明和初始化后的状态。变量 `res` 没有设置任何初始值，因此其内容为空。相比之下，`str1` 被设置为指向常量字符对象 `@This is string A`。

```objc
NSString *str1 = @"This is string A";
NSString *res;
res;
```

图 15.1 不可变字符串对象的声明和初始化

当我们向程序 15.3 中的 `str1` 发送 `uppercaseString` 消息时，我们根据字符 `str1` 创建了一个新字符串，该字符串对象中的任何小写字符都被替换为大写字符，如图 15.2 所示。

# 字符串对象 323

```objc
NSString *str1 = @"This is string A";
str1 = @"This is string A";
```

```objc
res = [str1 uppercaseString];
// res = THIS IS STRING A
```

图 15.2 向字符串对象发送 `uppercaseString` 消息

注意 `str1` 指向原始字符串对象，并且创建了一个新的字符串对象。

向 `str` 发送 `lowercaseString` 消息的方式也是一样的：创建一个新对象，其由 `str` 中的所有大写字符转换为小写组成。这如图 15.3 所示。注意，上一步创建的大写字符串的引用不再存在。你不需要担心这个；系统的内存管理会为你清理。

```objc
NSString *str1 = @"This is string A";
str1 = THIS IS STRING A
```

```objc
res = [str1 lowercaseString];
// res = this is string a
```

图 15.3 向字符串对象发送 `lowercaseString` 消息

程序 15.5 阐述了处理字符串的其他方法。这些方法允许你从字符串中提取子字符串并进行搜索以找到另一个字符串出现的位置。

某些方法要求你通过指定范围来识别子字符串。范围由起始索引加上字符计数组成。索引号从零开始，所以你通过数字对 `{0, 3}` 来指定字符串中的前三个字符。`NSString` 类（以及其他 Foundation 类）使用特殊数据类型 `NSRange` 来创建范围规范。它实际上是一个结构体的别名（typedef），该结构包含两个成员：`location` 和 `length`，每个都定义为 `NSInteger`。程序 15.5 使用了这种类型。

> 你可以在第 13 章“底层 C 语言特征”中阅读结构。不过，你仍然从本章随后的讨论中获得足够的操作结构的信息。

## 程序 15.5

// 基础字符串操作 - 继续

```objc
#import <Foundation/Foundation.h>
int main(int argc, char * argv[]) {
    @autoreleasepool {
        NSString *str1 = @"This is string A";
        NSString *res;
        NSRange subRange;
        // 从字符串中提取前 3 个字符
        res = [str1 substringToIndex: 3];
        NSLog("@First 3 chars of str1: %@", res);
        // 从索引 5 开始提取到末的字符
        res = [str1 substringFromIndex: 5];
        NSLog("@Chars from index 5 of str1: %@", res);
        // 提取索引 8 到 13 的字符（6 个字符）
        res = [[str1 substringFromIndex: 8] substringToIndex: 6];
        NSLog("@Chars from index 8 through 13: %@", res);
        // 实现相同事情更简单方法
        res = [str1 substringWithRange: NSRange(8, 6)];
        NSLog("@Chars from index 8 through 13: %@", res);
        // 在另一个内部查找一个
        subRange = [str1 rangeOfString: @"string A"];
        NSLog("@String is at index %lu, length is %lu", (unsigned long)subRange.location, (unsigned long)subRange.length);
        if (subRange.location == NSNotFound) {
            NSLog("@String not found");
        } else {
            NSLog("@String is at index %lu, length is %lu", (unsigned long)subRange.location, (unsigned long)subRange.length);
        }
    }
    return 0;
}
```

## 程序 15.5 的输出

```
@First 3 chars of str1: Thi
@Chars from index 5 of str1: string A
@Chars from index 8 through 13: string
@Chars from index 8 through 13: string A
@String is at index 8, length is 6
```

```objc
// 从不可变字符串创建可变字符串
```

```objc
mstr = [NSMutableString stringWithString:strString];
NSLog("%@", mstr);
```

```objc
// 插入字符
```

```objc
[mstr insertString:@"mutable" atIndex:7];
NSLog("%@", mstr);
```

```objc
// 如果在末尾插入，有效的拼接
```

```objc
[mstr insertString:@" and string B*" atIndex:[mstr length]];
NSLog("%@", mstr);
```

```objc
// 或者直接使用 appendString
```

```objc
[mstr appendString:@" and string C"];
NSLog("%@", mstr);
```

```objc
// 根据范围删除子字符串
```

```objc
[mstr deleteCharactersInRange: NSMakeRange(16, 13)];
NSLog("%@", mstr);
```

```objc
// 先查找范围再将其用于删除
```

```objc
substr = [mstr rangeOfString:@"string B and *"];
if (substr.location != NSNotFound) {
    [mstr deleteCharactersInRange:substr];
    NSLog("%@", mstr);
}
```

```objc
// 直接设置可变字符串
```

```objc
[mstr setString:@"This is string A*"];
NSLog("%@", mstr);
```

```objc
// 现在用另一个字符串替换范围内的字符
```

```objc
[mstr replaceCharactersInRange: NSMakeRange(8, 8)
withString:@"a mutable string"];
NSLog("%@", mstr);
```

```objc
// 查找并替换
```

## 328 第 15 章 数字、字符串与集合

```objc
search = @"This is";
replace = @"An example of*";
substr = [mstr rangeOfString:search];
if (substr.location != NSNotFound) {
    [mstr replaceCharactersInRange:substr
    withString:replace];
    NSLog("%@", mstr);
}
// 查找并替换所有出现次数
search = @"a";
replace = @"X*
```

## 程序 15.6 输出

```
This is string A
This is mutable string A
This is mutable string A and string B
This is mutable string A and string B and string C
This is mutable string B and string C
This is mutable string C
This is string A
This is a mutable string
An example of a mutable string
An example of X mutable string
```

声明
`MutableString *mstr;`

## 字符串对象 329

将 `mstr` 声明为持有字符字符串对象的变量，其内容在程序执行期间可能会发生变化。这一行：
`mstr = [MutableString stringWithString:str1];`

将 `mstr` 设置为内容为 `str1` 中字符拷贝的字符串对象，即 "This is string A"。当 `stringString:` 方法发送给 `NSMutableString` 类时，返回一个可变字符串。当发送给 `NSString` 类时（如程序 15.5 所示），你会得到一个不可变字符串对象。

`insertString:AtIndex:` 方法从指定的索引数字开始向接收者插入指定的字符。在这种情况下，你将字符串 "mutable" 插入到索引为 7 的位置，即字符串中第 8 个字符之前。与不可变字符串对象不同，这里没有返回结果，因为接收者被修改了；你可以这样做是因为它是一个可变字符串。

第二次 `deleteCharactersInRange:` 调用使用 `length` 方法在另一个字符串的末尾插入一个字符。`appendString:` 方法让这项任务简单一点。

通过使用 `deleteCharactersInRange:` 方法，你可以从字符串中删除指定数量的字符。将范围 `[16, 13]` 应用于字符串
`This is mutable string A and string B and string C`

它会从索引数字 16（或字符串中的第 17 个字符）开始删除 13 个字符 "string A and " string B"，如图 15.4 所示。

![](img/e9df1bbea9058fb77610264ec2bf7c_347_0.png)

图 15.4 字符串的索引化

`rangeOf:` 方法用于程序 15.5 后的后续行，以展示如何创建并删除字符串。在首先验证字符串 "string B" 存在于 `mstr` 后，使用 `deleteCharactersInRange:` 方法删除字符，并将 `rangeOf:` 方法的范围作为参数。

你可以使用 `setString:` 方法直接设置可变字符串的内容。在使用该方法将 `mstr` 设置为字符串 "This is string A" 后，`replaceCharactersInRange:withString:` 方法替换字符串中的部分字符。字符串的大小不一定相同；你可以用另一个大小相等或不等的字符串来替换。在语句中：

```objc
[mstr replaceCharactersInRange:NSMakeRange(0, 8)
withString:@"a mutable string];
```
