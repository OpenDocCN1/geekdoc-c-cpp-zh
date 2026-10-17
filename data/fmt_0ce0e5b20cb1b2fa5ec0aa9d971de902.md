
对于实例出现在 Interface Builder 面板上的类，其并行角色存在一种例外。通用步骤是：在你的项目中定义该类，从 Interface Builder 面板将该对象拖到你的界面中，然后使用 Interface Builder Info 窗口中的“Custom Class”名称将该对象与你的子类关联。然而，在这种情况下，子类的 `initWithCoder:` 方法不会在反归档化期间被调用；相反，会发送一个 `init` 消息。你应该在 `awakeFromInit:` 中为自定义对象执行任何特殊设置，该方法会在 nib 文件中的所有对象反归档化后被调用。

# 属性的存储与访问

“属性”一词在 Cocoa 中既有通用含义，也有特定语言的含义。通用概念源于对象建模的设计模式。语言特定的含义则与声明属性（declared properties）特性有关。

正如[对象建模](page 167) 所描述，属性是对象的定义特征（在对象建模模式中称为*entity*），并且是其封装的数据。属性可以是两种类型之一：属性（attribute），例如标题和位置；或者是关系（relationship）。关系可以是一对一或一对多的，并且可以采取多种形式，例如输出（outlet）、代理（delegate）或其他对象的收集器。属性通常（但并非总是）存储为实例。

设计良好的类的一个整体策略部分，是强制执行封装。客户端不应直接访问存储属性的地方，而应通过类的接口来访问它们。访问对象属性的方法称为访问器方法（accessor methods，或简称为 accessor），用于设置对象属性的值。它们充当 getter（getters）的作用，调节对属性的访问并强制对象实例数据的封装。获取值的访问器方法是 getter，而设置属性值的方法是 setter 方法。

声明属性特性（在 Objective-2.0 中引入）对你控制属性访问的方式带来了变化，有些变化是细微的。声明属性是声明类属性 getter 和 setter 方法的简写。在实现块（implementation block）中，你可以请求编译器合成（synthesize）这些方法。正如[声明属性](page 61) 总结的，你在数据的 `@interface` 块中使用 `@property` 指令来声明属性。定义指定了属性的名称和类型，并可能包含告知编译器如何实现访问器方法的修饰符。

在设计类时，有几个因素影响你如何存储和访问类的属性。你可以选择使用声明属性并让编译器为你合成访问器方法。或者，你可以自己实现类的访问器方法；即使你使用了声明属性，这也是一个选项。另一个重要因素是你的代码是否运行在垃圾回收环境中。如果启用了垃圾回收，那么访问器方法的实现比在内存管理代码中要简单得多。接下来的章节描述了存储和访问属性的各种替代方案。

# 利用声明属性

除非你有极充分的理由反而行之，否则建议在新项目中使用 Objective-C 2.0 的声明属性，而不是手动编写所有的访问器方法。首先，声明属性让你从实现访问器方法的繁琐负担中解放出来。其次，通过让编译器为你合成访问器方法，你减少了编程错误发生的概率，并确保了类实现中更一致的行为。最后，声明属性的声明式风格使得你的意图对其他开发者来说可见。

基础子类设计

2010-12-13 | © 2010 Apple Inc. All Rights Reserved.

# 第 3 章

# 为 Cocoa 程序添加行为

你可能用 `@property` 声明某些属性，但仍需要为它们实现所有者方法（owner methods）。这样做的原因是希望该方法执行比简单的获取或设置属性值更多的操作。例如，该属性——一个大图像文件——必须从文件中加载，出于性能考虑，你希望你的 getter 延迟加载它（在第一次被请求时加载）。如果你因为这种原因需要实现访问器方法，请参见“实现访问器方法”（page 125）获取详情。你可以通过以下方式告诉编译器不要合成访问器方法：在类的 `@implementation` 块中指定属性但不指定 `@dynamic` 指令；或者对 `@dynamic` 属性不指定 `@synthesize` 指令（作为默认）；如果实现中已经存在此类方法且没有针对它的 `@synthesize` 指令，编译器将放弃合成访问器方法。

