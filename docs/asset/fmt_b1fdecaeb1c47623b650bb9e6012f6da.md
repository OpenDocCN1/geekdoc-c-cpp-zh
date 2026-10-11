
```objc
// Basic String Operations - Mutable Strings

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSString *strl = @"This is string A";
        NSString *search, *replace;
        NSMutableString *mstr;
        NSRange substr;

        // Create mutable string from nonmutable
        mstr = [NSMutableString stringWithString: strl];
        NSLog("%@", mstr);

        // Insert characters
        [mstr insertString:@"@ mutable" atIndex: 7];
        NSLog("%@", mstr);

        // 如果在末尾插入，则是有效的拼接
        [mstr insertString:@"@ and string B" atIndex: [mstr length]];
        NSLog("%@", mstr);

        // 或者可以直接使用 appendString
        [mstr appendString:@"@ and string C"];
        NSLog("%@", mstr);

        // 根据范围删除子字符串
        [mstr deleteCharactersInRange:NSMakeRange(16, 13)];
        NSLog("%@", mstr);

        // 先找到范围，然后将其用于删除
        substr = [mstr rangeOfString:@"@string B and "];
        if (substr.location != NSNotFound) {
            [mstr deleteCharactersInRange:substr];
            NSLog("%@", mstr);
        }

        // 直接设置可变字符串
        [mstr set:@"This is string A"];
        NSLog("%@", mstr);

        // 现在用另一个字符串替换一段范围的字符
        [mstr replaceCharactersInRange:NSMakeRange(8, 8) withString:@"a mutable string"];
        NSLog("%@", mstr);

        // 搜索并替换
        search = @"This is";
        replace = @"An example of";
        if (substr.location != NSNotFound) {
            [mstr replaceCharactersInRange:substr withString:replace];
            NSLog("%@", mstr);
        }

        // 搜索并替换所有出现
        search = @"a";
        replace = @"x";
        substr = [mstr rangeOfString:search];

        while (substr.location != NSNotFound) {
            [mstr replaceCharactersInRange:substr withString:replace];
            substr = [mstr rangeOfString:search];
        }
        NSLog("%@", mstr);
    }
    return 0;
}
```

# 程序 15.5 输出

This is string A

This is mutable string A

This is mutable string A and string B

This is mutable string A and string B and string C

This is mutable string B and string C

This is mutable string C

This is string A

This is a mutable string

An example of a mutable string

An example of a mutable string

### 声明

`NSMutableString *mstr;` 将 `mstr` 声明为一个持有字符字符串对象的变量，其内容在程序执行期间可能会发生。

```objc
mstr = [NSMutableString stringWith:str1];
```

将`mstr` 设置为其内容是 `str1` 中字符拷贝的字符串对象，或 "This is string A"。当 `stringWith:` 方法发送给 `NSMutableString` 类时，会返回一个可变字符串对象。当它发送给 `NSString` 类时（如程序 15.5 所示），你得到的是不可变字符串对象。

`insertString:AtIndex:` 方法将指定的字符字符串从指定的索引开始插入到接收者中。在这种情况下，你将字符串 "mutable" 插入从索引 7 开始的字符串，或者说插入到字符串第8个字符之前。与不可变对象的方法不同，这里没有返回值，因为接收者被修改了——你可以这样做是因为它是可变字符串对象。

第二次调用 `insertString:AtIndex:` 使用 `length` 方法在另一个字符串的末尾插入一个字符字符串。`appendString:` 方法让这项任务变得简单一点。

通过使用 `deleteCharactersInRange:` 方法，你可以从字符串中删除指定数量的字符。当范围 `{16, 13}` 应用于字符串 `This is mutable string A and string B and string C` 时，会删除从索引16（或字符串中的第17个字符）开始的13个字符 "string A and "。如图 15.4 所示。

### 图 15.4. 字符串索引

![](img/6897a0c84e438cb4e5aad2d8a2fad0b8_509_0.png)

`rangeOfString:` 方法在程序 15.5 的后续行中使用，用于展示如何先定位字符串再删除它。在首先确认 `mstr` 中不存在 "@string B and" 后，使用 `deleteCharactersInRange:` 方法删除字符，并将 `range:` 方法返回的范围作为其参数。

