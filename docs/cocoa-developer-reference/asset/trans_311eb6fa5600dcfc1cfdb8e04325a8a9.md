
## 使用键值编码

与选择器类似，键值编码（KVC）为 Objective-C 引入了方向性。但 KVC 是一项非常不同且不相关的技术，其应用也大不相同。

KVC 使得通过属性名称字符串间接访问属性成为可能。

```objective-c
aReturn = anObject.aProperty;                 //Direct access
aReturn = [anObject valueForKey: @"aProperty"]; //KVC access
```

KVC 在理论上看起来很简单，但在实践中可能很棘手。一些问题包括：

- **值必须“对象化”。** 这项技术更准确地说应称为键对象编码（Key-Object Coding），因为除少数例外，值必须包装在对象内部。
- **KVC 通常不用于标准属性访问。** 使用标准 setter、getter 和 `@synthesize` 更容易。
- **KVC 广泛用于初始化并返回成组的值，以及访问数据集合对象中的值。** 必须掌握它才能有效地使用 Cocoa。
- **Cocoa 的键路径管理可能显得难以捉摸。** 你可以使用 `object.property.subproperty` 语法定义键路径。但并非所有类都支持键路径访问，而支持它的类也并不总是以一致的方式实现。这尤其适用于可变数据集合。
- **KVC 使捕获错误变得更困难。** 如果使用字符串字面量作为键，编译器无法检查它们。你可以通过在头文件中将键字符串定义为常量，并在整个代码中使用它们来解决此问题。

### “对象化”值

考虑这个简单的 KVC 示例，它读取并设置 `NSWindow` 的一些值。这段代码看起来是设置 `hasShadow` 属性的合理尝试。

```objective-c
[window setValue: NO forKey: @"hasShadow"];
```

但它不起作用，因为 `setValue:` 期望一个对象，而不是 BOOL。正确的代码是：

```objective-c
[window setValue: [NSNumber numberWithBool: NO]
        forKey: @"hasShadow"];
```

这说明了值必须如何对象化，从而给 KVC 增加了一层额外的复杂性。图 9.10 说明了这一点。

**图 9.10**

将数值类型转换为 NSNumber 对象，然后再转换回来。如果不将数值类型“对象化”，就无法对它们使用 KVC。

![](img/2b293e29fc15b0797f113b85dd429b6e_244_0.png)

**注意**

如果有 `set...` 方法，请将 `set` 后的第一个字符转换为小写。例如，`NSWindow` 有一个 `setHasShadow` 方法。对应的键是 `hasShadow`。

### 使用 NSNumber

字符串已经通过 `@` 字符对象化了。要将数值对象化，请将它们包装在 `NSNumber` 实例中。所有数值类型，包括 `int`、`float`、`BOOL` 等，都必须以类似方式包装。有关支持类型的完整列表，请参阅 NSNumber 类参考。

例如，使用以下代码设置 float：

```objective-c
[window setValue:
    [NSNumber numberWithFloat: 0.75]
    forKey: @"alphaValue"];
```

NSNumber 支持名为 <type>Value 的方法，可将 NSNumber 转换回其等效的简单类型。读取值的等效代码如下：

```objective-c
BOOL returnFlag =
    [[window valueForKey: @"hasShadow"] boolValue];
float aFloat =
    [[window valueForKey: @"alphaValue"] floatValue];
etc...
```

**提示**

创建新键时，在键名中包含类型定义会很有用，可以作为提醒或“代码工具提示”。

```objective-c
@"something"     //Bad
@"somethingBOOL" //Good
```

### 使用 nil

由于 NSNumber 是对象类型，其值可能为 nil。如果代码可能访问尚未设置的值，那么测试这一点很重要：

```objective-c
if ([window valueForKey:@"hasShadow"] != nil)
    BOOL returnFlag = [[window valueForKey:@"hasShadow"]
        boolValue];
```

Cocoa 的键很可能已初始化。自定义对象可能包含也可能不包含初始化代码，因此良好的做法是确保所有可能的值都正确初始化，或者在使用返回值之前测试它们是否为 nil。

### 使用 NSNull

令人困惑的是，集合对象——NSDictionary、NSArray、NSSet 等——使用一种不同但等效的值，称为 null。

nil 是空指针，而 null 是用作缺失且未定义值占位符的对象。null 定义为 NSNull 类的输出，它是 NSNull 的一个实例。