如果你的程序禁用了垃圾回收，你需要将属性声明限定为 `import`。默认情况下（`assign` 属性），合成的 setter 方法执行简单的赋值，这对于垃圾回收代码是合适的。在内存管理代码中，你必须在 setter 方法中保留（retain）或复制（copy）被赋值的对象；当你用 `retain` 或 `copy` 修饰符限定属性时，请告知编译器。注意，对于类遵循 `NSCopy` 协议的对象属性，你应该始终指定 `copy` 修饰符，即使启用了垃圾回收。

下面的示例说明了使用 `@interface` 块以及 `@implementation` 块中的 `@synthesize` 和 `@dynamic` 通过属性声明（带有不同的属性组合）可以实现的各种行为。以下代码指示编译器为声明的 `name` 和 `accountID` 属性合成访问器方法；由于 `accountID` 属性是只读的，编译器只合成一个 getter 方法。在这种情况下，假设已启用垃圾回收。

```
@interface MyClass : NSObject
NSString *name;
NSNumber *accountID;

@property (copy) NSString *name;
@property (readonly) NSNumber *accountID;
//
@end
@implementation MyClass
@synthesize name, accountID;
//
@end
```

示例中的属性声明告诉编译器 `preview` 是只读的，因此它不会寻找 setter。通过 `@implementation` 块中的 `@dynamic` 指令，它还指示编译器不要合成 getter，并提供了该方法的实现。

```
@interface MyClass : NSObject
NSImage *previewImage;
@property (readonly) NSImage *previewImage;
// ...
@end
@implementation MyClass
@dynamic previewImage {
    if (previewImage == nil) {
        // lazy加载图像并赋值给 ivar
    }
    return previewImage;
}
// ...
@end
```

示例中的属性声明告诉编译器 `currentHost` 具有 `retain` 修饰符，这指示编译器保留该值。

```
@interface MyClass : NSObject {
NSHost *currentHost;
Boolean hidden;
}
@property (retain, nonatomic) NSHost *currentHost;
```

基础子类设计

2010-12-13 | © 2010 Apple Inc. All Rights Reserved.

## 第3 章

为 Cocoa 程序添加行为

对于布尔属性，采用变体形式的 getter 方法是可以接受的。在这种情况下，它的形式为 `isAttribute`。例如，一个名为 `hidden` 的布尔类型实例变量将有一个 `isHidden` getter 方法和一个 `setHidden` setter 方法。

如果实例变量是标量类型（如 `int` 或 `float`），则访问器方法的实现通常非常简单。类型为 `float` 的实例变量 `currentRate` 在列表 3-5 显示了如何实现访问器方法。

### 列表 3-5 为标量实例变量实现访问器

```
(float)currentRate {
    return currentRate;
}
```

```
(void)setCurrentRate:(float)newRate {
    currentRate = newRate;
}
```

如果启用了垃圾回收，对于对象值属性的 setter 访问方法的实现也只是简单的赋值。列表 3-6 显示了你如何实现此类方法。

### 列表 3-6 为对象实例变量实现访问器（启用垃圾回收）

```
(NSString*)jobTitle {
    return jobTitle;
}
```

```
(void)setJobTitle:(NSString*)newTitle {
    jobTitle = newTitle;
}
```

当实例变量持有对象且未启用垃圾回收时，情况就会变得微妙。因为这些对象必须是持久的，并且在赋值时必须被创建、复制或保留。当 setter 访问器更改实例变量的值时，它只负责确保持久性，而不负责妥善处理旧值。getter 则将实例变量的值传递给请求的对象。鉴于 Cocoa 对象所有权策略的两个假设，这两种类型的访问器操作对内存管理都有影响：

- 从方法返回的对象（例如通过 getter 访问返回）在调用对象的作用范围内是有效的。换句话说，保证该对象在该作用范围内不会被释放或更改值。

- 当调用对象从方法作为访问器接收到一个对象时，除非它显式地保留（retain）或复制（copy）了该对象，否则不应释放该对象。

