
原本指向 `_firstName` 的偏移量现在指向 `_dateOfBirth`。任何硬编码了偏移量的代码最终都会读取到错误的值。为了说明该值，图 2.1 显示了在假设指针为 4 字节的情况下，在添加 `_dateOfBirth` 实例变量前后的类内存布局。

使用在编译时计算偏移量的代码在类定义改变时除非重新编译，否则就会崩溃。例如，库中可能存在使用旧类定义的代码。如果与使用新类定义的代码链接，运行时将出现不兼容性。各种语言发明了多种技术。Objective-C 采用的方法是通过让类对象（更多关于类对象请见项目 14）存储偏移量来使实例变量变得特殊。然后在运行时，会查找偏移量，这样如果类定义改变，偏移量就会更新；每当访问实例变量时，都会使用正确的偏移量。你甚至可以在运行时向类添加实例变量。这被称为

## 项目 6：理解属性

非脆弱的应用二进制接口（ABI）。ABI 定义了（其他事情）代码如何生成的约定。非脆弱的 ABI 也意味着实例变量可以在类延续分类（class-continuation category，见项目 27）或实现中定义。因此，你不需要再在接口中声明所有的实例变量，因此你不会在公共接口中泄露关于你实现的内部信息。

| Person | | Person | |
|---|---|---|---|
| +0 | `_firstName` | +0 | `_dateOfBirth` |
| +4 | `_lastName` | +4 | `_firstName` |
| +8 | `_someInternalData` | +8 | `_lastName` |
| | +12 | `_someInternalData` |

**图 2.1** 添加另一个实例变量前后的类数据布局

鼓励使用访问器方法而不是直接访问实例变量是克服这一问题的另一个因素。属性由实例变量支持，但它们提供了一种整洁的抽象。你可以自己编写访问器，但在真正的 Objective-C 风格中，访问器遵循严格的命名模式。由于这种严格的命名，可以引入一种语言结构来提供自动创建访问器方法的方法。这就是 `@property` 语法的出现的地方。

你在对象接口的定义中使用属性来提供访问对象所封装的数据的标准手段。因此，属性也可以被认为是简写，表示将为具有给定类型和给定名称的变量提供访问器。例如，考虑以下类：

```objc
@interface EOCerson : NSObject
@property NSString *firstName;
@property NSString *lastName;
@end
```

# 第 2 章：对象、消息传递与运行时

对于类的使用者来说，这等同于编写以下类：

```objc
@interface EOCerson : NSObject
- (NSString*)firstName;
- (void)setFirstName:(NSString*)firstName;
- (NSString*)lastName;
- (void)setLastName:(NSString*)lastName;
@end
```

使用属性时，你使用点语法，类似于在纯 C 中访问栈分配结构体的成员。编译器将点语法转换为对访问器的调用，就像你直接调用它们一样。因此，使用点语法和直接调用访问器之间绝对没有区别。下面的代码示例显示了等效性：

```objc
EOCerson *aPerson = [Person new];
```

```objc
aPerson.firstName = @"Bob"; // 等同于：
[aPerson setFirstName:@"Bob"];
```

```objc
NSString *lastName = aPerson.lastName; // 等同于：
NSString *lastName = [aPerson lastName];
```

但属性不仅如此。如果你允许，编译器将通过名为自动合成（autosynthesis）的过程为你编写这些方法的代码。需要注意的是，是编译器在操作，所以你不会在编辑器中看到合成方法的源码。在生成代码的同时，编译器还会向类添加一个实例变量，其类型为所需的类型，名称为属性名前加上下划线。在前面的示例中，会有两个实例变量：`_firstName` 和 `_lastName`。可以在类的实现中使用 `@synthesize` 语法来控制此实例变量的名称，例如：

```objc
@implementation EOCerson
@synthesize firstName = _myFirstName;
@synthesize lastName = _myLastName;
@end
```

使用 `synthesize` 语法将产生名为 `_myFirstName` 和 `_myLastName` 的实例变量，而不是默认值。从默认值更改实例变量名称是不常的；然而，如果你不喜欢使用下划线方法来命名实例变量，可以使用它来按你的 own命名。

## 第 6 项：理解属性

你想要的属性。但我鼓励你使用默认的命名方案，因为如果每个人都遵循相同的约定，代码对所有人来说都是可读的。

如果你不希望编译器为你合成访问器方法（accessor methods），你可以自己实现这些方法。然而，如果你只实现了其中一个访问器，编译器仍然会为你合成另一个。停止其自动合成的另一种方法是使用 `dynamic` 关键字，它告诉编译器不要自动创建实例变量来支持属性，也不要为你创建访问器。此外，在编译访问该属性的代码时，编译器将忽略访问器尚未定义的这一事实，并信任它们在运行时是可用的。例如，这在对 CoreData 的 `NSManagedObject` 进行子化时用到，访问器是在运行时动态创建的。`NSManagedObject` 选择这种方法是因为这些属性并不是实例变量。数据来自于所正在使用的任何数据库后端。