你可以使用 `set:` 方法直接设置可变字符串对象的内容。在使用该方法将 `mstr` 设置为字符串 "@This is string A" 后，`replaceCharactersInRange:withString:` 方法用另一个字符串替换字符串中的某些字符。字符串的大小不必相同；你可以用一个相等或不相等大小的字符串替换另一个。因此，在语句：

```objc
[mstr replaceCharactersInRange:NSMakeRange(8, 8) withString:@"a mutable string"];
```

这8个字符 "string A" 被替换为16个字符 "a mutable string"。

程序示例中的剩余几行显示了如何执行搜索和替换操作。在第一种情况下，你在 `mstr` 内部定位字符串 "@This is"，并将其设置为 "An example of"。接下来设置了一个循环以实现“搜索并替换所有”的操作。注意，如果替换字符串为空，你将导致无限循环。其次，如果替换字符串为空（那么），你实际上删除了该字符串的所有出现处。当然，如果你只是想删除某一次出现，可以使用 `deleteCharacters:` 方法。

最后，`NSMutableString` 类还包含 `replaceOccurrencesOfString:withString:options:range:` 方法，你可以使用它来实现相同的结果并规避无限循环的风险。

```objc
mstr replaceOccurrencesOfString:search withString:replace options:nil range:NSMakeRange(0, [mstr length]);
```

`NSString` 类包含 100多个可以处理字符串对象的方法。表 15.2 汇总了一些常用的方法，而表 15.3 列出了 `NSMutableString` 类提供的某些额外方法。其他方法（如处理路径和读取文件内容）将在本书的剩余部分中介绍。你应该查看 `NSString` 类的文档，以更好地了解你可以利用的各种方法。

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

返回从字符串开始到索引 `i` 处字符的子字符串

比较两个字符串，忽略大小写

比较两个字符串

测试字符串是否以 `nsstring` 开头

测试字符串是否以 `nsstring` 结尾

测试两个字符串是否相等

返回一个每个单词首字母大写（且每个转换后的单词剩余字母均转换为小写）的字符串

返回一个转换为小写的字符串

返回一个转换为大写的字符串

返回一个转换为 UTF-8 C 风格字符串的字符串

返回字符串的双精度精度（double）浮点数表示

返回字符串的浮点数表示

返回字符串的 `NSInteger` 表示

返回字符串的整数表示

在表 15.2 和表 15.3 中，`url` 是一个 `NSURL` 对象，`path` 是指定文件路径的 `NSString` 对象，`nsstring` 是一个 `NSString` 对象，`i` 是一个代表字符串中有效字符数量的 `NSInteger` 值，`enc` 是一个指定字符编码的 `NSStringEncoding` 对象，`err` 是一个在发生错误时描述错误的 `NSError` 对象，`size` 和 `opts` 是 `NSInteger` 类型，`range` 是一个指示字符串内有效字符范围的 `NSRange` 结构。

表 15.3 中的方法用于创建或修改 `NSMutableString` 对象。

### 表 15.3. 常用 NSMutableString 方法

| 方法 | 描述 |

| --- | --- |

| `+(id) stringWithCapacity: size` | 创建一个初始包含 `size` 个字符的字符串。 |

| `-(id) initWithCapacity: size` | 初始化一个初始容量为 `size` 个字符的字符串。 |

| `-(void) setString: nsstring` | 将字符串设置为 `nsstring`。 |

| `-(void) appendString: nsstring` | 在接收者的末尾追加 `nsstring`。 |

| `-(void) deleteCharactersInRange: range` | 删除指定范围内的字符。 |

| `-(void) insertStringAtIndex: i` | 从索引 `i` 开始在接收者中插入 `nsstring`。 |

| `-(void) replaceCharactersInRange: range: nsstring` | 用 `nsstring` 替换指定范围内的字符。 |

`NSString` 对象在本文的后续部分被广泛使用。如果你需要将字符串解析为标记（tokens），可以查看 Foundation 的 `NSScanner` 类。

## 数组对象

Foundation 数组是对象的有序集合。大多数情况下，数组中的元素是同一种类型的，但并非如此。就像可变和不可变字符串一样，也有可变和不可变数组。不可变数组由 `NSArray` 类处理，而可变数组由 `NSMutableArray` 处理。后者是前者的子类，这意味着它继承了它们的方法。

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

### 注意