考虑到这两个假设，让我们看看名为 `title` 的 `NSString` 实例变量的 getter 和 setter 访问器的两种可能实现。列表 3-7 显示了第一种。

### 列表 3-7 为对象实例变量实现访问器——良好的技术

```
(NSString*)jobTitle {
    return jobTitle;
}
```

```
(void)setTitle:(NSString*)newTitle {
if (title != newTitle) {
    title autorelease;
    title = [newTitle copy];
}
}
```

注意，getter 访问器只是返回实例变量。相反，setter 访问器则很忙。在验证传入的实例变量值与当前值不同后，在复制新值之前对当前值进行自动释放。（向对象发送 `autorelease` 比发送 `release` 更“线程安全”）。然而，这种方法仍然存在潜在的危险。如果客户端正在使用 getter 返回的对象，而此时 setter 访问器自动释放了 `NSString` 对象，并在不久后该对象被释放并销毁，那么客户端对实例变量的引用将不再有效。

列表 3-8 显示了访问器方法的实现，该方法通过在 getter 中保留（retain）和自动释放（autorelease）实例变量来绕过这个问题。

### 列表 3-8 为对象变量实现访问器——更好的技术

```
(NSString *)title {
    return [[self retain] autorelease];
}
(void)setTitle:(NSString *)newTitle {
    if (title != newTitle) {
        [title autorelease];
        title = [newTitle copy];
    }
}
```

在上述两个 setter 方法示例（列表 3-5 和列表 3-7）中，新的 `NSString` 变量是被复制的而不是保留的。通用规则是：如果没有被保留，你就应该复制它。如果一个实例是一个值对象——即代表字符串、日期、数字或记录等内容的对象——你应该复制它。换句话说，你想要该对象的自己的副本。

然而，如果要存储和访问的对象是一个对象实体（例如 `UIView` 或 `NSWindow`），你应该保留它。实体的开销更高且具有关联性，复制它们可能是昂贵的。判断一个对象是值对象还是实体的一种方法，是决定你感兴趣的是对象的值还是对象本身。如果你感兴趣的是值，它就是一个值对象，你应该复制它（当然，假设该对象符合 `NSCopy` 协议）。

在 setter 中决定保留还是复制实例变量的另一种方法，是确定实例是属性（attribute）还是关系（relationship）。这对于模型对象特别有用，模型对象是代表应用程序数据的对象。属性本质上与值对象相同：它是封装该对象的定义特征，例如颜色（`NSColor`）或标题。另一方面，关系仅仅是如此：保留与一个或多个对象的关系（通过引用）。通常情况下，在 setter 方法中，你复制属性的值并保留关系。然而，关系具有基数（cardinality）；它们可以是一对一或一对多的。一对多关系（通常由集合对象，如 `NSArray` 实例表示表示）可能需要 setter 方法执行一些比简单保留实例变量之外的操作。详情请参阅《模型对象实现指南》。关于作为属性或关系的对象属性，请参阅“键值机制”（第 128 页）。

# 第 3 章

为 Cocoa 程序添加行为

要使子类的每个属性都符合键值编码（key-value coding）的要求，请执行以下操作之一：

- 对于命名为 `key` 的属性或一对一关系，请实现命名为 `key`（getter）和 `setKey:`（setter）的访问器方法。例如，如果你有一个名为 `salary` 的属性，你将拥有 `salary` 和 `setSalary:` 访问器方法（如果编译器合成了声明的属性，它会遵循此模式，除非另有规定）。

- 对于一对多关系，如果基于基于一个集合的实例变量（例如 `NSArray` 对象）或返回集合的实例方法，请让 getter 方法的名称与属性相同（例如 `employees`）。如果该属性是可变的，则 getter 方法不应返回一个可变集合（如 `NSMutableArray`）；你必须实现 `insertObject:forKeyAtIndex:` 和 `removeObjectForKeyIndex:`。如果该实例不是集合且 getter 方法没有返回集合，则你必须实现其他 `NSObjectCoding` 方法。

要使你的对象符合 KVO（键值观察）规范，请确保你的对象符合 KVC（键值编码）规范；如果你对自动通知满意，你可以选择实现手动键值观察，这需要额外的工作。

