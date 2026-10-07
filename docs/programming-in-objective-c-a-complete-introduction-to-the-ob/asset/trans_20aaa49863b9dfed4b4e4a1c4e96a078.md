

```objc
[matches addObject:obj];
return YES;
}
else
  return NO;
];
```

// 查看我们是否找到了匹配项

```objc
if ([matches count])
  return matches;
else
  return nil;
```

如果你想从数组中查找多个一个匹配项，也可以使用 `indexOfObjectsPassingTest:` 方法。该方法返回一个 `NSIndexSet`，其中包含了所有符合条件的元素索引。我们使用的以下版本用于查找并返回所有匹配的地址卡的索引。

```objc
- (NSIndexSet *) lookupAll:(NSString *)theName

```

```objc
NSIndexSet *result = [book indexOfObjectsPassingTest:
  ^(id obj, NSInteger idx, BOOL *stop) {
  if ([obj name] caseInsensitiveCompare:theName] == NSOrderedSame)
    return YES; // 找到了匹配项，继续查找
  else
    return NO; // 继续查找
}];
```

// 返回结果

```objc
return result;
```

你可以练习一下修改 `lookupAll` 方法的第二个版本，使其像第一个版本一样返回一个包含匹配地址卡的数组（提示：在 `indexOfObjectsPassingTest:` 方法完成后，遍历索引集中的每个索引，并将相应的元素添加到你将返回的数组中）。

表 15.11 中列出了一些代表性的 `NSIndexSet` 方法。在表中，`idx` 是一个 `NSInteger` 整数。鼓励你在文档中查找该类并学习更多相关信息。

## 第 15 章 数字、字符串和集合

表 15.11 一些 NSIndexSet 方法

| 方法 | 说明 |
| --- | --- |
| + (NSIndexSet) indexSet | 创建一个空索引集 |
| - (BOOL) containIndex: idx | 如果索引集包含该索引则返回 YES，否则返回 NO |
| - (NSUinteger) count | 返回索引集中集中索引的数量 |
| - (NSUinteger) firstIndex | 返回集合中的第一个索引；如果为空则返回 NSNotFound |
| - (NSUinteger) indexLessThanIndex: idx | 返回小于 idx 的最近索引；如果没有小于 idx 的索引则返回 NSNotFound。另见 indexLessThanEqualTo:; indexGreaterThanIndex;: 以及 indexGreaterThanEqualTo;: |
| - (NSUinteger) lastIndex | 给集合中的最后一个索引；如果集合为空则返回 NSNotFound |
| - (NSIndexSet *) indexesPassingTest: (BOOL*) (NSUinteger idx, BOOL *stop) block | 应用于集合中每个元素的块。返回 YES 则将 idx 添加到结果的 NSIndexSet 中，否则返回 NO；将 stop 指向的变量设置为 YES 以结束处理 |

## 练习题

- 1. 在你的文档中查找 `NSDate` 类。为 `NSDate` 添加一个名为 `ElapsedDays` 的新分类（category）。在新分类中，根据以下方法添加一个方法：`(unsigned long) elapsedDays: (NSDate*)date;`；让新方法返回接收者与方法参数之间已过去的天数。编写一个程序来测试你的新方法。（提示：查看 `years:months:days:hours:minutes`。）

- 2. 修改在本章中 `AddressBook` 类开发的 `lookup:` 方法，使其对名称表达式的部分匹配例如 `[myBook lookup:@"steve"]` 能够匹配到名称中任何位置包含该字符串的条目。对使用 `sortedArraySelector:` 方法的版本进行修改，同时也对章节末尾使用的 `indexOfObjectsPassingTest:` 方法的版本进行修改。

- 3. 使用练习 2 的结果，修改 `lookup:` 方法以搜索所有匹配的地址。让该方法返回所有匹配卡片的数组，如果没有匹配项则返回 `nil`。对使用 `sortedArraySelector:` 方法的版本进行修改，同时也对在“创建一个播放列表对象”末尾展示的版本进行修改，并添加和移除歌曲。如果新歌曲不在主播放列表中，应将其添加到主播放列表中。确保如果歌曲从主播放列表中移除，它也会从音乐集合中的所有播放列表中被移除。创建一个 `MusicCollection` 对象，并向集合中添加和移除播放列表。搜索并显示任何歌曲、任何播放列表或整个集合的信息。确保你的所有类都没有内存泄漏！

