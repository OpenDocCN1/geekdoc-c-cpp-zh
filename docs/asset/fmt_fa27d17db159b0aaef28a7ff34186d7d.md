
Objective-C 引用计数架构中一个重要的特性是所谓的自动释放池（`autorelease pools`）。你不需要调用 `release` 来立即减少对象的引用计数（并可能将其释放），你也可以调用 `autorelease`，它会在稍后的某个时间执行释放，通常是在下一次运行事件循环时，但也可能更早发生（参见项目 34）。

这个特性非常有用，特别是当从方法返回对象时。在这种情况下，你并不总是希望以调用者所有的的方式返回它。例如，考虑以下方法：

```objc
- (NSString*)stringValue {
  NSString *str = [[NSString alloc]
    initWithFormat:@"I am this: %@", self];

  return str;
}
```

## 项目 29：理解引用计数

在这种情况下，`str` 返回时的引用计数为 +1，因为调用 `alloc` 返回时计数为 +1，且没有对应的平衡的 `release`。这里 +1 的意义是，你作为调用者，负责一次 `retain`。然而，这并不意味着引用计数正好是 1。它可能更高，那是 `initWithFormat` 方法内部的实现细节。你唯一需要担心的是平衡那一次 `retain`。

但是，你不能在方法内部释放 `str`，因为否则它会在返回之前被立即释放。因此，使用 `autorelease` 来指示该对象应该在稍后的某个时间释放，但保证在未来有足够的时间，以至于调用者如果需要持有它，就可以进行 `retain`。换句话说，该对象保证在跨方法调用边界时依然存活。事实上，释放将在最外层的自动释放池清空时发生（参见项目 34），除非你有自己的自动释放池，它将在当前线程事件循环的下下一次轮询时执行。将此应用于 `stringValue` 方法，结果如下：

```objc
(NSString*)stringValue {
  NSString *str = [[NSString alloc]
    initWithFormat:@"I am this: %@", self];
  return [str autorelease];
}
```

现在，返回的 `NSString` 对象在返回给调用者时一定是存活的。因此，可以这样使用对象：

```objc
NSString *str = [self stringValue];
NSLog(@"The string is: %@", str);
```

这里不需要额外的内存管理，因为 `str` 返回时是自动释放的，因此是平衡的。由于自动释放池中的释放不会等到下一次运行事件循环时发生，所以该对象在 `log` 语句中不需要显式地 `retain`。然而，如果对象需要被持有（例如设置为实例变量），则需要对对象进行 `retain` 并在随后将其释放：

```objc
_instanceVariable = [[self stringValue] retain];
// ...
[_instanceVariable release];
```

因此，`autorelease` 是一种延长对象生命周期的方法，使其能够跨方法调用边界。

# 第 5 章：内存管理

![](img/72498492af77d8c75e17783675fe4432_171_0.png)

**图 5.3** 对象图中的保留循环

## 保留循环

引用计数中需要注意的一个常见场景是所谓的保留循环（`retain cycle`），当多个对象循环地地引用另一个对象时，就会发生这种情况。这会导致内存泄漏，因为循环中没有任何对象会看到其引用计数降为 0。循环中的每个对象至少都有循环中的另一个对象对其维持引用。在图 5.3 中，三个对象都对其他两个对象中的一个有一个单一引用。在这个循环中，所有的引用计数均为 1。

在垃圾回收的环境中，这种情况通常会被识别为所谓的“孤立岛屿”（`island of isolation`）。在这种情况下，垃圾器会释放所有三个对象。在 Objective-C 的引用计数架构下并没有这种奢侈。问题通常通过使用弱引用（参见项目 33）或通过外部影响导致一个对象放弃对另一个对象的保留来解决。无论哪种情况，保留循环都会被打破，内存不再泄漏。

## 需要记住的事

- 引用计数内存管理基于一个递增的计数器。

## 项目 30：使用 ARC 让引用计数变得简单

