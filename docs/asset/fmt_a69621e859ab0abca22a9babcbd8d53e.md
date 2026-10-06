
- `(id)initWithCoder:(NSCoder *)decoder`

```objc
{
    bookName = [decoder decodeObjectForKey:@AddressBookBookName];
    book = [decoder decodeObjectForKey:@AddressBookBook];
    return self;
}
```

## 编写编码解码方法

接下来的测试程序为程序 19.6。

## 程序 19.6 测试程序

```objc
#import "AddressBook.h"

int main(int argc, char * argv[]) {
    @autoreleasepool {
        NSString *aName = "Julia Kochan";
        NSString *aEmail = "@jewls37@axlc.com";
        NSString *bName = "Tony Iannino";
        NSString *bEmail = "@tony.iannino@techfitness.com";
        NSString *cName = "@Stephen Kochan";
        NSString *cEmail = "@steve_steve_kochan.com";
        NSString *dName = "@Jamie Baker";
        NSString *dEmail = "@jbaker@gmail.com";

        AddressCard *card1 = [[AddressCard alloc] init];
        AddressCard *card2 = [[AddressCard alloc] init];
        AddressCard *card3 = [[AddressCard alloc] init];
        AddressCard *card4 = [[AddressCard alloc] init];

        AddressBook *myBook = [[AddressBook alloc] init];

        // 第一设置四张地址卡
        [card1 setName:aName andEmail:aEmail];
        [card2 setName:bName andEmail:bEmail];
        [card3 setName:cName andEmail:cEmail];
        [card4 setName:dName andEmail:dEmail];

        [myBook initWithName:aName];

        // 带有地址卡的通讯录存档
        [myBook addCard:card1];
        [myBook addCard:card2];
        [myBook addCard:card3];
        [myBook addCard:card4];

        [NSKeyedArchiver archiveObject:myBook toFile:@"addressbook"];

        // 从文件中反存档通讯录
        AddressBook *decodedBook = [NSKeyedUnarchiver unarchiveObjectFromFile:@"addressbook"];

        // 显示反存档的通讯录的内容
        [decodedBook print];
    }
    return 0;
}
```

## 442 第19章 归档

```objc
Foo *myFoo2;
```

```objc
myFoo.strVal = @"This is the string";
myFoo.intVal = 12345;
myFoo.floatVal = 98.6;
[NSKeyedArchiver archiveRootObject:myFoo toFile:@"foo.arch"];
myFoo2 = [NSKeyedUnarchiver unarchiveObjectFile:@"foo.arch"];
NSLog(@"%@\n%@", myFoo2.strVal, myFoo2.intVal, myFoo2.floatVal);
return 0;
```

## 程序 19.8 输出

```
This is the string
12345
98.6
```

以下消息对对象进行归档：

```objc
[encoder encodeObject:strVal forKey:@"FoostrVal"];
[encoder encodeInt:intVal forKey:@"FoointVal"];
[encoder encodeFloat:floatVal forKey:@"FloatVal"];
```

某些数据类型（如 `char`, `short`, `long` 和 `long long`）未列在表 19.1 中；你必须确定你的数据对象的类型并使用适当的例程。例如，`short` 通常是 16 位，`int` 和 `long` 可以是 32 或 64 位，而 `long` 是 64 位。（你可以使用第 13 章“底层语言特性”中描述的 `sizeof` 运算符创建一个 `short int`，首先将其存储在 `int` 中，然后使用 `encodeIntForKey` 对其进行归档。反转过程以获取它：使用 `decodeIntForKey` 并将其赋值给你的 `short int` 变量。）

## 使用 NSData 创建自定义归档

你可能不会使用 `archiveRootObject:ToFile:` 方法直接将对象写入文件，就像我们在之前的示例中所做的那样。例如，你可能想收集部分或全部对象，并将它们存储在单个归档文件中。你可以在 Objective-C 中使用名为 `NSData` 的数据类来实现，这在第 16 章“处理文件”中简要提到过。