- 10. 编写一个程序，接收一个 `Number` 对象的 `NSArray`（其中每个 `NSNumber` 代表一个整数），并生成一个频率表，列出每个整数在数组中出现的次数。使用 `NSCountedSet` 对象来构建频率计数。

- 11. 当使用 `addCard:` 方法将卡片添加到地址簿时，谁拥有那张卡片？卡片上的任何信息可以被更改并影响存储在地址簿中的卡片吗？你能想到一种更安全的方法来实现此方法吗？

## 处理文件

Foundation 框架允许你访问文件系统以对文件和目录执行基本操作。这是通过 `NSFileManager` 提供的，其方法包括：

- 创建新文件
- 从现有文件读取
- 将数据写入文件
- 移除（删除）文件
- 测试文件是否存在
- 确定文件大小以及其他属性
- 复制文件
- 测试文件以检查内容是否相等

许多这些操作也可以在目录上执行。例如，你可以创建一个目录，读取其内容或删除它。另一个功能是链接文件的能力。也就是说允许同一个文件以两个名称存在，甚至可能在不同的目录中。

要打开文件并对文件进行多次读写操作，你可以使用 `NSFileHandle` 提供的方法。这些方法允许你

- 打开文件进行读取、写入或更新
- 移动到文件的指定位置
- 从文件读写入指定数量的字节

`NSFileHandle` 的方法也可以应用于设备或套接字。但在本章中我们只关注普通文件。

## 第 16 章 处理文件

`NSURL` 类允许你处理 URL，在应用程序中使用。`NSBundle` 类允许你处理应用程序包。这包括在包中搜索特定资源，例如图像。我们将在章末尾轻要介绍该类。

## 管理文件和目录：NSFileManager

文件或目录通过 `NSFileManager` 使用路径（pathname）进行唯一标识。路径是一个 `NSString` 对象，可以是相对路径或全路径。相对路径是相对于当前目录的。所以，文件名 `copy1.m` 表示当前目录下的 `copy1.m`。斜杠字符表示目录列表。`ch6/copy1.m` 也是一个相对路径，表示 `ch6` 目录下的 `copy1.m`。全路径也称为绝对路径，以 `/` 开头。在你的 Mac 上，家目录的全路径是 `/Users/stevechan`。此路径指定了三个目录：`/`（根目录）、`/Users` 和 `stackoverflowchan`。

特殊字符 `~` 用作用户目录的缩写。因此 `~linda` 将是 linda 用户目录的缩写，路径可能是 `/Users/linda`。单独的波浪表示当前用户的家目录，使得路径 `~/copy1.m` 指向用户家目录下的文件 `copy1.m`。其他 UNIX 风格路径字符，如表示当前目录的 `.` 和表示父目录的 `..`，在被任何 Foundation 方法使用之前应从路径中移除。提供了可用于此的路径实用工具。

你应该尽量避免在程序中硬编码路径。你将在本章看到，提供了方法和函数可以获取当前目录、用户家目录以及可用于临时文件的路径。你应该尽可能避免这样做。我们将在章晚些时候看到 Foundation 有一个获取特殊目录列表的函数。该函数对于开发 Mac OS 和 iOS 应用程序很有用。

表 16.1 总结了一些处理文件的 `NSFileManager` 方法。在表中，`path`、`path1`、`path2`、`from` 都是 `NSString` 对象；`attr` 是一个 `NSDictionary` 对象；`err` 是 `NSError` 的指针，你可以提供它以获取特定错误的详细信息。如果你为 `err` 指定 `NULL`，将采取默认操作，对于返回 `BOOL` 的方法，操作成功则返回 YES，失败则返回 NO。我们在本章中不会深入讨论这个对象。

