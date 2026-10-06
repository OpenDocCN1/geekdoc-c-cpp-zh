
这是一个名为 Foo 的类的简单定义，它包含三个实例变量——其中一个是 `NSString`，另一个是 `int`，第三个是 `float`。该类有一个 setter 方法、三个 getter 方法，以及两个用于归档的编码/解码方法。

```
@interface Foo: NSObject <NSCoding>

@property (copy, nonatomic) NSString *strVal;
@property int intVal;
@property float floatVal;
@end
```

实现文件如下：

```
@implementation Foo

@synthesize strVal, intVal, floatVal;

-(void) encodeCoder:(NSCoder *)encoder {
    [encoder encodeObject:strVal forKey:@"strVal"];
    [encoder encodeInt:intVal forKey:@"intVal"];
    [encoder encodeFloat:floatVal forKey:@"floatVal"];
}

-(id) initWithCoder:(NSCoder *)decoder {
    strVal = [decoder decodeObjectForKey:@"strVal"];
    intVal = [decoder decodeIntForKey:@"intVal"];
    floatVal = [decoder decodeFloatForKey:
```

```
@"floatVal"];
  return self;
}
@end
```

编码程序首先使用之前所示的 `encodeObject:forKey` 方法对字符串值 `strVal` 进行编码。

在程序 19.8 中，创建了一个 Foo 对象，将其归档到文件，解归档然后显示。

## 程序 19.8. 测试程序

```
#import <Foundation/Foundation.h>
#import "Foo.h" // 我们的 Foo 类定义

int main (int argc, char * argv[]) {
  @autoreleasepool {
    Foo *myFoo = [[Foo alloc init];
    Foo *myFoo2;

    [myFoo setStrVal:@"This is the string"];
    [myFoo setIntVal: 12345];
    [myFoo setFloatVal: 98.6];

    [NSKeyedArchiver archiveRootObject:myFooToFile:@"foo.arch"];

    myFoo2 = [NSKeyedUnarchiver unarchiveObjectWithFile:@"foo.arch"];
    NSLog("%@\n%i\n%g", [myFoo2 strVal], *)
```

```
[myFoo2 intVal],
      [myFoo2 floatVal]];
  }
  return 0;
}
```

## 程序 19.8. 输出

```
This is the string
12345
98.6
```

以下消息归档了对象中的三个实例变量：

```
[encoder encodeObject: strVal forKey:
@"strVal"];
[encoder encodeInt: intVal forKey:
@"intVal"];
[encoder encodeFloat: floatVal forKey:
@"floatVal"];
```

一些基本数据类型（如 `char`、`short`、`long` 和 `long long`）未列在表 19.1 中；你必须确定数据对象的大小并使用适当的例程。例如，一个 `short int` 通常是 16 位，`int` 和 `long` 可以是 32 或 64 位，而 `long long` 是 64 位。（你可以使用第 13 章“底层 C 语言特性”中描述的 `sizeof` 运算符来确定任何数据类型的大小。）因此，为了归档一个 `short int`，先将其存储在 `int` 中，然后使用 `encodeIntForKey:` 进行归档。反转该过程以获取：使用 `decodeIntForKey:` 然后将其赋值给你的 `short int` 变量。

## 使用 NSData 创建自定义归档

你可能不想像上一个程序示例那样使用 `archiveRootObject:ToFile:` 方法直接将对象写入文件。例如，也许你可能想收集部分或所有对象并将它们存储在单个归档文件中。你可以在 Objective-C 中使用数据类 `NSData` 来此，我们在第 16 章“处理文件”中简要介绍过该类。

正如第 16 章提到的，`NSData` 对象可以预留一块内存，你可以在其中存储数据。该数据区域的典型用途可能是写入文件，或者存储从磁盘读取的文件内容。创建一个可变数据区域简单的方法是使用 `data` 方法：

```
dataArea = [NSMutableData data];
```

这创建了一个空缓冲区，其大小随着程序的执行而按需要扩展。

作为一个简单的示例，假设你想将地址录和一个 Foo 对象归档到同一个文件中。假设在本例中，你已经为 `AddressBook` 和 `AddressCard` 类添加了键值归档方法（参见程序 19.9）。

## 程序 19.9

```
#import "AddressBook.h"
#import "Foo.h"

int main (int argc, char * argv[])
{
```

```
@autoreleasepool {
  Foo *myFoo = [[Foo alloc] init];
  NSMutableData *dataArea;
  NSKeyedArchiver *archiver;
  AddressBook *myBook;

// 插入程序 19.7 中的代码以创建地址录
// 在 myFoo 中包含四张地址卡

[myFoo setStrVal:@"This is the string"];
[myFoo setIntVal:12345];
[myFoo setFloatVal: 98.6];

// 设置区域并连接一个 NSKeyedArchiver 到它
dataArea = [NSMutableData data];
archiver = [[NSKeyedArchiver alloc] initWithWritingData:dataArea];

// 归档数据区域中的对象
[archiver encodeObject:myBook:@"addrbook"];
[archiver encodeObject:myFoo:@"fool"];

// 将数据区域写入文件
if ([dataArea writeToFile:@"foo.arch" atomically:YES]) {
    NSLog(@"Archiving success!");
} else {
    NSLog(@"Archiving failed!");
}
  }
}
```
