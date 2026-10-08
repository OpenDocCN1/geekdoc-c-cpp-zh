
这是一个原始类型（primitive），并且无论原始类型的类型如何都能工作。你可以将其封装在一个宏中，但如果你这样做，请注意不要传递一个带有副作用的表达式。

请注意，你必须传递指向原始值的指针。此方法将使用类型编码来确定该原始类型的大小，然后对其进行拷贝。

通常情况下，你会使用其他构造构造函数之一。例如，如果你想从一个整数创建一个 `NSNumber` 实例，可以这样做：

```
NSNumber *twelve = [NSNumber numberWithInt: 12];
```

生成的对象可以添加到集合中。与 `NSValue` 不同，`NSNumber` 实例是有序的因此你可以对包含 `NSNumber` 实例的集合进行排序。

`numberArray.m` 示例将一组 `NSNumber` 实例存储在数组中，然后使用 `-compare:` 选择器对其进行排序。从输出可以看出，无论数字是如何创建的，排序都是强制执行的。

# 第 5 章：数字

```
NSArray *a = [NSArray arrayWithObjects:
[NSNumber numberWithUnsignedLongLong:
ULLONG_MAX],
[NSNumber numberWithInt: -2],
[NSNumber numberWithFloat: 300.057],
[NSNumber numberWithInt: 1],
[NSNumber numberWithDouble: 200.0123],
[NSNumber numberWithLongLong: LLONG_MIN]
nil];
NSArray *sorted =
[a sortedArrayUsingSelector:@selector(compare:)];
NSLog("%%@", sorted);
```

来自：numberArray.m

```
2010-03-15 14:50:48.166 a.out[51465:903] (
"-9223372036854775808",
"-2",
1,
"200.0123",
"300.057",
18446744073709551615
)
```

输出来自：numberArray

## 执行小数算术

```
NSDecimalNumber *one = [NSDecimalNumber one];
NSDecimalNumber *fortyTwo = [NSDecimalNumber decimalNumberWithString:"42"];
NSDecimalNumber *sum = [one decimalNumberByAdding:fortyTwo];
NSDecimalNumber accumulator = [sum decimalValue];
NSDecimalNumber temp = [fortyTwo decimalValue];
NSDecimalMultiply(&accumulator, &accumulator, &temp, NSRoundPlain);
temp = [one decimalValue];
NSDecimalAdd(&accumulator, &accumulator, &temp, NSRoundPlain);
NSDecimalNumber *result = [NSDecimalNumber decimalNumberWithString:accumulator];
```

来自：decimal.m

C 语言提供了两种处理数字的选项：整数和浮点值。

浮点值由两个部分组成：尾数和指数。它们的值是 2 的幂乘以尾数。

浮点值的问题在于它们是二进制的。这意味着它们的精度是根据二进制位定义的，而这并不总是你想要的。例如，对于金融应用程序，你可能需要精确存储到四位小数的金额。这通过浮点值是不可能的；像 0.1 这样的值无法用任何有限的二进制浮点表示，就像三进制的 0.1（三分之一）无法用任何有限的十进制序列一样。

二进制数一组二的幂的和，就像十进制数是十的幂的和一样。对于分数值，小数点后的数字表示二分之一、四分之一、八分之一等。如果你尝试通过相加二的幂来创建一个 0.1 的值，你永远不会成功，尽管你会越来越接近。当你尝试通过相加十的幂来创建一个三分时（三十分之一，加上百分分之一，再加上千分之一，等等），也会发生同样的情况。

一种解决方案是使用定点算术。与其存储美元，你可能存储分之百分。这时你必须记住归一化你的值，并且你受到整数类型范围的限制。Objective-C 提供了另一种选项：小数浮点类型。

`NSDecimal` 类型是一个表示小数值的 C 结构体。由于有点奇怪的是，没有用于创建这些类型的 C API。你必须创建一个 `NSNumber` 实例，然后向它发送一个 `-decimalValue` 消息。

然后你有两种进行算术运算的选择。`NSNumber` 实例是不可变的。你可以根据算术结果创建新实例——例如，向其中发送 `decimalNumberByAdding:` 消息。