任何其他方法名都表示返回的对象将不会由调用代码拥有。在这些情况下，对象将以自动释放（`autoreleased`）的方式返回，以便确保该值在跨越方法边界时仍然有效。如果希望确保对象活得更久，调用代码必须对其进行留存（`retain`）。

`ARC` 自动处理维护这些规则所需的所有内存管理，包括返回自动释放对象的代码，如下面的代码所示：

```objc
+ (EOCPerson*)newPerson {
    EOCPerson *person = [[EOCPerson alloc] init];
    return person;
    /**
   * 方法名以 'new' 开头，由于 'person'
   * 已经因为 'alloc' 产生了一个不平衡的 +1 引用计数，
   * 返回时不需要进行 retain、release 或 autorelease。
   */
}
```

```objc
+ (EOCPerson*)somePerson {
    EOCPerson *person = [[EOCPerson alloc] init];
    return person;
    /**
   * 方法名没有以任何一个“所有权”（owning）前开头，
   * 因此 ARC 在返回 'person' 时会添加一个 autorelease。
   * 等价的手动引用计数语句是：
   * return [person autorelease];
   */
}
```

```objc
(void)doSomething {
    EOCPerson *personOne = [EOCPerson newPerson];
    //

    EOCPerson *personTwo = [EOCPerson somePerson];
    //
```

此时，`personOne` 和 `personTwo` 出了作用域，因此 `ARC` 需要按照要求对它们进行清理。

- `personOne` 是以此代码块拥有的方式返回的，因此需要被 `release`。

- `personTwo` 以非此代码块拥有的方式返回的，因此不需要被 `release`。

- 等价的手动引用计数清理代码是：

  - `[personOne release];`

# 第 5 章：内存管理

`ARC` 通过命名规范标准化了内存管理规则，这让该语言的新手通常认为是不寻常的。很少有语言像 Objective-C 那样强调命名。熟悉这一概念对于成为一名优秀的 Objective-C 开发者至关重要。`ARC` 有助于这一过程，因为它为你做了大量工作。

除了 `retain` 和 `release` 之外，`ARC` 还有其他优点。它还能执行手动难以或无法完成的优化。例如，在编译时，如果可能，`ARC` 可以合并 `release` 和 `autorelease` 以抵消它们。如果它看到同一个对象被多次 `retain` 和多次 `release`，`ARC` 有时可以移除 `retain` 和 `release` 对。

`ARC` 还包含一个运行时（`runtime`）组件。那部分的优化更有趣，并且有助于证明为什么所有未来的代码都应该在 `ARC` 下编写。记住某些对象从方法返回时是自动释放返回的。有时，调用代码需要对对象进行留存（`retain`），如下场景所示：

对 `initWith:` 的调用返回了一个自动释放的 `EOCPerson`。但编译器在设置实例变量时也需要添加一个 `retain`，因为它持有强引用。因此，在手动引用计数的世界中，之前的代码等于以下内容：

```objc
EOCPerson *tmp = [EOCPerson initWithName:@"Bob Smith"];
myPerson = [tmp retain];
```

你在这里注意到 `initWithName:` 方法中的 `autorelease` 和 `retain` 是多余的，这是正确的。移除两者对性能是有益的。但在 `ARC` 下编译的代码需要与非 `ARC` 代码兼容，以保持后兼容。`ARC` 本可以移除 `autorelease` 的概念，并规定从方法返回的所有对象都以 +1 引用计数返回。然而，这将破坏向后兼容。

## 项目 30：使用 ARC 让引用计数变得简单

但 `ARC` 确实包含运行时行为来检测“多余的 `autorelease` + 立即 `retain`”的情况。它通过一个特殊函数实现，该函数在对象以自动释放方式返回时运行。它不是直接调用对象的 `autorelease` 方法，而是调用 `objc_autoreleaseReturnValue`。该函数会检查从当前方法返回后立即将执行的代码。如果检测到将对返回的对象进行 `retain`，则会在全局数据结构（取决于处理器）中设置一个标记，而不是执行 `autorelease`。同样，留存从方法返回的自动释放对象的调用代码使用一个名为 `objc_retainAutoreleaseReturnValue` 的函数，而不是直接调用 `retain`。该函数检查标记，如果没有执行 `retain` 则就不操作。设置和检查标记的额外工作比执行 `autorelease` 和 `retain` 更快。

