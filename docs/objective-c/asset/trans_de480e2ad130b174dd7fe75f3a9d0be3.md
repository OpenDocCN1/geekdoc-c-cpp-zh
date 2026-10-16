

# 使用 NSData 和 NSMutableData

在处理二进制数据块时，Foundation 为你提供了 NSData 和 NSMutableData 类，以便以面向对象的方式操作该数据。这些类可以管理缓冲区的分配和释放，并且还提供了一个对象包装器，以便将数据存储在集合类中。它们还提供了将数据写入文件和通过套接字通信传输数据的接口。

## 创建 NSData 对象

你可以通过使用之前已分配的现有低级数据结构，或通过从支持 NSCopying 协议的任何其他类型的 Objective-C 对象复制数据来创建 NSData 对象。

要使用 C 数据结构中的原始字节创建 NSData 对象，你可以使用工厂方法 +dataWithBytes:length:，它接受指向数据缓冲区的指针，然后将该数据缓冲区中的字节复制到 NSData 对象中。如果你更喜欢直接访问缓冲区内部的字节，而不复制它们，你可以使用工厂方法 +dataWithBytesNoCopy:length:，它也会构造一个 NSData 对象，但不会复制数据，从而导致一个 NSData 对象，其缓冲区直接访问你提供的原始内存。在这种情况下，所提供的字节必须使用 malloc 分配，因为 NSData 对象在释放时将使用 free 函数释放字节。由于 NSMutableData 允许你对其中的数据进行修改，因此在指向外部分配的缓冲区时这样做会导致问题，因此在使用 NSMutableData 时，无论你是否指定复制，对象都会复制字节。清单 14.5 显示了使用预分配的字节缓冲区创建 NSData 对象的示例。

### Listing 14.5
### 创建一个 NSData 对象

```
char *buf = malloc(1024);

NSData *data = [NSData dataWithBytes:buf length:1024];
```

NSData 对象最常见的用途之一是访问存储在文件或 Internet 上的资源中的字节。你可以使用工厂方法 +dataWithContentsOfFile: 轻松地创建包含文件内容的 NSData 对象，它将要读取的文件路径作为其参数。要执行相同的操作但使用来自 Internet 的资源，你可以使用工厂方法 +dataWithContentsOfURL:。此方法将使用提供的 URL 中的提供协议访问 Internet 并下载资源，并将该资源的原始数据作为 NSData 对象的原始数据提供。像往常一样，就像这些便捷方法的大多数情况一样，下载过程将阻塞当前线程，直到完成，因此请谨慎使用此方法。NSData 还提供了用于将数据写入磁盘的方法 -writeToFile:atomically: 和 -writeToURL:atomically:。其中后一种方法仅支持写入本地文件 URL。每个方法都将一个次要参数作为是否以原子方式写入文件。这在你写入的数据特别大的情况下尤其重要，因为你的应用程序可能在写入数据过程中终止。这可能导致磁盘上的文件损坏。atomic 参数指定文件将首先写入临时文件，并在文件操作完成后，临时文件将被复制到最终位置。通过使用此标志，你可以确信原始文件只有在替换文件已成功完全写入时才会被覆盖。

## 访问 NSData 对象中的原始字节

NSMutableData 类为包含你想要操作字节的 NSData 对象提供了一个面向对象的接口。你可以使用方法 -appendBytes:length: 和 -appendData: 向其中添加字节；你可以使用方法 -replaceBytesInRange:withBytes: 替换字节；你还可以使用方法 -setLength: 来截断或扩展 NSMutableData 缓冲区。如果你只想将缓冲区的特定部分清零（将其字节设置为 0），你可以使用方法 -resetBytesInRange:。这为你提供了按需操作文件和结构中的原始数据的所有工具。清单 14.6 显示了如何使用此功能从磁盘读取文件，修改特定字节，然后将其写回磁盘。在这种情况下，所涉及的文件是一个遗留游戏数据存档文件，它使用硬编码的文件格式，其中特定值存储在数据中的特定位置。

### Listing 14.6
### 修改游戏存档文件的原始字节

```
int goldOffset = 617; // at location 617 in the file
int goldLength = 4; // 4 bytes are used for storing the gold

NSRange goldRange = NSMakeRange(goldOffset, goldLength);
NSMutableData *gameData = [NSMutableData dataWithContentsOfFile:@"..."];

[gameData replaceBytesInRange:goldRange withBytes:newGoldValue];
[gameData writeToFile:@"..." atomically:YES];
```

正如你所见，`NSData` 为访问原始数据提供了一个非常方便的低级接口。它还为将该数据存储在集合类中提供了一个方便的包装器，就像 `NSNumber` 和 `NSValue` 一样。

## Summary

本章的目的是向你介绍一些使处理非标准 Objective-C 数据变得更容易的类。它们在处理集合时特别方便，正如你在第 13 章中看到的那样，集合仅适用于 Objective-C 对象。这些类为该低级数据提供了一个非常简单的包装器，以便你可以在集合类中使用它们，并利用 Objective-C 的面向对象功能。我们生活在一个充满边缘条件和遗留数据的世界。Objective-C 为任何语言提供了最干净、最集成的遗留数据接口之一。其 C 语言根源使其特别适合此任务。

# 处理时间和日期

在计算机上处理日期传统上是一个复杂的问题。日期尽管看起来如此，实际上并不像看上去那么简单。它们充满了异常和边缘条件，例如闰年、日历变更等等。对该主题的全面考虑表明，即使考虑到这些异常，仍然存在关于日历应追溯多远以及如何处理落在该边界之前的日期等问题。CE/BCE 标准是我们习惯的，实际上是一个相当无效的权宜之计。

如果你需要更多关于处理日期有多困难的证明，请回想一下本世纪初计算行业经历的 Y2K 问题。 naive 的程序员之前认为他们可以用只有两位数字来表示日期中的年份。当世纪标记滚动时，数百万行代码不得不重写。

即使现在，我们也面临着由于大多数计算机使用 32 位整数作为自 1970 年 1 月 1 日以来的秒数计数来存储其日期而导致的未来日期问题。不幸的是，这个计数器将在 2032 年左右溢出。虽然这可能看起来很遥远，但我提醒你，程序员在编写他们的两位数字年份处理代码时对 2000 年说了同样的话。

即使你忽略这些更大的问题，仍然存在如何在应用程序中正确处理日期和时间这一非常实际的问题。例如，你如何处理确定一周持续时间的小时数。你对这个问题的第一反应可能只是将一天中的小时数乘以七。这将是一个典型但天真的反应。但如果其中一天是我们从夏令时更改为标准时间或反之的日子呢？现在你的计算突然变得不正确了。

这类问题在软件开发中非常常见，并导致了一些非常高调的错误，这些错误造成了数百万美元的公关损害和客户问题。不要成为那个程序员。

## In This Chapter

- 使用 NSDate 和 NSCalendar 操作日期
- 处理时间间隔
- 本地化日期