正如第 16 章提到的，`NSData` 对象可以用于预留内存区域，你可以在其中存储数据。该数据区域的典型用途可能是提供临时数据，随后将其写入文件，或者可能持有从磁盘读取的文件内容。创建可变数据区域最简单的方法是使用数据方法：

```objc
dataArea = [NSMutableData data];
```

这创建了一个空缓冲区，其大小在程序执行过程中根据需要进行扩展。

作为一个简单的示例，假设你想将你的通讯录和其中一个 `Foo` 对象归档在同一个文件中。在本例中，假设你已经为 `AddressBook` 和 `AddressCard` 类添加了键归档方法（程序 19.9）。

## 程序 19.9

```objc
#import "AddressBook.h"
#import "Foo.h"

int main (int argc, char *argv[]) {
    @autoreleasepool {
        Foo *myFoo = [[Foo alloc] init];
        NSMutableData *dataArea;
        NSKeyedArchiver *archiver;
        AddressBook *myBook;

        // 插入程序 19.7 中的代码以创建一个包含四个地址卡的
        // 通讯录，存储在 MyBook 中
        myFoo.strVal = @"This is the string";
        myFoo.intVal = 12345;
        myFoo.floatVal = 98.6;

        // 设置数据区域并将其连接到 NSKeyedArchiver
        dataArea = [NSMutableData data];
        archiver = [[NSKeyedArchiver alloc] initForWritingWithMutableData:dataArea];

        // 现在我们可以开始归档对象
        [archiver encodeObject:myBook forKey:@"@myaddbook"];
        [archiver encodeObject:myFoo forKey:@"@foo"];

        [archiver finishEncoding];

        // 将归档的数据区域写入文件
        if ([dataArea writeToFile:@"@Archive" atomically:YES] == NO) {
            NSLog(@"Archiving failed!");
        }
    }
    return 0;
}
```

## 444 第19章 归档

分配一个 `NSKeyedArchiver` 对象时，通过发送 `initForWritingWithMutableData` 消息来指定写入归档数据的区域；这就是你之前创建的 `NSMutableData` 数据 `dataArea`。存储在 `archiver` 中的 `NSKeyedArchiver` 对象现在可以向程序中的对象发送归档消息了。事实上，在收到 `finishEncoding` 消息之前，它会归档并存储指定区域中的所有消息。

这里这里有两个对象需要编码：第一个是你的通讯录，第二个是 `Foo` 对象。你可以对这些对象使用 `encodeObject:forKey:`，因为你之前已经为 `AddressBook`、`AddressCard` 和 `Foo` 类实现了编码器和解码器方法。（理解这个概念很重要。）

当你完成两个对象的归档后，向归档器发送 `finishEncoding` 消息。此后不能再编码任何对象，你需要发送此消息来完成归档过程。

你设置并命名为 `dataArea` 的区域现在包含了你归档的对象，其格式可以写入文件。消息表达式

```objc
dataArea write:@"myArchive" atomically:YES
```

该该表达式向你的数据流发送 `writeToFile:atomically:` 消息，要求其将其数据写入命名为 `myArchive` 的指定文件。

从语句可以看出，`writeToFile:atomically:` 方法在操作成功时返回 `BOOL`，在失败（可能是指定了无效的文件路径或文件系统已满）时返回 `NO`

这些都在程序 19.10 中

## 程序 19.10

```objc
#import "AddressBook.h"
#import "Foo.h"

int main(int argc, char *argv[]) {
    @autoreleasepool {
        Foo *myFoo = [[Foo alloc] init];
        NSMutableData *dataArea;
        NSKeyedArchiver *archiver;
        AddressBook *myBook;

        // 假设这里已经创建了 myBook 并填充数据
        // ... (省略部分逻辑以匹配上下文)
        dataArea = [NSMutableData data];
        archiver = [[NSKeyedArchiver alloc] initForWritingWithMutableData:dataArea];

        [archiver encodeObject:myBook forKey:@"@myaddbook"];
        [archiver encodeObject:myFoo forKey:@"@foo"];

        [archiver finishEncoding];

        if ([dataArea writeToFile:@"@Archive" atomically:YES] == NO) {
            NSLog(@"Archiving failed!");
        }
    }
    return 0;
}
```
