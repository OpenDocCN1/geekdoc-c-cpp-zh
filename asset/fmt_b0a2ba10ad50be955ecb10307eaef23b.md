
这是一个所有“视图(views)”都继承的类。它们是用户界面的构建块，负责按钮、文本字段和表格的绘制。该类的名称是自而易见的，并使用了整个 UIKit 框架中使用的 `UI` 前缀。

- `UIViewController` (class)

视图（`UIView`）处理视图的绘制，但不负责控制视图内显示的内容。那是该类的工作：“视图控制器（view controller）”。它的命名方式保持了从左到右的易读性。

# 第 19 条：使用清晰且一致的命名

- `UITableView` (class)

这是一种特定的视图，用于在表格中显示项目列表。因此，它的命名方式是父类加上修饰符，以区分它是哪种视图。这种给父类加前缀的方法是整个命名规范中的共同主题。它可以简单地命名为 `UITableView`，但将无法清楚它是一个视图。你必须查找接口声明以确定它是什么。例如，如果你创建一个专门用于显示图像的特定表格视图。你可以创建一个名为 `ECIUITableView` 的子类，你始终在前面加上自己的前缀，而不是使用父类的前缀（在本例中为 UIKit 的 `UI` 前缀）。原因是你无权向另一个框架的命名空间添加任何内容，而且另一个框架可能会在未来创建一个同名的类。

- `UITableView` (class)

正如 `UITableView` 是视图的一种特定类型，这是一种特殊的视图控制器，专门用于控制表格视图。因此，它的命名方式相似。

- `UITableViewDelegate` (protocol)

该协议定义了一个接口，视图可以通过该接口与另一个对象进行通信，并以其所定义的代理接口的类命名，这确保了从左到右的易读性。（关于代理模式（Delegate pattern）的更多信息，请参见第 23 条。）

重要的是，你应该在命名上保持一致。此外，如果你在另一个框架内进行子类化，请确保遵循它的规范。例如，如果你通过子类 `UITableView` 创建自定义视图，请确保类名的最后一个单词是 `View`。同样，如果你创建了自己的代理协议，你应该将其命名为它所代理的类，后面紧跟 `Delegate` 单词。遵循这种命名结构将确保当你以后回来查看或他人使用该代码时，你的代码是有意义的。

## 注意事项

- 遵循 Objective-C 中已成标准的命名方式来创建符合规范且感觉正确的接口。
- 确保方法名简洁但准确，并让它们的使用像句子一样从左到右易读。

# 第 3 章：接口与 API 设计

- 避免在方法名中使用类型的缩写。
- 最重要的是，确保方法名与你自己的代码或与其集成的代码一致。

## 第 20 条：为私有方法名加前缀

类的功能比其外部看起来要多得多，是非常常见的。在编写类实现时，编写仅供内部使用的方法很常见。对于此类方法，我建议在它们的名称前加上一些内容。这有助于通过区分公共方法和私有方法，从而辅助调试。

使用标记处理私有方法的另一个原因是考虑更改方法名或签名时。如果该方法是公共的，这种更改应该经过更仔细的考虑，因为更改类的公共 API 可能不是理想的。这样，该类的消费者也需要更新他们的代码。然而，如果该方法是内部的，则只需要更改类自身的代码。使用标记来指示私有方法意味着在进行此类更改时，这种区别一目易见。

使用的前缀取决于你的个人偏好。包含在前缀中的良好字符选择是下划线和字母 `p`。我倾向于使用前缀 `p_`，因为 `p` 表示“private（私有）”，下划线在方法名开始前提供了一个视觉间隙。方法名随后按照通常的驼命名继续，首字母小写。例如，一个名为 `EObject` 的类可能像这样：

```
@import <Foundation.h>

@interface EObject : NSObject

- (void)publicMethod;

@end

@implementation EObject

- (void)publicMethod {

  /* ... */

}

- (void)p_privateMethod {

  /* ... */

}

@end
```

如果你来自 C++ 或 Java 等语言，你可能奇怪为什么不简单地将方法标记为私有（private）。在 Objective-C 中，没有方法可以将方法标记为私有。所有对象都能响应消息，并且可以在运行时检查对象以确定它响应哪些消息。这就是为什么你要使用命名规范来规定语义。在 Objective-C 中，没有机制限制谁、什么或何时可以调用方法。新成员可能不习惯，但拥抱动态性释放了它的力量。然而，治理这种动态性至关重要，而使用命名规范就是实现这一点。

```
@interface EViewController : UIViewController

```

```
@end
@implementation EViewController

```

然而，结果显示 `UITableView` 也实现了一个名为 `_resetViewController` 的方法！当你调用它时，来自 `EViewController` 的版本将会运行，而原本应该调用原始版本。除非你深入研究库，否则你不会这一点，因为该方法名没有公开。毕竟，它是由下划线表示的私有方法。总而言之，当你在既不是 Apple 的不是你的框架中进行子类化时，你无法该框架使用的是什么私有前缀（如果有），除非它有文档。在这种情况下，你可以选择使用自己的前缀（见第 15 条）作为私有方法前缀，以极大减少任何潜在冲突的风险。同样，你应该考虑他人如何子类化你的类。这就是为什么你应该为私有方法使用前缀。如果没有实现源码，除了使用相当复杂的工具外，无法找到公共接口定义之外的类实现了哪些方法。