下面的代码通过展示 `ARC` 如何使用这些特殊函数说明了这种优化：

```objc
// 在 EOCPerson 类内部
(EOCPerson*)personWithName:(NSString*) name {
    EOCPerson *person = [[EOCPerson alloc] init];
    person.name = name;
    objc_autoreleaseReturnValue(person);
}
```

```objc
// 使用 EOCPerson 类
EOCPerson *tmp = [EOCPerson personWithName:@"Matt Galloway"];
myPerson = objc_retainAutoreleaseReturnValue(tmp);
```

这些特殊函数具有特定处理器的实现，以利用最优方案。以下伪代码解释了发生了什么：

```objc
id objc_retainAutleaseReturnValue(id object) {
    if (object) {
        return [object retain];
    }
    return nil;
}
```

```objc
id objc_autoreleaseReturnValue(id object) {
    if (object) {
        return [object autorelease];
    }
    return object;
}
```

（注：伪代码文本是碎片，已根据标准的 `ARC` 运行时行为进行了重建以保持连贯性。）

设置和检查标记的额外工作比执行 `autorelease` 和 `retain` 更快。

## 变量的内存管理语义

`ARC` 还处理局部变量和实例变量的内存。默认情况下，每个变量都是强引用。理解这一点很重要，特别是对于实例变量，因为其语义可能与手动引用计数不同。例如考虑以下代码：

```objc
@interface EObjectClass : NSObject {
    id _object;
}
```

```objc
@implementation EObjectClass
- (void)setup {
    _object = [EOObjectClass new];
}
@end
```

`_object` 实例变量在 `ARC` 下不会自动留存其值。因此，当 `setup` 方法在 `ARC` 下编译时，它会变为：

```objc
- (void)setup {
    id tmp = [EOObjectClass new];
    _object = [tmp retain];
    [tmp release];
}
```

# 第 5 章：内存管理

在这种情况下，设置实例变量时，对象将不会被保留。使用 `__weak` 修饰符自动置空弱引用仅在运行时的最新版本（Mac OS X 10.7 和 iOS 5.0）中可用，因为它们依赖于新添加的功能。

当应用于局部变量时，这些修饰符通常用于打破 `block` 可能会引入的保留循环（见第 40 节）。`block` 会自动保留它捕获的所有对象，如果一个保留 `block` 的对象又被该 `block` 留，有时会导致保留循环。可以使用 `__weak` 局部变量来打破保留循环：

```objc
NSURL *url = [NSURL URLWithString:@
```

# ARC 对实例变量的处理

如所述，`ARC` 也会处理实例变量的内存管理。这需要 `ARC` 在释放（`deallocation`）期间自动生成清理代码。任何持有强引用的变量都需要释放，`ARC` 通过钩入 `dealloc` 方法来实现这一点。在手动引用计数中，你必须自己编写编写如下所示的 `dealloc` 方法：

```objc
+ - (void)dealloc {
  [foo release];
  [bar release];
  [super dealloc];
}
```

在 `ARC` 中，不需要这种 `dealloc` 方法；生成的清理程序将通过利用 Objective-C++ 的特性来实现此。一个 Objective-C++ 对象在释放期间必须调用该对象持有的所有 C++ 对象的析构函数。当编译器看到一个对象包含 C++ 对象时，它会生成一个名为 `_cxx_destruct` 的方法。`ARC` 借用此方法并在内部发出所需的清理代码。

然而，如果你有任何非 Objective-C 对象（例如 CoreFoundation 对象或通过 `malloc()` 分配的堆内存），你仍然需要清理它们。但你不需要像以前那样调用父类的 `dealloc` 实现。记住，在（此处原文缺失）调用 `dealloc` 时

