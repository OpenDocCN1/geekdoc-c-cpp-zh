
在 32 位下运行的代码中，它被 typedef 为 float；在 64 位下运行的代码中，它被 typedef 为 double。无论如何，NSInteger 类型的变量不是指针，因此没有 *。³

这可能会让人困惑。NSNumber 是对象，而 NSInteger 不是。你需要查阅文档来弄清哪个是哪个。下面是你可能声明两个变量的方式，其中一个为 NSNumber，另一个为 NSInteger：

```objc
NSNumber *income;
NSInteger age;
```

Objective-C 还有用于处理布尔值的 BOOL 类型。我们通常不会为逻辑计算做那些花哨且难以阅读的算术运算。相反，我们把 BOOL 看作具有 YES 或 NO 值之一。在谈论布尔值时，我们特别小心不要使用 *true* 或 *false* 这样的词。我们不想让人觉得我们是外地人。

## 5.3 Getter 和 Setter

在 Greeter 类中，我们可以轻松获取和设置 name 的值。在下面示例的第一行高亮代码中，我们获取并打印 name 的值；在第二行高亮代码中，我们设置它的值：

下载 `Properties/HelloWorld12/Greeter.m`

```objc
#import "Greeter.h"

@implementation Greeter
-(NSString *) greeting {
    return [[NSString alloc] initWithFormat:@"Hello, %@!", name];
}
-(id) initWithName:(NSString *) newName {
    if (self = [super init]){
        name = newName;
    }
    return self;
}
-(id) init {
    return [self initWithName:@"World"];
}
```

3. 在这个 Stack Overflow 问题 http://stackoverflow.com/questions/2189212/why-object-doesomething-and-not-object-dosomething 的回答中，对对象和简单的 C 结构有很好的解释。该回答由 Apple 工程师 Bill Bumgarner 撰写，他使用的标准用户名是 bbum。他的 Stack Overflow 帖子以及他对各种其他邮件列表（例如 http://lists.apple.com 上的 cocoa-dev 列表）的贡献总是值得寻找。他不时会在自己的博客 http://www.friday.com/bbum/ 上总结自己的想法。

### Joe 问……

### 我必须遵循这些命名约定吗？

是的。遵循这些命名约定很重要，因为它们将实现你不久后就会看到的许多“魔法”。这些只是约定——编译器并不强制这些名称，但遵循它们*非常*重要。

```objc
-(NSString *)description {
    return [[NSString alloc] initWithFormat:@"name: %@ \n created: %@",
           name, [NSDate date]];
}
@end
```

如果我们想允许其他对象获取和设置 name 的值，我们会在 Greeter 头文件中声明一个 getter 和一个 setter，并在实现文件中实现它们。

getter 是一个实例方法，返回 name 实例变量的当前值，因此返回类型必须是 NSString *。getter 不接受任何参数。剩下唯一需要操心的是给它起什么名字。在 Objective-C 中，属性 xyz 的 getter 也命名为 xyz。你完全不需要把 *get* 插入名称中。

setter 也是一个实例方法。它不返回任何内容，但需要把 name 的新值作为一个 NSString * 接收，我们会把这个参数称为 name。至于方法名，在 Objective-C 中，属性 xyz 的 setter 命名为 setXyz。换句话说，你以 *set* 开头，后面跟上变量名，并将变量名的首字母转换为大写。

将这些访问器声明添加到你的头文件中：

下载 `Properties/HelloWorld13/Greeter.h`

```objc
#import <Cocoa/Cocoa.h>

@interface Greeter : NSObject {
    NSString *name;
}
-(NSString *) greeting;
-(id) initWithName:(NSString *)name;
-(NSString *) name;
-(void) setName:(NSString *) name;
@end
```

要看到它生效，你需要在 applicationDidFinishLaunching: 中像下面高亮行那样添加对该方法的调用：

下载 `Properties/HelloWorld13/HelloWorldAppDelegate.m`

```objc
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    Greeter *greeter = [self greeterFor:@"Maggie"];
    NSLog(@"Greeter: %@", greeter);
    NSTextField *label = [self labelWithText:[greeter greeting]];
    [self setUpperCasedName:greeter];
    [[self.window contentView] addSubview:label];
}
```