> **进阶阅读：**阅读《键值编程指南》和《键值观察指南》以了解更多关于这些技术。关于使用 KVC、KVO 和 [绑定 (Mac OS X)](第 187 页) 的 Cocoa 绑定技术总结，请参阅[对象间的通信](第 175 页)中的相关章节。

# 对象基础设施

如果子类设计良好，该类的实例的行为将符合 Cocoa 对象的预期。使用该对象的代码可以与该类的其他实例进行比较，发现其内容（例如在调试器中），并对对象执行基本操作。

自定义子类应该实现（即使不是全部）以下根类和绑定协议方法：

- **isEqualTo:** 和 **hash:**—实现这些 `NSObject` 方法，以为它们的比较引入某些特定对象的逻辑。例如，如果你通过序列号拥有你的类的实例，那么等等的依据是什么？欲更多信息请参阅[自省](第 87 页)。

- **description**—实现此 `NSObject` 方法以返回一个简要描述对象属性或内容的字符串。该信息由调试器中的打印对象返回，并用于字符串中的 `%@` 格式化对象。例如，如果你有一个具有名称、日期、部门和位置 ID 属性的假设 `Employee` 类。该类的 `description` 方法应该如下所示：

- **copyWithZone:**—如果你向子类的客户端暴露拷贝其实例的能力，则你应该实现 `NSCopying` 协议的此方法。值对象（包括模型对象）是拷贝的典型候选者；而 `UIView` 和 `NSColor` 则不是。如果你的类实例是可变的，你应该遵守 `NSMutableCopying` 协议。

- **initWithCoder:** 和 encodeCoder:—如果你预计你的类实例会被归档（例如，使用模型类），你应该采用 `NSCoding` 协议（如有必要）并实现这两个方法。有关关于 `NSCoding` 方法的更多信息，请参阅“入口和出口点”（第 121 页）。

如果任何祖先类采用了正式协议，你也必须确保你的类正确符合该协议。如果父类的方法实现对你的类来说是不够，你的类应该重新实现这些方法。

# 错误处理

对于任何编程领域来说，程序员妥善处理错误是公理化的要求。然而，什么是“妥善”，通常取决于编程语言、应用程序环境和其他因素。

要使你的对象符合 KVO 规范，如果你对自动通知满意，你可以选择实现手动键值观察，这需要额外的工作。

> **进阶阅读：**阅读《键值编程指南》和《键值观察指南》以了解更多关于这些技术。关于使用 KVC、KVO 和 [绑定 (Mac OS X)](第 187 页) 的 Cocoa 绑定技术总结，请参阅[对象间的通信](第 175 页)中的相关章节。

对象基础设施

自定义子类应该实现（即使不是全部）以下根类和绑定协议方法：

- **isEqualTo:** 和 **hash:**—实现这些 `NSObject` 方法，以为它们的比较引入某些特定对象的逻辑。例如，如果你通过序列号拥有你的类的实例，那么等等的依据是什么？欲更多信息请参阅[自省](第 87 页)。

- **description**—实现此 `NSObject` 方法以返回一个简要描述对象属性或内容的字符串。该信息由调试器中的打印对象返回，并用于字符串中的 `%@` 格式化对象。例如，如果你有一个具有名称、日期、部门和位置 ID 属性的假设 `Employee` 类。该类的 `description` 方法应该如下所示：

- **copyWithZone:**—如果你向子类的客户端暴露拷贝其实例的能力，则你应该实现 `NSCopying` 协议的此方法。值对象（包括模型对象）是拷贝的典型候选者；而 `UIView` 和 `NSColor` 则不是。如果你的类实例是可变的，你应该遵守 `NSMutableCopying` 协议。

- **initWithCoder:** 和 encodeCoder:—如果你预计你的类实例会被归档（例如，使用模型类），你应该采用 `NSCoding` 协议（如有必要）并实现这两个方法。有关关于 `NSCoding` 方法的更多信息，请参阅“入口和出口点”（第 121 页）。
