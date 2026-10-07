

```objc
[myFoo setIntVal: 12345];
[myFooFloatVal: 98.6];
```

```objc
// 设置一个数据区域并将其连接到 NSKeyedArchiver 对象
dataArea [NSMutableData data];
archive [[NSKeyedArchiver alloc] initForWritingMutableData:dataArea];
// 现在我们可以开始归档对象了
archiver encodeObject:myBook forKey:@"myaddrbook";
archiver encodeObject:myFoo forKey:@"myfoo";
archiver finishEncoding];

// 将归档的数据区域写入文件
if ([dataArea writeToFile:@"myArchive" atomically:YES] NO)
    NSLog(@"Archiving failed");

[archiver release];

[myFoo release];
[pool drain];
return 0;
```

在分配了一个 `NSKeyedArchiver` 之后，消息 `initForWritingMutableData` 被发送到了你之前创建的数据区域；即 `NSMutableData` 区域 `dataArea`。存储在 `archiver` 中的 `NSKeyedArchiver` 对象现在可以向你程序中的对象发送消息了。事实上，在接收到 `finishEncoding` 消息之前，它会将所有消息归档并存储在指定的数据区域中。

这里有两个对象需要归档——第一个是你的地址录，第二个是你的 `Foo`。你可以对这些对象使用 `encodeObject:forKey:`，因为你之前已经为 `AddressBook`、`AddressCard` 和 `Foo` 类实现了编码器和解码器方法。（理解这一概念非常重要）。

当你完成这两个对象的处理时，向 `archiver` 发送 `finishEncoding` 消息。此后不能再有任何对象被归档，并且你需要发送此消息来完成归档过程。

你设置的名为 `dataArea` 的区域现在包含了你归档的对象，其格式可以被写入文件。消息表达式 `dataArea writeToFile:@"myArchive" atomically:YES` 向你的数据流发送 `writeToFile:atomically` 消息，要求它将数据写入你命名为 `myArchive` 的指定文件。
从语句中可以看出，`writeToFile:atomically` 方法返回一个 `BOOL` 值：操作成功返回 `YES`，失败则返回 `NO`（可能是指定了无效的文件路径或文件系统已满）。

从你的归档文件中恢复数据非常简单：你只需要反向操作即可。首先，你需要像之前一样分配一个数据区域。接下来，你需要将归档文件读取到数据区域；然后你必须创建一个 `NSKeyedUnarchiver` 对象并告诉它从指定区域解码数据。你必须调用 `decode` 来提取你的归档对象。完成后，你向 `NSKeyedUnarchiver` 对象发送 `finishDecoding` 消息。
所有这些操作都在程序 19.10 中完成。

## 程序 19.10

```objc
#import "AddressBook.h"
#import "Foo.h"

int main (int argc, char *argv[]) {
{
    NSAutorePool *pool = [NSAutorePool alloc init];
    NSData *dataArea;
    NSKeyedUnarchiver *unarchiver;
    Foo *myFoo;
    AddressBook *myBook;
    // 读取归档文件并将一个
    // NSKeyedUnarchiver 对象连接到它

    dataArea = [NSData dataWithContentsFile:@"myArchive"];

    if (!dataArea) {
        NSLog("Can't read back archive file!");
        return 1;
    }

    unarchiver = [[NSKeyedUnarchiver alloc] initForReadingWithData:dataArea];

    // 解码我们之前存储在归档中的对象
    myBook = [unarchiver decodeObjectForKey:@"myaddbook"];
    myFoo = [unarchiver decodeObjectForKey:@"myfoo"];

    [unarchiver finishDecoding];

    [unarchiver release];

    // 恢复是否成功
    [myBook list];
    NSLog("%@\n%@", [myBook strVal], [myFoo floatVal]);

    [pool release];
    return 0;
}
}
```

## 程序 19.10 输出

Steve 的地址录内容：
Jamie Baker jbaker@hitmail.com
Julia Kochan jewls337@axlc.com
Stephen Kochan steve@steve.kochan.com
Tony Iannino tony.iannino@techfitness.com

这是字符串
12345
98.6

输出验证了地址录和你的 Foo 对象已成功重新编码。

## 使用归档器进行拷贝

在程序 18.2 中，你尝试拷贝一个数组——你发现实际字符串并没有被拷贝，只有引用被拷贝了。你可以使用 Foundation 的功能创建深拷贝。程序 19.11

```objc
#import <Foundation.h>

int main (int argc, char *argv[]) {
{
    NSAutorePool *pool = [NSAutorePool alloc init];
    NSData *dataArea;
    NSKeyedUnarchiver *unarchiver;
    NSMutableArray *array2;
    NSString *mstr;

    // 这是关于 OCR 文本中描述的
    // 深拷贝逻辑的占位符。

    [pool release];
    return 0;
}
}
```