## 注意事项

- 为私有方法名加前缀，以便与公共方法区分开。
- 避免使用单个下划线作为方法前缀，因为这是 Apple 保留的。

# 第 21 条：理解 Objective-C错误模型

许多现代语言（包括 Objective-C）都有异常。如果你来自 Java 背景，你可能习惯于使用异常处理错误情况。如果你习惯于使用异常处理此任务，你将不得不回去忘记你所知道的一切并重新开始。

## 项目 21：理解 Objective-C 错误模型

首先需要注意的是，自动引用计数（ARC，参见项目 30）默认情况下并不是异常安全的。在实践中，这意味着任何应该在抛出异常的作用域结束时释放的对象，将不会被释放。可以通过开启编译器标志来生成异常安全的代码，但这会引入额外的代码，即使在没有抛出异常场景的情况下也必须运行这些代码。开启此项的编译器标志是 `-fobjc-arc-exceptions`。

即使不使用 ARC，在使用异常时，编写防止内存泄漏的代码也是困难的。假设创建了一个资源，并在不再需要时需要释放它。如果在资源被释放之前抛出了异常，那么该释放操作将永远执行：

```objc
id someResource = /* ... */;
if ( /* 检查错误 */ ) {
  @throw [NSException exceptionWithName:@"ExceptionName"
                         reason:@"There was an error"
                         userInfo:nil];
}
[someResource doSomething];
[someResource release];
```

```objc
```

当然，解决这个问题的方法是在抛出异常之前释放 `someResource`；然而，如果有许多资源需要释放且代码路径更加复杂，代码很容易变得杂乱。此外，如果向此类代码中添加新内容，很容易忘记在每次抛出异常之前都添加释放操作。

Objective-C 近期采用的方法是，将异常留给那些“应当避免恢复且异常应导致应用程序退出”的罕见场景。这意味着不需要涉及复杂的异常安全代码。

请记住，异常仅用于致命错误（fatal errors）。当你创建一个在在使用之前应该被子类化的抽象基类时，这里有一个你应该考虑在自己的类中抛出异常的场景示例。与某些其他语言不同，Objective-C 没有语言构造结构来表示一个类是抽象的。实现类似效果的最好方法是在任何必须在子类中重写的方法中抛出异常。任何尝试创建抽象基类实例并使用它的人都会得到一个异常：

```objc
(void)mustOverrideMethod {
  NSString *reason = [NSString stringWithFormat:
    @"%@ must be overridden"
    NSStringFromSelector(_cmd)];

  @throw [NSException exceptionWithName:NSInternalInconsistencyException
                               reason:reason
                               userInfo:nil];
}
```

但如果异常仅用于致命错误，那么其他错误该怎么办？Objective-C 选择的指示非致命错误的范式是从发生错误的方法中返回 `nil` / `0`，或者使用 `NSError`。返回 `nil` / `0` 的示例是在初始化方法中无法根据传入的参数初始化实例：

```objc
- (init)initWithValue:(id)value {
  if ((self = [super init])) {
    if ( /* Value 意味着实例无法创建 */ ) {
      self = nil;
    } else {
      // 初始化实例
    }
  }
  return self;
}
```

在这种情况下，如果 `if` 语句确定无法用传入的值创建实例——可能 `value` 本身需要为非空——`self` 被设置为 `nil`，并且返回的是这个值。初始化方法的调用者将理解发生了错误，因为没有创建实例。

`NSError` 提供了多多的活性，因为它能够返回错误的具体原因。一个 `NSError` 对象封装了三部分信息：

- *错误域 (String)*：发生错误的错误域。这通常是一个全局变量，用于唯一定义错误的源头。例如，URL 处理子系统使用 `NSURLErrorDomain` 域来处理所有来自解析或从 URL 获取数据时的错误。
- *错误代码 (Integer)*：在特定的错误域内唯一标识发生了何种错误的代码。通常使用枚举（enum）来定义特定错误域内可能发生的错误集合。例如，失败的 HTTP 请求可能会使用 HTTP 状态码作为此值。
- *用户信息 (Dictionary)*：关于错误的额外信息，例如本地化描述以及另一个代表导致此错误发生的错误，以便能够表示错误链的信息。

在 API 设计中，错误通常使用的第一种方法是通过使用**代理协议（delegate protocols）**。当发生错误时，对象可以通过协议的其中一个方法传递其代理错误。例如，`NSURLConnection` 包含了其代理协议 `NSURLConnectionDelegate` 中的以下方法：

```objc
(void)connection:(NSURLConnection *)didFailWithError:(NSError*)error
```

