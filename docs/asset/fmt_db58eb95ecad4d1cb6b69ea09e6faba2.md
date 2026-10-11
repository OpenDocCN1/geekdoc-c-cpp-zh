
# Glossary

### Application Kit
用于开发应用程序用户界面的框架，包括菜单、工具栏和窗口等对象。它是 Cocoa 的一部分，更常被称为 `AppKit`。

### ARC
参见 [Automatic Reference Counting（自动引用计数）](#automatic-reference-counting)。

### archiving（归档）
将对象数据的表示转换为稍后可以恢复（反归档）的格式。

### array（数组）
值的有序集合。数组可以被定义为基础 Objective-C 类型，并在 Foundation 中作为对象实现。

### delegate（代理）
一个旨在由另一个对象执行动作的对象。

### designated initializer（指定初始化器）
类中或子类（通过向父类发送消息）中所有其他初始化方法将调用的方法。

### dictionary（字典）
在 Foundation 中通过 `NSMutableDictionary` 和 `NSDictionary` 类实现的键值对集合。

### directive（指令）
在 Objective-C 中，以 `@` 符号开头的特殊结构。`@interface`、`@end` 和 `@class` 都是指令的示例。

### Distributed Objects（分布式对象）
一个应用程序中的 Foundation 对象与另一个应用程序（可能运行在另一个机器上）中的 Foundation 对象通信的能力。

### dynamic binding（动态绑定）
在运行时确定要调用的方法，而不是在编译时。

### dynamic typing（动态类型）
在运行时确定对象所属的类，而不是在编译时。参见 static typing（静态类型）。

### encapsulation（封装）
参见数据封装。

### extern variable（外部变量）
参见全局变量。

### factory method（工厂方法）
参见类方法。

### factory object（工厂对象）
参见类对象。

### formal protocol（正式协议）
一组在 `@protocol` 指令声明的名称下分组的相关方法。不同的类（不一定相关）可以通过实现（或继承）其所有要求的方法来采用正式协议。参见 informal protocol（非正式协议）。

### forwarding（转发）
将消息及其相关参数发送到另一个方法进行执行的过程。

### Foundation framework（Foundation 框架）
一组类、函数和协议，构成了应用程序开发的基础，提供了基本设施，如内存管理、文件和 URL 访问、存档以及处理集合、字符串、数字和日期对象的任务。

### framework（框架）
一组相关的类、函数、协议、文档、头文件和其他资源的集合。例如，Cocoa 框架用于在 Mac OS X 下开发交互式图形应用程序。

### function（函数）
一个由名称标识的语句块，可以接受通过值传递给的一个或多个参数，并可选地返回一个值。函数可以是定义所在文件的局部（静态）函数，也可以是全局函数此时它可以从其他文件的函数或方法中调用。

### garbage collection（垃圾回收）
一种运行时内存管理系统，会自动释放未引用的对象所使用的内存。iOS 运行时环境不支持垃圾回收。

### gcc
由自由软件基金会（FSF）开发的编译器名称。`gcc` 支持许多编程语言，包括 C、Objective-C 和 C++。`gcc` 是 Mac OS X 中用于编译 Objective-C 程序的标准编译器。

### gdb
用于 `gcc` 编译的程序的标准调试工具。

### getter method（get 方法）
一种获取实例变量值的访问器方法。参见 setter method（set 方法）。

### global variable（全局变量）
定义在任何方法或函数之外的变量，可以通过同一源文件中的任何方法或函数访问，也可以从将变量声明为 `extern` 的其他源文件访问。

### header file（头文件）
一个包含常用定义、宏和变量声明的文件，通过 `#import` 或 `#include` 语句包含在程序中。

### id
一种可以持有任何类型对象指针的通用对象类型。

### immutable object（不可变对象）
其值不能修改的对象。Foundation 框架中的示例包括 `NSString`、`NSDictionary` 和 `NSArray` 对象。参见 mutable object（可变对象）。

### implementation section（实现部分）
类定义中的部分，包含在相应接口部分（或按协议定义）中声明方法的实际代码（即实现）。

### informal protocol（非正式协议）
一组声明为分类的逻辑相关方法，通常是作为一个分类，非正式协议中的所有方法并不需要实现。参见 formal protocol（正式协议）。

### inheritance（继承）
从根对象开始将方法和实例变量从类传递给子类的过程。

### instance（实例）
类的具体表示。实例是通常通过向类对象发送 `alloc` 或 `new` 消息创建的对象。

### instance method（实例方法）
可以由类的实例调用的方法。参见 class method（类方法）。

### instance variable（实例变量）
声明在接口部分（或继承自父类）的变量，包含在对象的每个实例中。实例方法可以直接访问它们的实例变量。

### Interface Builder（接口构建器）
Mac OS X 下用于为应用程序构建图形用户界面的工具。

### interface section（接口部分）
用于声明类及其父类、实例变量和方法的部分。对于每个方法，还声明了参数类型和返回值。参见 implementation section（实现部分）。

### internationalization（国际化）
参见 localization（本地化）。

### isa
在根对象中定义的特殊实例变量，所有对象都继承它。`isa` 变量用于在运行时识别对象所属的类。

### linking（链接）
将一个或多个对象文件转换为可执行程序的过程。

### local variable（局部变量）
作用范围限制在定义它的块中的变量。变量可以是方法、函数或语句块的局部的。

### localization（本地化）
使程序适合在特定地理区域内执行的过程，通常通过将消息翻译成本地语言并处理时区、货币符号、日期格式等事情。有时 *localization* 仅指语言翻译，而 *internationalization* 术语指过程的其余部分。

### message（消息）
方法及其相关参数发送给对象（接收者）。

### message expression（消息表达式）
封装在方括号中的表达式，指定了对象（接收者）和要发送给该对象的消息。

### method（方法）
属于类的过程，可以通过向类对象或从类类的实例发送消息来执行。参见 [class method]()[instance method]。

### mutable object（可变对象）
其值可以更改的对象。Foundation 框架支持可变和不可变的数组、集合、字符串和字典。参见 [immutable object]().

### nil
一个类型为 `id` 的对象，用于表示无效对象。它的值被定义为 `0`。`nil` 可以接收消息。

### notification（通知）
向已注册在特定事件发生时接收提醒的对象发送消息的过程。

### NSObject
Foundation 下的根对象。

### null character（空字符）
值为 `0` 的字符。空字符常量用 `'\0'` 表示。

### null pointer（空指针）
无效的指针值，通常定义为 `0`。

### object（对象）
一组变量和相关方法。可以向对象发送消息以执行其任一方法。

### object-oriented programming（面向对象编程）
一种基于类和对象的编程方法，并在这些对象上执行操作。

### parent class（父类）
另一个类继承的类。也称为超类。

### pointer（指针）
引用另一个对象或数据类型的值。指针实现为特定对象的地址。类的实例是指内存中对象位置的指针。

### polymorphism（多态）
不同类的对象接受相同消息的能力。

### procedural programming language（过程化语言）
一种通过定义一组操作数据的过程和函数来定义程序的语言。

### property declaration（属性声明）
为实例变量指定属性的方法，允许编译器为实例变量生成无泄漏且线程安全的访问器方法。属性声明还可以用于为将在运行时动态加载的访问器方法声明属性。

### preprocessor（预处理器）
一个对源代码进行第一遍处理的程序，处理以 `#` 开头的行，这些行可能包含预处理语句。常见用途包括使用 `#define` 定义宏，使用 `#import` 和 `#include` 其他源文件，以及使用 `#if`、`#ifdef` 和 `#ifndef` 条件地包含源行。

### property list（属性列表）
标准格式的不同类型对象的表示。属性列表通常以 XML 格式存储。

### protocol（协议）
类为了遵循或采用必须实现的方法列表。协议提供了一种跨类的标准接口。参见 formal protocol（正式协议） informal protocol（非正式协议）。

### receiver（接收者）
接收消息的对象。在被调用的方法内部，接收者可以称为 `self`。

### reference count（引用计数）
对象被引用的次数。通过向对象发送 `retain` 消息增加，通过向其发送 `release` 消息减少。

### root object（根对象）
继承层次结构中没有父类的顶层对象。

### runtime（运行时）
程序执行的时间；也负责执行程序指令的机制。

### selector（选择器）
用于选择对象要执行方法的名称。编译后的选择器类型为 `SEL`，可以使用 `@selector` 指令生成。

### self
在方法内部使用的变量，用于引用消息的接收者。

### set
一个无序的唯一对象集合，在 Foundation 中通过 `NSSet`、`NSMutableSet` 和 `NSCountedSet` 类实现。

### setter method（setter 方法）
设置实例变量值的访问方法。参见 getter method（getter 方法）。

### statement（语句）
一个或多个以分号终止的表达式。

### statement block（语句块）
用大括号括起来的一个或多个语句，其作用域限于该语句块。

### static function（静态函数）
使用 `static` 关键字声明的函数，只能由同一源文件中定义的其他函数或方法调用。

### static typing（静态类型）
在编译时显式识别对象所属的类。参见 dynamic typing（动态类型）。

### static variable（静态变量）
作用域限于其定义的块或模块的变量。静态变量默认初始值为 `0`，并在方法或函数调用期间保留其值。

### structure（结构）
一种聚合数据类型，可以赋值给其他类型的结构。它可以作为参数传递给函数和方法，并由它们返回。

### subclass（子类）
也称为子类，子类继承其父类或超类的方法和实例变量。

### super
在方法中使用的关键字，用于引用接收者的父类。

### super class（超类）
特定类的父类。参见 super。

### synthesized method（合成方法）
编译器自动为你创建的 setter 方法或 getter 方法。它是在 Objective C 2.0 语言中引入的。

### UIKit
一个用于为 iOS 设备开发应用程序的框架。除了提供用于处理窗口、按钮和标签等常用 UI 元素的类外，它还定义了处理加速度计和触控界面等设备特定功能的类。`UIKit` 是 Cocoa Touch 的一部分。

### Unicode character（Unicode 字符）
一种表示包含数百万个字符字符集的标准。`NSString` 和 `NSMutableString` 类处理包含 Unicode 字符的字符串。

### union（联合体）
一种聚合数据类型，例如包含共享存储区域成员的结构体。在任何时刻，这些成员中只有一个可以占用该存储区域。

### Xcode
一种用于 Mac OS X 和 iOS 程序开发的编译和调试工具。

### XML（可扩展标记语言）
在 Mac OS X 上生成的属性列表（property lists）的默认格式。

### zone（区域）
用于分配数据和对象的指定内存区域。程序可以使用多个区域来更高效地管理内存。

# 附录 B. 通讯录应用程序源代码

供你参考，这里你在第二部分“Foundation 框架”中使用的通讯录示例的完整接口和实现文件。这包括 `AddressCard` 和 `AddressBook` 类的定义。你应该在你的系统上实现这些类；然后扩展类定义以使其更加实用和强大。这是你学习该语言并熟悉构建程序、处理类与对象以及操作 Foundation 框架极极方法。

## AddressCard 接口文件

```objc
#import <Foundation/Foundation.h>

@interface AddressCard : NSObject <NSCopying, NSCCoding>

@property (nonatomic, copy) NSString *name, *email;

-(void) setName:(NSString*) theName andEmail:(NSString*) theEmail;
-(void) assignName:(NSString *) theName andEmail:(NSString *) theEmail;
-(NSComparisonResult) compareNames:(id) element;

-(void) print;

@end
```

## AddressBook 接口文件

```objc
#import <Foundation/Foundation.h>
#import "AddressCard.h"

@interface AddressBook: NSObject <NSCopying, NSCoding>

@property (nonatomic, copy) NSString *bookName;
@property (nonatomic, strong) NSMutableArray *book;

- (id) initWithName:(NSString *) name;
- (void) sort;
- (void) addCard:(AddressCard *) theCard;
- (void) sortCard;
- (void) removeCard:(AddressCard *) theCard;
- (int) entries;
- (void) list;
- (AddressCard *) lookup:(NSString *) theName;

@end
```

## AddressCard 实现文件

```objc
#import "AddressCard.h"

@implementation AddressCard

@synthesize name, email;

-(void) setName: (NSString *) theName andEmail:
(NSString *) theEmail
{
    self.name = theName;
    self.email = theEmail;
}

// 比较指定地址卡中的两个名称
-(NSComparisonResult) compareNames: (id) element
{
    return [name compare: [element]];
}

-(void) print
{
    NSLog("@===============================================");
    NSLog("@| (@| %-31s |", [name UTF8String]);
    NSLog("@| %-31s |", [email UTF8String]);
    NSLog("@|                               |");
    NSLog("@|                               |");
    NSLog("@|                               |");
    NSLog("@|               O               O               |");
    NSLog("@===============================================");
}

    return self;
}
@end
```

## AddressBook 实现文件