点击 Build & Run，你将看到类似下面的输出：

```
The name was originally Maggie.
The name is now MAGGIE.
```

现在让我们引入属性，并开始精简和简化我们的代码。

## 5.4 将访问器转换为属性

让我们盘点一下当前进度。我们已经公开了 Greeter 类的一个名为 name 的属性，并且可以获取和设置它。我们分三步完成了这件事：

- 1. 在头文件中声明一个名为 name 的实例变量。
- 2. 在头文件中声明一个名为 name 的 getter 和一个名为 setName: 的 setter。
- 3. 提供了大部分是样板代码的内容，在实现文件中实现这些方法。

现在我们将使用 Objective-C 2.0 属性来修改最后两步，并在某些情况下省去第一步。

将 getter 和 setter 的声明替换为以下内容：

下载 `Properties/HelloWorld14/Greeter.h`

```objc
#import <Cocoa/Cocoa.h>

@interface Greeter : NSObject {
    NSString *name;
}
-(NSString *) greeting;
-(id)initWithName:(NSString *)name;
@property(copy) NSString *name;

@end
```

暂时忽略编译器指令 @property 后面括号中的 copy。你应该把该高亮行的其余部分理解为声明一个名为 name、类型为 NSString 的属性。就目前而言，这一行声明了一个名为 name 的 getter 和一个名为 setName 的 setter。

如果你现在点击 Build & Run，代码会像以前一样正常工作。你将能够从 HelloWorldAppDelegate 调用 getter 和 setter，而不会出现任何警告或错误。换句话说，这个 @property 指令正在声明你的 getter 和 setter——事实上，它做的还不止这些，你将在第 96 页的 5.6 节 *属性特性* 中看到。

我们实现 getter 和 setter 方法的方式并没有什么特别之处。事实上，如果我们要求编译器这样做，它可以为我们创建实现。将你的 getter 和 setter 实现替换为以下高亮行：

`Download Properties/HelloWorld14/Greeter.m`

```objc
#import "Greeter.h"

@implementation Greeter

@synthesize name;
```

`@synthesize` 指令告诉编译器实现相应 `@property` 指令中声明的方法。

那么，让我们回顾一下创建属性的三个步骤。我们在头文件中的花括号之间声明一个实例变量。我们使用 `@property` 指令在头文件中花括号之外声明 getter 和 setter。到目前为止，我们只是在声明一个变量和一个属性（换句话说，访问器方法），这就是为什么我们在头文件中这样做。现在是时候实现我们为变量声明的方法了。实现放在 `.m` 文件中，所以我们要把 `@synthesize` 指令放在那里。

点击 Build & Run，程序应该会像以前一样正常工作。换句话说，getter 和 setter 正在被正确生成。

## 5.5 点表示法

既然你已经声明并合成了属性，就应该以不同的方式调用它们。当你想要调用 getter 时，我希望你使用点表示法，而不是你一直使用的方法调用语法。

换句话说，将以下内容：

```objc
[self name]
```

替换为：

```objc
self.name
```

要看到实际效果，这意味着你要把 greeting 方法中的代码改成下面这行高亮代码：

下载 `Properties/HelloWorld14/Greeter.m`

```objc
- (NSString *) greeting {
    return [[NSString alloc] initWithFormat:@"Hello, %@!", self.name];
}
```

同样，你会将下面这个版本的 setter：

```objc
[self setName:newName];
```

替换为：

```objc
self.name = newName;
```

这会把 initWithName: 方法改成这样：

下载 `Properties/HelloWorld14/Greeter.m`

```objc
- (id) initWithName:(NSString *) newName {
    if (self = [super init]) {
        self.name = newName;
    }
    return self;
}
```

在每种情况下，方法调用形式和点语法形式的行为都完全相同。事实上，点语法只是语法糖，会编译成方法调用形式。不过你会发现，如果你在获取和设置属性时始终使用点语法，代码会变得更容易阅读。

这让人感觉好像又回到了原点。以 setter 为例，我们一开始是这样直接设置变量的：

```objc
name = newName;
```

然后我们引入了 setter。现在你被告知要像这样使用 setter 方法来设置底层实例变量的值：

```objc
[self setName:newName];
```