当判定认为存在错误时（例如到远程服务器的连接超时），会调用此方法来处理代表所发生情况的错误。这个代理方法不需要实现，因此由 `NSURLConnection` 类的用户来决定是否有必要知道该错误。这比抛出异常更好，因为是否告知错误交由用户自行决定。

`NSError` 的另一种使用方式是通过传递给方法的**输出参数（out-parameter）**。它看起来如下：

```objc
(BOOL)doSomething:(NSError**)error
```

错误变量作为指向 `NSError` 指针的指针传递给方法。或者，你可以将其视为指向 `NSError` 对象的指针。这使得方法实际上可以在返回返回值之外额外返回一个 `NSError` 对象。它的用法如下：

```objc
NSError *error = nil;
BOOL ret = [object doSomething:&error];
if (error) {
  // 发生了错误
}
```

通常，返回此类错误的方法还会返回一个布尔值，表示如果你不在乎错误可以检查这个布尔值。当你不在乎错误是什么时，错误参数也可以是 `nil`。例如，你可能会这样使用该方法：

```objc
BOOL ret = [object doSomething:nil];
if (ret) {
  // 发生了错误
```

在实际上，当使用 ARC 时，编译器会将方法签名中的 `NSError**` 翻译为 `NSError*autorelease*`；这意味着所指向的对象将在方法结束时被自动释放。对象必须这样做，因为 `doSomething:` 方法无法保证调用者能够释放它创建的 `NSError` 对象，因此必须添加 `autorelease`。这与大多数方法的返回值的语义相同（以 `new`、`alloc`、`copy` 和 `mutableCopy` 开头的方法除外）。

方法通过输出参数这样返回错误：

```objc
- (BOOL)doSomething:(NSError**)error {
  // 可能导致错误的操作
  if ( /* 发生了错误 */ ) {
    if (error) {
      // 通过输出参数传递 'error'
      *error = [NSError errorWithDomain:domain
                               userInfo:userInfo];
    }
    return NO; ///// 表示失败
  } else {
    return YES; ///// 表示成功
  }
}
```

## 项目 22：理解 NSCopying 协议

```objc
// EOCErrors.h
extern NSString *const EOCErrorDomain;

typedef NS_ENUM(NSUInteger, EOCError) {
    EOCErrorUnknown = -1,
    EOCErrorInternalInconsistency = 100,
    EOCErrorGeneralFault = 105,
    EOCErrorBadInput = 500;
};

// EOCErrors.m
NSString *const EOCErrorDomain = @"EOCErrorDomain";
```

为你的库创建一个错误域（error domain）是明智的，因为这允许你创建并返回 `NSError` 对象，让消费者可以从你的库中确定这些错误。为错误代码创建一个枚举也是一个好主意，因为它记录了错误并为代码提供了有意义的名称。你也可以决定在定义这些错误的头文件中进行注释，或者对每种错误类型提供更详细的描述。

## 注意事项

- 仅将异常（exceptions）处理会导致整个应用程序崩溃的致命错误。
- 对于非致命错误，提供一个代理方法（delegate method）来处理错误，或者提供一个输出参数 `NSError` 对象。

## 项目 22：理解 NSCopying 协议

对对象进行的一项常见操作是复制它。在 Objective-C 中，这是通过使用 `copy` 方法实现的。支持你自己的类进行复制的方法是实现 `NSCopying` 协议，该协议包含一个方法：

```objc
- (id)copyWithZone:(NSZone*)zone
```

这回到了以前 `NSZone` 被用于将内存划分为不同区域（zones），并且在特定区域内创建对象的时代。现在，每个应用都只有一个区域：默认区域。尽管这是你需要实现方法，但你不需要担心 `zone` 参数是什么。

`copy` 方法在 `NSObject` 中实现，它简单地带上默认区域调用 `copyWithZone:`。请记住，尽管重写 `copy` 可能很有诱惑力，但需要实现的是 `copyWithZone:`。

# 第 3 章：接口与 API 设计

为了支持复制，你只需要需要声明你实现了 `NSCopying` 协议，并实现其中的唯一方法即可。例如，考虑一个代表人的类。在接口定义中，你会声明你实现了 `NSCopying`：

```objc
#import <Foundation/Foundation.h>

@interface EOCPerson : NSObject <NSCopying>
@property (nonatomic, copy, readonly) NSString *firstName;
@property (nonatomic, copy, readonly) NSString *lastName;

- (initWithFirstName:(NSString*)firstName andLastName:(NSString*)lastName;

@end
```

然后，你实现该协议要求的唯一方法：

```objc
- (copyWithZone:(NSZone*)zone {
    EOCPerson *copy = [[self class] allocWithZone:zone]
                      initFirstName:_firstName
                      andLastName:_lastName];

    return copy;
}
```

这个示例简单地将初始化副本的所有工作交给了指定的初始化方法。有时，你可能需要对副本执行进一步的操作，例如，如果类中的其他数据结构没有在初始化器中设置：例如，如果 `EOCPerson` 包含一个数组，该数组通过复制来结交或疏远另一个 `EOCPerson`。在这种情况下，你也会想要复制朋友数组。以下是这种操作如何运作的完整示例：
