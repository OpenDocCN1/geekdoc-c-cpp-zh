

# 第 3 章

# 为 Cocoa 代理添加行为

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

