

将所有内容整合起来，代码如下所示：

```objectivec
int i;
NSArray *theArray;
NSString *name1;
NSString *name2;
NSString *name3;
NSString *name4;

// assign values to the four names
name1 = @"Maria";
name2 = @"Mercedes";
name3 = @"Leopold";
name4 = @"Frederick";

// create and populate the array
theArray = [NSArray arrayWithObjects:name1, name2, name3, name4, nil];

NSLog(@"object1 = %@", [theArray objectAtIndex:0]);
NSLog(@"object2 = %@", [theArray objectAtIndex:1]);
NSLog(@"object3 = %@", [theArray objectAtIndex:2]);
NSLog(@"object4 = %@", [theArray objectAtIndex:3]);

i = [theArray count];
NSLog(@"theArray count = %d", i);
```

输出结果看起来像这样：

```text
2008-07-28 04:45:54.518 CocoaData2[944]  object1=Maria
2008-07-28 04:45:54.520 CocoaData2[944]  object2=Mercedes
2008-07-28 04:45:54.520 CocoaData2[944]  object3=Leopold
2008-07-28 04:45:54.520 CocoaData2[944]  object4=Frederick
2008-07-28 04:45:54.520 CocoaData2[944]  theArray count = 4
```

### **NSMutableArray**

`NSArray` 类的一个缺点是，一旦创建后你就无法更改它。如果你不能更改某些东西（例如数组），那么它就是*不可变的*。相反，那些可以更改的则是*可变的*数组。因此，Cocoa 还提供了 `NSMutableArray`。要创建一个 `NSMutableArray`，你可以使用其 `arrayWithCapacity` 方法：

```objectivec
NSMutableArray *theArray = [NSMutableArray arrayWithCapacity:0];
```

因为你随时可以扩展或缩小 `NSMutableArray` 数组的大小，所以使用零个项目的空间来创建数组是安全的。

![](img/ea40cad434a338535474e82c1a6ace20_213_0.png)

使用 **NSMutableArray**，你可以在创建它之后更改数组中的元素。这使得它更适合维护动态的信息列表：

- **向 NSMutableArray 添加项目：** 使用 `addObject` 方法：

  ```objectivec
  [theArray addObject:name1];
  [theArray addObject:name2];
  [theArray addObject:name3];
  ```

- **从数组中移除项目：** 使用 `removeObjectAtIndex` 方法。此方法从数组中移除一个对象，并在过程中调整数组大小。例如，要移除第二个名称（位于 `index 1`），可以使用如下代码：

  ```objectivec
  [theArray removeObjectAtIndex:1];
  ```

- **插入一个对象：** 使用 `insertObject` 方法。该方法将一个对象插入数组，并随之调整数组大小。此示例将第二个名称（`name2`）重新插入到数组中：

  ```objectivec
  [theArray insertObject:name2 atIndex:1];
  ```

- **用另一个对象替换数组中的元素：** 使用 `replaceObjectAtIndex:withObject:` 方法。此代码片段将数组中的第二个名称替换为 name3：

  ```objectivec
  [theArray replaceObjectAtIndex:1 withObject:name3];
  ```

因为 **NSMutableArray** 继承自 **NSArray**，你可以使用本节前面介绍的方法来查找数组的大小并查询特定元素。

# 处理布尔数据类型

布尔数据类型表示只能处于两种状态且仅限两种状态的信息。例如，开/关开关以布尔方式运行，因为你只有两个选项。是/否问题的运作方式类似。Objective-C 拥有自己的布尔数据类型：**BOOL**。除了通常的 **TRUE** 和 **FALSE** 值外，Objective-C 使用 **YES** 和 **NO**。此代码片段展示了你通常使用 **BOOL** 变量的一些方式：

```objectivec
BOOL answerWasFound;

answerWasFound = FindTheAnswer();

if (answerWasFound)
// 或者
if (answerWasFound == YES)
```

除了使用 Objective-C **BOOL** 类型的值 **YES** 或 **NO** 之外，出于另一个原因这也很重要：它可以与 Cocoa 中的其他对象协同工作。再次强调，数组和其他类型的集合对象期望其元素本身也是对象。如果你想在 Cocoa 中创建一个布尔值的 **NSArray**，你会将 **BOOL** 类型传递给 **NSNumber** 的 **numberWithBool** 类方法：

```objectivec
// create an NSNumber with a BOOL
n = [NSNumber numberWithBool:YES];

// add the NSNumber to an array
[theArray addObject:n];
```

# 处理日期