# 第 30 节：使用 ARC 使引用计数更简单

显式使用引用计数是非法的。因此，`ARC` 在替你生成并运行 `.cxx_destruct` 方法的同时，也会自动调用父类的 `dealloc` 方法。在 `ARC` 下，`dealloc` 方法看起来可能像这样：

```objc
(void)dealloc {
  CFRelease(_coreFoundationObject);
  free(_heapAllocatedMemoryBlob);
}
```

`ARC` 生成释放操作意味着通常不需要 `dealloc` 方法。这通常会显著减小项目源代码的，并有助于减少样板代码。

# 重写内存管理方法

在 `ARC` 之前，可以重写内存管理方法。例如，单例实现通常会重写 `lease` 为一个空操作，因为单例不能被释放。这在 `ARC` 下现在认为是非法的，因为这样做可能会干扰 `ARC` 对对象生命周期的理解。由于这些方法是非合法的调用和重写，`ARC` 在需要执行 `retain`、`release` 或 `autorelease` 时，会进行不通过 Objective-C 消息分发（见第 11 节）的优化。相反，该优化是在运行时深处的 C 函数实现的。这能够实现如前所述的优化，例如返回一个立即被保留的 `autorelease` 对象时。

## 注意事项

- 自动引用计数 (`ARC`) 让开发者无需担心大多数内存管理问题。使用 `ARC` 减少了类中的样板代码。

- `ARC` 通过在适当的地方添加 `retain` 和 `release` 几乎完全地处理对象的生命周期。变量修饰符可用于指示内存管理语义：以前，`retain` 和 `release` 是手动安排的。

- 方法名称一直被用于指示返回对象的内存管理语义。`ARC` 固化了这些规范，并使得无法不遵守。

- `ARC` 仅处理 Objective-C 对象。这意味着 CoreFoundation 对象不被处理，必须应用适当的 `CFRetain/CFRelease` 调用。

# 第 31 节：仅在 dealloc 中释放引用和清理观察

对象经历其生命周期最终会被释放，这就是 `dealloc` 方法进入的地方。在对象的生命周期内，当它的保留计数降为 0 时，该方法恰好被调用一次。尽管如此，无法保证具体的何时被调用。此外，你可能认为你通过手动查看 `retain` 和 `release` 的位置就能知道它何时会被调用。但在实践中，任何库都可能在你不知情的情况下操作该对象，导致释放发生在另一个时间。运行时会在准确的时间为你调用它。此外，在对对象调用 `dealloc` 后，该对象就不再有效了，后续的方法调用也是无效的。

那么在 `dealloc` 中你应该做什么呢？主要任务是释放对象拥有的任何引用。这意味着释放任何 Objective-C 对象，`ARC` 会通过 `.cxx_destruct` 自动方法替你将其添加到 `dealloc` 方法中（见第 30 节）。

在 `dealloc` 中做的另一个有用的工作是清理任何已设置的观察。如果使用了中心中心来注册通知，这里是取消注册的好地方，这样它们就不会被尝试发送给已释放的对象。object。

```objc
(void)dealloc {
  CFRelease(coreFoundationObject);
  [NSNotificationCenter defaultCenter] removeObserver:self];
}
```

注意，当使用手动计数而非 `ARC` 时，`[super dealloc]` 应该是你做的最后件事。`ARC` 自动强制这一点，这也是为什么使用它更简单、更安全的另一个原因。释放对象拥有的每个对象。

# 第 31 节：仅在 dealloc 中释放引用和清理状态

不应依赖在任何特定时间被调用，你没有意识到某些东西正持有该对象。在这种情况下，你持有稀缺资源的时间比预期的长，这是不希望的。在这些场景中，通常实现另一个在应用程序完成对象时调用的方法。这样资源的生命周期就是确定的。

一个可能需要清理方法的对象示例是管理到服务器连接的对象。也许是数据库的连接。这样一个类的接口可能如下：

```objc
#import <Foundation/Foundation.h>
```