```objective-c
NSNull *nullValue = [NSNull null];
```

这种奇怪的构造是访问 null 值的唯一方式。

### 避免错误

如果 KVC 系统找不到某个键，就会引发错误。你可以通过在正在访问的对象中实现 valueForUndefinedKey: 方法来控制 KVC 错误。添加以下样板方法签名，实现该方法以创建有用的返回，例如代码可以捕获的错误值：

```objective-c
- (id)valueForUndefinedKey:(NSString *)key
{
    //return a default value to avoid generating an exception
}
```

当你尝试设置未识别的键的值时，会触发等效的 setValue: forUndefinedKey: 方法。用空实现重写此方法是避免生成写入时异常的最简单方式。

### 使用键值观察

键值观察（KVO）是一项相关技术，它将键与观察者方法关联起来。每当值更新时，观察者方法就会被触发。你可以使用它来监视任何符合 KVO 的对象中的任何属性。

KVO 字面意思是，当值被修改时，观察者方法会被触发——这是一种远程查看形式。即使被观察对象与执行观察的对象之间没有其他连接，KVO 也能工作。

观察者方法接收一个包含更改详情的字典。可以将该字典配置为报告旧值、新值、原始值和先前值的任意组合。观察者方法可以位于不同的对象中。图 9.11 说明了其工作方式。

**图 9.11**
理解 KVO。`registerAsObserver:` 方法运行一次以启用 KVO。每次键路径的值被修改时，都会运行 `observeValueForKey:` 方法。

![](img/2b293e29fc15b0797f113b85dd429b6e_246_0.png)

```objective-c
- (void)registerAsObserver
{
    [objectToWatch addObserver: watchingObject
                    forKeyPath:@"observedProperty"
                       options:(NSKeyValueObservingOptionNew |
                                NSKeyValueObservingOptionOld)
                       context:NULL];
}
```

这会将 `watchingObject` 初始化为 `objectToWatch` 中 `observedProperty` 键的观察者。对象可以观察自身，因此两个对象都可以是 `self`。

`options` 字段将两个选择标志按位或在一起，并设置字典以返回旧值和新值。`context` 是一个自由字段，可用于将任意指针传递给观察者。

要处理更新，请将以下方法添加到观察者中。该方法定义是传入参数的样板列表。同一个方法体可以处理多个属性的更新，因此包含一组条件判断并为每个属性运行单独的代码会很有用。

例如，假设你有一个名为 `myObject` 的对象，它是 `MyClass` 的实例，并且有一个名为 `thisInt` 的属性。以下代码将触发 KVO 更新，**只要你是在另一个对象中运行它**：

```objective-c
myObject.thisInt = 15;
```

访问器方法由外部属性写入触发。但是，如果你在 myObject 中包含内部更新代码，该赋值不会使用访问器，因此该赋值对 KVO 不可见。

```objective-c
@implementation MyClass
...
thisInt += 10;
```

一种解决方案是使用显式代码强制更新：

```objective-c
[self willChangeValueForKey: @"thisInt"];
thisInt = thisInt + 10;
[self didChangeValueForKey: @"thisInt"];
```

当你想把一个数字加到另一个数字上时，这种做法很难看，而且会带来很多额外麻烦。其他解决方案也是可能的，但最优雅的是对关键赋值使用 `self` 和点语法：

```objective-c
self.thisInt = thisInt+10;
```

指定 `self` 会强制赋值使用访问器，从而以简单易读的方式解决问题。仅将其用于*关键*赋值。为了提高性能，不要在计算中的中间步骤使用它。

你还必须检查在使用绑定（第 13 章中描述）时是否使用了访问器。绑定使用 KVO，如果你不使用访问器设置值，它们就无法正确跟踪更新。

![](img/2b293e29fc15b0797f113b85dd429b6e_248_0.png)

**注意**  
此解决方案适用于点语法。如果你不赞成点语法，你将不得不使用丑陋的老式构造，例如 `[self setThisInt: [self thisInt] + 10];`。

### 使用 KVO

KVO 可以极其强大。你的应用可以监视代码中任何位置的事件，并自动响应给定的值或应用状态。在代码中某处设置一个值，可以自动触发一系列依赖事件。许多 Cocoa 对象都符合 KVO；你的应用可以观察 Cocoa 对象属性的变化，并根据需要做出响应。一些应用包括以下内容：