```objc
@interface EOCPerson : NSManagedObject
@property NSString *firstName;
@property NSString *lastName;
@end
```

```objc
@implementation EOCPerson
@dynamic firstName, lastName;
@end
```

在这个类中，将不会合成任何访问器或实例变量。当你尝试访问任何一个属性时，编译器也不会发出警告。

### 属性属性

你应该注意的属性另一个方面是所有可以用于控制编译器生成的访问器的属性。使用三个属性的示例所示：

```objc
@property (nonatomic, readwrite, copy) NSString *firstName;
```

属性可以分为四类。

### 子性 (Atomicity)

默认情况下，合成的访问器包含锁定以确保它们是原子性的。如果你提供了 `nonatomic` 属性，则不使用锁定。请注意，虽然没有 `atomic` 属性（缺少 `nonatomic` 属性即假认为 `atomic`），但如果你想显式指定，仍然可以应用它，而不会产生编译器错误。如果你自己定义访问器，你应该提供指定的原子性。

#### 读/写 (Read/Write)

- `readwrite`: 同时提供 getter（get）和 setter（set）。如果属性是合成的，编译器将生成这两个方法。
- `readonly`: 仅提供 getter（get），且编译器仅在属性是合成时才会生成它。如果你只想从外部读取该属性，但在类扩展分类（class-continuation category）中内部将其重新声明为读/写，则可能需要使用。更多信息请参见第 27 项。

#### 内存管理语义 (Memory-Management Semantics)

属性封装数据，数据需要具体的所有权语义。这只影响 setter。例如，setter 应该是保留（retain）新值，还是将其赋值给底层实例变量？当编译器合成访问器时，它使用这些属性来决定为你编写什么代码。如果你创建了自己的访问器，必须遵守你为该属性所指定的规范。

- `assign`: setter 是一个简单的赋值操作，用于标量类型，如 `CGFloat` 或 `NSInteger`。
- `strong`: 这表示属性定义了所有权关系。当设置新值时，首先保留新值，然后释放（release）旧值，最后设置值。
- `weak`: 这表示属性定义了非所有权关系。当设置新值时，不会保留新值，也不会释放旧值。这与 `assign` 的作用相似，但当属性指向的对象在任何时候被销毁时，该值也会置为 nil。
- `unsafe unretained`: 语义与 `assign` 相同，但用于对象类型，以表示一种非所有权（untained）关系，且在目标被销毁时不会置为 nil（unsafe），这与 `weak` 不同。
- `copy`: 这表示了一种类似于 `strong` 的所有权关系；然而，它不是保留值，而是复制值。这通常用于类型为 `NSString*` 时以保持封装，因为传入 setter 的值可能是子类 `NSMutableMutableString` 的实例。如果是这种可变体，该值在属性设置后可能会发生变化，而对象对此不知情。因此，取一个不可变的副本以确保字符串不会在对象下方发生变化。任何可能是可变的对象都应该进行拷贝。

### 方法名称 (Method Names)

可以使用以下属性控制访问器方法的名称：

- `getter=<name>`: 指定 getter 的名称。这种方法通常用于布尔属性，你希望 getter 以 `is` 为前缀。例如，在 `UISwitch` 类中，开关开启或关闭的属性定义如下：

```objc
@property (nonatomic, getter=isOn) BOOL isOn;
```

- `setter=<name>`: 指定 setter 的名称。这种方法并不常用。

你可以使用这些属性对合成的访问器进行细粒度的控制。但你应该注意，如果你实现了自己的访问器，你应该自己确保它们遵循指定的属性。例如，声明为 `copy` 的属性应该确保在 setter 中获取对象的副本。否则，该属性的使用者会产生错误的印象，并可能因为未遵守约定而引入 bug。

即使在其他可能设置该属性的方法中，确保你遵守属性定义中规定的语义也是重要的。例如，考虑 `EOCPerson` 类的扩展。它将属性的内存管理语义声明为 `copy`，因为该值可能是可变的。它还添加了一个初始化器来设置姓和名的的初始值：

```objc
@interface EOCPerson (EOC)
@property (copy, readonly) NSString *firstName;
@property (copy, readonly) NSString *lastName;

- (id)initWithFirstName:(NSString *)firstName lastName:(NSString *)lastName;
@end

@implementation EOCPerson (EOC)
- (id)initWithFirstName:(NSString *)firstName lastName:(NSString *)lastName {
    if ((self = [super init])) {
        _firstName = [firstName copy];
        _lastName = [lastName copy];
    }
    return self;
}
@end
```

## 项目 7：在内部访问时直接访问成员变量

当另一个线程同时对其写入数据时，可能会产生不同的值。

因此，你通常希望在 iOS 上使用 `nonatomic` 属性。

但在 Mac OS X 上，你通常不会发现 `atomic` 属性访问是性能瓶颈。