**NSCalendarDate** 类为你提供了许多处理日期和时间的选项。你执行的最常见的任务之一是查找当前日期或时间。你可以用一行代码通过 **NSCalendarDate** 类方法来完成这一点：

```objectivec
NSDate *theDate = [NSCalendarDate date];
```

获取此日期后，你可以轻松将其转换为适合显示的 **NSString**。只需使用 **description** 方法以标准国际格式显示日期。在此示例中，**NSLog** 在控制台显示日期：

```objectivec
NSLog(@"theDate = %@", [theDate description]);
```

这会产生类似这样的结果：

```text
theDate = 2008-08-05 05:08:13 -0500
```

**description** 方法对于快速粗略的日期显示来说是合适的，但有时你希望以更用户友好的格式显示日期。**descriptionWithCalendarFormat** 方法可以帮助你构建一个包含日期或时间的 **NSString**。**descriptionWithCalendarFormat** 方法有三个参数。第一个参数是你进行简单日期工作时唯一需要担心的参数。该参数是一个 **NSString**，以你希望的格式表示日期。

Cocoa 在格式化日期显示方面给你提供了很大的灵活性。例如，以下代码片段将日期格式化为你在美国可能预期的样子：

```objectivec
NSLog(@"theDate = %@",
      [theDate descriptionWithCalendarFormat:@"%A, %B %d, %Y (%I:%M)" timeZone:nil locale:nil]);
```

这会导致日期格式如下：

```text
theDate = Monday, August 04, 2008 (10:15)
```

传递给 descriptionWithCalendarFormat 方法的那个看起来奇怪的字符串决定了你想显示日期的哪些元素。Apple 将这些奇怪的字符称为日期转换说明符。每个说明符是一个单字母代码，对应日期的某个方面。在前面的示例中，%A 代表星期几的名称，在这种情况下是星期一。接下来是 %B，它代表月份的名称（在这种情况下是八月）。你可以继续将这些说明符串联起来，直到构建出你喜欢的日期格式。表 10-1 详细列出了某些更常见的说明符。

| 表 10-1 | 日期格式说明符 |
| :--- | :--- |
| **代码** | **它代表什么** |
| %B | 月份名称 |
| %m | 作为整数的月份 |
| %e | 作为整数的日期 |
| %d | 作为两位整数的日期 |
| %A | 星期几名称 |
| %I | 小时 |
| %M | 分钟 |
| %S | 秒 |
| %Y | 年份 |

**第二部分：即时 Cocoa 和 Objective-C 语言**

# 第三部分

# 综合应用：深入 Cocoa 编程

# 第五波

作者：Rich Tennant

![](img/ea40cad434a338535474e82c1a6ace20_218_0.png)

# 在本部分中……

你已经了解了开发者工具的工作原理，掌握了 Objective-C 语言，甚至已经构建了自己的应用程序。现在是时候更上一层楼了。

第三部分将你的 Cocoa 技能提升到新的高度。你将通过创建具有各种功能的程序来发现如何添加每个酷炫的 Cocoa 应用程序中都具有的功能，这些功能范围从文本和图形到音频和视频。每个 Mac 用户都期望应用程序能处理文件，因此第三部分也涵盖了这一点。

# 第 11 章

# 文本

# 本章内容

- 显示文本
- 更改文本样式
- 编辑文本
- 将文本保存到文件
- 打开并显示文本文件

自第一台 Macintosh 计算机以来，Apple 就在设计、布局和排版方面引领着消费级计算机世界。Mac OS X 通过提供你将在计算机显示器上看到的最美观的文本之一，延续了这一传统。Cocoa 让程序员可以即时访问 OS X 的这些精彩功能。

本章向你展示了如何为了多种目的处理文本。首先，你在窗口中显示一些文本。然后，你操纵这些文本，扭曲其大小并改变其色调。接下来，你会发现将专业文本编辑功能添加到你的应用程序中是多么简单，只需很少或没有代码。最后，你将界面中的文本保存到文件以便日后调用。风格化的文本是许多类型应用程序的一个很棒的功能，Cocoa 为你提供了一大堆操纵这些文本的工具。

# 处理文本

Cocoa 有许多不同的控件用于在应用程序中处理文本。一些文本控件将文本作为标签显示；其他控件允许像文字处理器那样的完全编辑。Interface Builder 提供了几种用于处理文本的控件，但它们通常继承自两种控件之一：

- **NSTextField**：显示静态或动态文本。使用此控件显示一行文本。
- **NSTextView**：Cocoa 中文本字段的明星。这个家伙可以处理多行文本。当你想到文字处理器时，就想到 NSTextView。

