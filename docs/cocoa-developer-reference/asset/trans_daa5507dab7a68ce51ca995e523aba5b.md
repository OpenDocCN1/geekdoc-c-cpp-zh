
```
}
(a list of public properties prefixed with @property
    declarations)
(a list of public methods that can be accessed by other objects...)
(a list of public setter and getter methods, if used)
@end
```

@interface 指令告诉 Objective-C，接下来的行定义了类接口。该行的其余部分包含类名，类名可以是任意唯一字符串，后面跟着它继承特性的超类名称。

换句话说，这一行告诉 Objective-C 创建一个名为 *MyNewClass* 的新类，并从 NSObject 复制方法和属性。要继承不同的类，请替换 NSObject。例如，下面的代码替换为 NSView：

```
@interface MyNewViewClass : NSView <protocols>{...
```

> **注意**
>
> protocols 字段包含一个或多个命名的可选方法包，可在类中使用。协议是一种简化的复杂导入/包含形式。协议用作将相关方法组快速导入类的一种方式。它们是可选的，但许多 Cocoa 对象都使用它们。有关一些示例，请参见第 6 章。

实例变量（也称为 *ivars*）可以是带指针的对象，也可以是标准 C 数据类型。例如：

```
{
    NSView *aView;       //This is a pointer to a view
    int numberOfGiraffes; //This is a standard C int
}
```

花括号之间的属性列表定义了私有内部变量。要将它们暴露给其他对象，属性名必须加上 @property 指令前缀。

```
@property (nonatomic, retain) NSView *aView; // aView can be public
```

> **注意**
>
> `(nonatomic, retain)` 定义了对象属性的内存管理选项。C 数据类型不需要这个额外信息。有关更多信息，请参见第 12 章。

方法列表定义了可由其他对象触发的每个公共方法。例如：

```
- (void) thisIsAMethod;
// This is a method with no return value and no parameters
- (NSValue *) thisIsAnotherMethod: (int) aNumber;
// This is a method that returns an instance of NSValue and takes an int as a parameter
```

方法以签名形式列出——即一行摘要，列出方法中使用的类型、输出类型、名称和参数。签名以分号结尾。它们不包括实现代码。

在接口文件和实现文件中，Objective-C 都使用 – 字符作为实例方法定义的前缀，使用 + 作为类方法定义的前缀。

```
- (void) thisIsAnInstanceMethod;
+ (void) thisIsAClassMethod;
```

## 定义访问器：设置器和获取器

在 Objective-C 中，属性是私有的且不可见，除非为它们定义了设置器和获取器方法。设置器写入值；获取器读取值。属性可以允许其中一种或两种访问模式。你可以用代码显式定义设置器和获取器，也可以使用 @synthesize 指令隐式定义。

使用 @synthesize 为简单的读和写操作生成所需的设置器和获取器。该指令的作用很像宏，它会自动创建设置器和获取器代码。它还实现点格式的属性访问。

```
anInt = anObject.numberOfElephants;
anObject.numberOfWheels = 5;
```

这种语法在其他语言中很常见。在 Objective-C 中，只有当属性被合成时，它才有效。

当读取或写入属性会触发更复杂的结果时，请使用显式的设置器和获取器代码，例如对象状态发生变化，或访问其他属性和功能的操作。例如，设置器可以在窗口大小改变时自动重绘可见图形，或者获取器可以统计属性被访问的次数，并将计数写入另一个属性。

按照约定，获取器方法名与它们访问的属性名相同，而设置器会在名称前加上 set。在接口中定义设置器和获取器如下：

```
- (int) numberOfElephants; // A getter for the numberOfElephants property
- (void) setNumberOfWheels: (int) aNumber; // A setter for the numberOfWheels property
```

要使用它们，语法是

```
anInt = [anObject numberOfElephants];
[anObject setNumberOfWheels: 5];
```

编译器并不强制实施这种命名约定，但 Cocoa 中使用了它，它有助于使代码易于阅读。设置器和获取器代码的复杂度没有限制。如有必要，单个设置器方法可以显著改变整个应用程序的状态。

## 使用 self

在类中，self 用于访问内部方法。例如：

```
[self doSomethingInternal];
```

会触发 doSomethingInternal 方法，假定该类中存在该方法。内部方法可以是私有的或公共的。你也可以使用 self 使属性访问操作显式化。

```
// If aProperty uses a custom getter, this is necessary
aValue = [self aProperty];

// ...because this is interpreted as a pointer copy
aValue = aProperty;
```

## 定义类实现

实现文件的内容组织如下：

```
#import MyNewClass.h
#import (any other classes that are referenced)
@implementation MyNewClass
    (an optional list of @synthesize directives for properties)
    (an optional list of private variables)
    (a list of methods with full implementation code)
@end
```

#import 指令加载接口头文件。由于历史原因，Objective-C 对 Objective-C 头文件使用 #import，对 C 头文件使用 #include。文件的其余部分是已实现方法的列表。接口中列出的任何方法都必须在实现中实现。实现不必完整和完成——一个存根即可——但如果缺少它，编译器将抛出错误。

> **注意**
>
> 可以将头文件和实现合并到单个文件中。这是一种不好的做法，因为类经常需要导入其他类的接口声明。当头文件与代码不分离时，这会变得非常低效。

如果一个类引用了某个类或框架，它必须包含针对其头文件的 #import 指令。为了清晰和易记，良好的做法是在实现中包含 #import 指令。

要使用 @synthesize，请在其后跟一个属性名列表，并以分号结束该列表：

```
@synthesize aProperty, anotherProperty, somethingElse, aView;
```

这会对列出的四个属性运行 `@synthesize` 功能，并为它们生成设置器和获取器代码。然后，你可以使用点语法或常规方法代码从其他对象访问这些属性。

```
aValue = [thisObject aProperty];  // Using a synthesized getter
aValue = thisObject.aProperty; // Identical code using dot syntax

[thisObject aProperty: 5]; // Using a synthesized setter
thisObject.aProperty = 5; // Identical code using dot syntax
```

## 定义公共属性

总而言之，要创建一个可由其他对象访问的属性，你必须做三件事：

- 1. **在接口的 ivars 列表中包含它。**
- 2. **在接口中再次将其声明为 `@property`。**
- 3. **在实现中添加显式的设置器/获取器方法，或对属性使用 `@synthesize`。**

这三个步骤都是必需的。如果跳过其中一步，构建将失败，或者应用程序可能崩溃。如果更改属性名，必须在所有三个位置都更改它。

![](img/2b293e29fc15b0797f113b85dd429b6e_132_0.png)

**提示**

在专注于其余代码时，很难记住这三个步骤，因此将此摘要用作检查清单会很有帮助。最终，这三个步骤会开始变得自动化，但忘记某个步骤仍然是一个常见且普遍的错误。

## 定义公共方法

要定义公共方法，请遵循以下四个步骤：

- 1. **在接口中声明签名。** 签名包括类/实例类型、返回类型、名称和参数列表。以分号结尾。
- 2. **将签名复制到实现文件。**
- 3. **将分号替换为左花括号。**
- 4. **添加实现代码并关闭花括号。**

例如，以下代码完整定义了一个名为 `thisMethodDoesNothing` 的方法：

```
- (void) thisMethodDoesNothing; // Add this line to the method list in the interface
```