或者，你可以使用 C API，它可以直接修改结构体的值。如果你只执行一次算术操作并将结果存储在对象中，第一种方案更简单。如果你正在执行多个步骤，那么使用 C API 会更快。因为它们修改了结构体，所以你不需要为每个中间步骤创建一个新对象。

**注意：** C11 标准包含了小数类型，某些编译器作为扩展支持这些类型。`NSDecimal` 类型与这些不兼容。在大多数平台上，这并不重要。如果你目标是像 IBM 的 POWER6 这种具有小数算术硬件的设备，那么直接使用小数类型更好。

这两者都不是特别快。小数表示为数字数组，在两个数字归一化后，对它们进行成对操作。你可以预期获得与软件浮点实现类似的性能——可能稍差一点，因为 `NSDecimal` 没有被广泛使用，因此它不是许多优化的重点。

`NSNumber` 是 `NSNumber` 的子类，因此我们在下一节中查看的所有将 `NSNumber` 转换为字符串的方法都能按预期工作。你也可以使用访问数字对象上的标准方法将它们转换为 C 原始类型，但这些方法可能会截断或近似小数值。

## 字符串与数字之间的转换

```
int answer = [@"42" intValue];
NSString *answerString = [NSString stringWithFormat:@"%d", answer];
NSNumber *boxedAnswer = [NSNumber numberWithInt:answer];
XCTAssert([answerString isEqualToString:[boxedAnswer stringValue]], @"两个字符串应该是相同的");
```

来自：stratum.m

在数字和字符串之间转换有多种方法。许多表示简单数据的对象都有如 `-intValue` 的方法，用于返回整数表示。`NSString` 有这一系列中的几个方法。如果你有一个包含数值的字符串，你可以向它发送 `-doubleValue`、`-floatValue`、`-intValue` 或 `-longValue` 消息来将其转换为这些类型中的任何一种。在 64 位安全的 Foundation 版本中，你还可以向它发送 `-integerValue` 消息。这将返回 `NSInteger`。

有几种方法反过来，即从整数获取字符串。我们在第 6 章中查看一种：`NSString` 的 `+stringFormat:` 方法可以让你从原始类型构造字符串，就像使用 `sprintf()` 一样。如果你已经有一个 `NSNumber` 实例中的数字，有两种获取字符串的方法，其中一种是另一种封装。`-descriptionWithLocale:` 方法根据指定的区域设置生成字符串。实际上，它本身并不执行翻译。它向新的 `NSString` 发送 `initWithFormat:locale:` 消息。格式字符串取决于数字类型：例如，双精度数字将使用 `%0.16g` 格式字符串。这使用最多 16 位有效数字和所需的指数。

小数点分隔符取决于区域设置。如果你向 `NSNumber` 发送 `-stringValue` 消息，这等同于将 `nil` 作为参数发送 `-descriptionWithLocale:` 消息。这使用规范区域设置，这意味着没有任何本地化，因此结果在任何平台上都是相同的。

## 从字符串读取数字

```
NSScanner *parser = [NSScanner scannerWithString:@"1 plus 2"];

int operands[2];
NSString *operation;

[parser setCharactersToBeSkipped:[CharacterSet whitespaceCharacterSet]];

[parser scanInt:operands[0]];
[parser scanCharactersFromSet:[CharacterSet letterCharacterSet] toString:&operation];
[parser scanInt:operands[1]];
```

来自：scanner.m

任何 C 程序员首先学习使用的两个函数是 `printf()` 和 `scanf()`。这两个函数非常非常相似——一个几乎是另一个的反面——它们让你能够构造格式化字符串并从中解析数据。我们已经见过 `NSString` 有一个 `sprintf()` 的粗略物，所以你可以从格式字符串和变量构造字符串，但 Objective-C 的 `sscanf` 等价物是什么？给定字符串如何解析值？答案在于 `NSScanner` 类。这个类是一个非常强大的分词器。你创建一个附加字符串的 `NSScanner` 实例，然后一个接一个从从中扫描值。

你发送给扫描器的消息都具有
