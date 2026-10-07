

# property list

**property list (属性列表)** 一种以标准化格式表示不同类型对象的表示。属性列表通常以 XML 格式存储。

**statement (语句)** 以分号结尾的一个或多个表达式。

**protocol (协议)** 类必须实现或适配协议时所包含的方法列表。协议提供了一种跨类标准接口的方法。另请参见正式协议和非正式协议。

**statement block (语句块)** 括在在大括号内的一个或多个语句。可以在语句块内声明局部变量，其作用范围限于该块。

**receiver (接收者)** 接收消息的对象。在调用它的方法内部，接收者可以被称为 *self*。

**static function (静态函数)** 使用 `static` 关键字声明的函数，只能由同一源文件的其他函数或方法调用。

**retain count (引用计数)** 参见 retain count。

**static typing (静态类型)** 在编译时显式地标识对象所属的类。也称为动态类型。

**retain count (引用计数)** 对象被引用的次数。通过向对象发送 *retain* 消息来增加，通过向其发送 *release* 消息来减少。

**static variable (静态变量)** 其作用范围局限于定义它的块或模块。静态变量具有默认初始值 0，并在方法或函数调用期间保持其值。

**root object (根对象)** 继承层次结构中没有父类的顶层对象。

**structure (结构体)** 一种可以包含不同类型成员的聚合数据类型。结构体可以赋值给其他结构体，作为参数传递给函数并被返回。

**runtime (运行时)** 程序执行的时间；也是负责执行程序指令的机制。

**subclass (子类)** 也称为 *child class*，子类继承其父类或超类的方法和实例变量。

**selector (选择器)** 用于为对象选择方法的名称。编译后的选择器类型为 *SEL*，可以使用 `@selector` 指令生成。

**super** 在方法中使用的关键字，用于指代接收者的父类。

**self** 在方法内部使用的变量，用于指代消息的接收者。

**super class (父类)** 特特定类的父类。参见 *super*。

**set (集合)** 一种唯一对象的无序集合，通过 Foundation 中的 NSSet、NSMutableSet 和 NSCounted 类实现。

**synthesized (合成的)** 编译器自动为你创建的 setter 或 getter。它被添加到 Objective C 2.0 语言中。

**setter (set 方法)** 设置实例变量值的访问器方法。参见 *getter* 方法。

**UIKit** 一个用于为 iOS 设备开发应用程序的框架。除了提供处理窗口、按钮和标签等常用 UI 元素的类外，它还定义了处理设备特定功能（如加速度计和触摸界面）的类。UIKit 是 Cocoa Touch 的一部分。

**Unicode character (Unicode 字符)** 用于表示包含数百万字符集合的标准。NSString 和 NSMutable 类处理包含 Unicode 字符的字符串。

**union (联合体)** 一种聚合数据类型，例如包含共享相同存储区域成员的结构体。在任何时刻，这些成员中只有一个可以占用该存储区域。

**Xcode** 用于在 Mac OS X 上程序开发的编译和调试工具。

**XML** 可扩展标记语言。Mac OS X 上生成的属性列表的默认格式。

**zone (区域)** 用于分配数据和对象的指定内存区域。程序可以处理多个区域来更高效地管理内存。

## 附录 B

## 通讯录源码

为了供你参考，这里是你在第二部分“Foundation 框架”中一直使用的通讯录示例的完整接口和实现文件。这包含了 AddressCard 和 AddressBook 类的定义。你应该在你的系统中实现这些类；扩展类定义以使其更具实用性和更强大。这是你学习语言、熟悉构建程序、处理类和对象以及使用 Foundation 框架的极佳方式。

### AddressCard 接口文件

```objc
@import <Foundation/Foundation.h>

@interface AddressCard : NSObject <NSCopying, NSCoding> {
    NSString *name;
    NSString *email;
}

@property (nonatomic, copy) NSString *name, *email;

-(void)setName:(NSString *)theNameAndEmail:(NSString *)theEmail;
-(void)retainName:(NSString *)theNameAndEmail:(NSString *)theEmail;
-(NSComparisonResult)compareNames:(id)id:(id)element;

-(void)print;

@end
```

### AddressBook 接口文件

```objc
#import <Foundation/Foundation.h>
#import "AddressCard.h"
```

```objc
@interface AddressBook: NSObject <NSCopying, NSCopying>
{
    NSString *book;
}

@property (nonatomic, copy) NSString *book;

-(id)initWithWithName:(NSString *)name;
-(void)sort;
-(void)addCard:(AddressCard *)theCard;
-(void)removeCard:(AddressCard *)theCard;
-(int)entries;
-(void)list;
-(AddressCard *)lookup:(NSString *)theName;

@end
```

### AddressCard 实现文件

```objc
#import "AddressCard.h"

@implementation AddressCard

-(void)setName:(NSString *)theNameAndEmail:(NSString *)theEmail {
    _name = theName;
    _email = theEmail;
}

-(void)retainName:(NSString *)theNameAndEmail:(NSString *)theEmail {
    [_name retain theName];
    [_email retain theEmail];
}

-(NSComparisonResult)compareNames:(id)id:(id)element {
    return [_name compare:element];
}

-(void)print {
    NSLog("Name: %@, Email: %@", _name, _email);
}

-(id)copy {
    AddressCard *copy = [super copy];
    if (copy) {
        copy.name = [_name copy];
        copy.email = [_email copy];
    }
    return copy;
}

-(void)encodeWithWithCoder:(NSCoder *)encoder {
    [encoder encodeObject:_name forKey:@"name"];
    [encoder encodeObject:_email forKey:@"email"];
}

-(id)initWithWithCoder:(NSCoder *)decoder {
    self = [super initWithCoder:decoder];
    if (self) {
        _name = [decoder decodeObjectForKey:@"name"];
        _email = [decoder decodeObjectForKey:@"email"];
    }
    return self;
}

-(void)dealloc {
    [_name release];
    [_email release];
    [super dealloc];
}

@end
```

### AddressBook 实现文件

```objc
#import "AddressBook.h"

@implementation AddressBook

-(id)initWithWithName:(NSString *)name {
    self = [super init];
    if (self) {
        bookName = [[NSString alloc] initWithName:name];
        book = [[NSMutableArray alloc] init];
    }
    return self;
}

-(void)sort {
    [book sortUsingSelector:@selector(compareNames)];
}

-(void)addCard:(AddressCard *)theCard {
    [book addObject:theCard];
}

-(void)removeCard:(AddressCard *)theCard {
    [book removeObjectIdenticalTo:theCard];
}

-(int)entries {
    return [book count];
}

-(void)list {
    NSLog("Contents of %@ %@", bookName);
    for (AddressCard *theCard in book) {
        NSLog("%-20s %-32s", [theCard.name UTF8String], [theCard.email UTF8String]);
    }
}

-(AddressCard *)lookup:(NSString *)theName {
    for (AddressCard *nextCard in book) {
        if ([nextCard name] caseInsensitiveCompare:theName) {
            return nextCard;
        }
    }
    return nil;
}

-(void)dealloc {
    [bookName release];
    [book release];
    [super dealloc];
}

@end
```