## 需要记住的

- `@property` 语法提供了一种定义对象封装数据的方法。
- 使用属性（attributes）为被存储的数据提供正确的语义。
- 确保在任何设置属性的底层成员实例变量的地方，都遵循声明的语义。
- 在 iOS 上使用 `nonatomic`，因为如果使用 `atomic`，性能会受到严重影响。

# 项目 7：在内部访问时主要直接访问成员变量

外部应该始终使用属性来访问对象的成员变量，但在内部如何访问成员变量是 Objective-C 社区中一个备受激烈讨论的话题。有些人建议始终使用属性来访问成员变量，有些人建议始终直接访问成员变量，而我强烈建议你通过直接访问读取成员变量，但通过属性设置它们，尽管有几点注意事项。

考虑以下类：

```objc
@interface EOCerson : NSObject
@property (nonatomic, copy) NSString *firstName;
@property (nonatomic, copy) NSString *lastName;

// 用于 firstName + " " + lastName 的便利方法：
- (NSString*)fullName;
- (void)setFullName:(NSString*)fullName;
@end
```

便利方法 `fullName` 和 `setFullName` 可能这样实现：

```objc
- (NSString*)fullName {
    return [NSString stringWithFormat:"%@ %@", self.firstName, self.lastName];
}
```

# 第 2 章：对象、消息传递与运行时

```objc
/**
 假设所有全名恰好有 2 个部分。
 * 方法可以重写以支持更
 * 特的名字。
 */
```

```objc
(void)setFullName:(NSString*)fullName {
    NSArray *components = [fullName componentsSeparatedString:@" "];
    self.firstName = [components objectAtIndex:0];
    self.lastName = [components objectAtIndex:1];
}
```

在 getter 和 setter 中，我们都通过访问器方法（使用属性点语法）访问成员变量。假设你重写了这两个方法来直接访问成员变量：

```objc
(NSString*)fullName {
    return [NSString stringWithFormat:@"%@ %@", _firstName, _lastName];
}
```

```objc
(void)setFullName:(NSString*)fullName {
    NSArray *components = [fullName componentsSeparatedString:@" "];
    _firstName = [components objectAtIndex:0];
    _lastName = [components objectAtIndex:1];
}
```

这两种风格存在差异。

- 对成员变量的访问无疑会更快，因为它们不需要通过 Objective-C 方法分发（见项目 11）。编译器将产生直接访问存储对象成员变量内存位置的代码。
- 这种访问绕过了 setter 定义的属性内存管理语义。例如，如果你的属性被声明为 `copy`，直接设置成员变量将不会触发拷贝。新值将被保留（retain），而旧值将被释放（release）。
- 直接访问成员变量时，不会触发键值观察（KVO）通知。这在某些情况下可能是一个问题，也可能不是，取决于你希望你的对象如何表现。
- 通过属性访问可以让你更容易地调试属性周围的代码，因为你可以在 getter 和/或 setter 中添加断点，以确定是谁在何时访问了属性。

一个很好的折中方案是使用 setter 写入成员变量，并使用直接访问读取。这样做的好处是读取速度快，且不会失去通过属性写入的控制力。通过 setter 写入的最重要原因是你将确保内存管理语义得到维护。然而，这种方法有几点注意事项。

第一个注意事项是在初始化方法中设置值时。在这里，你应该始终使用直接成员变量访问，因为子类可能会重写 setter。考虑 `OCPerson` 有一个子类 `OCSmithPerson`，它被设计仅用于姓为 "Smith" 的人。该子类可能会这样重写 `lastName` 的 setter：

```objc
- (void)setName:(NSString*)lastName {
    if (![lastName isEqualToString:"Smith"]) {
        [NSException raiseWithName:@"InvalidNameException" format:@"Name must be Smith"];
    }
    _lastName = lastName;
}
```

# 第 2 章：对象、消息传递与运行时

## 需要记住的

- `@property` 语法提供了一种定义对象封装数据的方法。
- 使用属性（attributes）为被存储的数据提供正确的语义。
- 确保在任何设置属性的底层成员实例变量的地方，都遵循声明的语义。
- 在 iOS 上使用 `nonatomic`，因为如果使用 `atomic`，性能会受到严重影响。

## 项目 8：理解相等性

来自 `NSObject` 类本身的这些方法的默认实现是：两个对象相等当且仅当它们的指针值相同。要理解如何为自己的对象重写这些方法，理解其约定是重要的。任何通过 `isEqual:` 方法判断相等的对象必须从 `hash` 方法返回相同的值。然而，两个 `hash` 方法返回相同值的对象并不一定相等。

剩下的就是哈希方法了。回想这个约定：相等的对象必须返回相同的哈希值，但具有相同哈希值的对象并不一定相等。因此，重写 `isEqual:` 是至关重要的。一个完全可以的哈希方法如下：

```objc
(NSUInteger)hash {
    return 1337;
}
```
