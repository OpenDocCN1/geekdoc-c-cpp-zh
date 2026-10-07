

# 列表 7-3 实例方法的实现

```objc
1 - (id)initWithName:(NSString*)newName atFrequency:(double)newFrequency {
2 self = [super init];
3 if (self != nil) {
4 _name = newName;
5 _frequency = newFrequency;
6 }
7 return self;}
```

列表 7–3 展示了你的广播电台类中一个实例方法的实现。一个初始化方法接受一个新的名称和频率。许多 OS X 和 iOS 类都有类似的初始化实例方法。与其先初始化类然后单独设置各种值，许多许多类初始化方法允许使用特殊的初始化方法，或者在本例中，在初始化时传递多个值。

在前面的示例中，第 1 行是你方法的接口，它包含两个参数：`newName` 和 `newFrequency`。要使用此方法，调用者只需执行以下操作：

```objc
RadioStation my = [[RadioStation alloc] initWithName:@"WOW FM" atFrequency:102.5];
```

该方法还定义为返回一个 `id`。`id` 是一个通用对象，所有的 Objective-C 对象都是 `id` 类型，就像 `RadioStation` 是一个对象一样。现在，让我们来看剩余的实现。

第 2 行引用了你不需要在任何地方定义的特殊变量。关键字 `self` 用于表示“该类的此实例”，因此第 2 行正在分配“该类的此实例”——即使用特殊变量 `super init` 返回的值。关键字 `super` 是“超类”的缩写，它可以被认为是“类的父类”。任何初始化方法通常都会被认为类似于第 2 行的结构。

为什么第 2 行是必要的？嗯，如果你有一个派自另一个对象的对象（记住，类是 `RadioStation : NSObject`），你必须告诉父对象初始化它自己。父对象通过告诉它的父对象初始化它自己来执行相同的操作，直到到达顶层对象。如果另一个类使用你的类作为父类，你的代码也必须获取一个 `init` 调用，以便 `RadioStation` 可以被初始化。这是 Objective-C 现实世界中的标准问题。类在创建时需要告诉它的父类初始化它自己，每当类消失时，需要告诉父类释放它自己。

第 3 行检查 `[super init]` 调用是否成功。如果成功，`self` 的值将是 `nil` 以外的值，这个值实际上意味着“未初始化”。

第 4 行和第 5 行将该类的实例变量设置为传入此方法的值。

第 8 行将 `self` 返回给调用者。就像调用 `[super init]` 一样，你的初始化函数需要将新对象返回给调用者。

# 使用新类

你创建了一个简单的 `RadioStation` 类，但单靠它并不能做什么。在这一节中，你将创建一个类并维护一个 `RadioStation` 类列表。

# 创建你的项目

启动 Xcode（见图 7–1）并创建一个名为 RadioStations 的新项目。

![](img/322e107ddf8f5cd963a6efafdcd86f38_146_0.png)

图 7–1. 打开 Xcode 以便创建新项目。

- 1. 确保你选择了 iOS application 并选中了 Single Application 模板，如图 7–2 所示。
- 2. 选中模板后，点击 Next 按钮。

![](img/322e107ddf8f5cd963a6efafdcd86f38_147_0.png)

**图 7–2. 在新项目窗口中选择模板**

- 3. 接下来，将 Product Name（应用程序名称）设置为 RadioStations。
- 4. 设置 Company Identifier（用一个虚拟公司即可）并将 Device Family 设置为 iPhone（如图 7–3 所示）。同时，确保勾选了“Use Automatic Reference Counting”。

# 第 7 章：Objective-C 类、对象和方法

![](img/322e107ddf8f5cd963a6efafdcd86f38_148_0.png)

图 7-3. 为新的 iPhone 应用程序命名

- 5. 点击 Next 按钮，Xcode 会问你想将新项目保存在什么位置。你可以将项目保存在桌面上或 Home 文件夹的任何地方。我喜欢桌面，因为它容易找到。一旦你做出选择，只需点击 Create 按钮。
- 6. 一旦点击 Create 按钮，Xcode Workspace 窗口应该是可见的，如图 7–4 所示。

# 第 7 章：Objective-C 类、对象和方法

![](img/322e107ddf8f5cd963a6efafdcd86f38_149_0.png)

# 添加对象

现在，你可以添加新对象了。

- 1. 首先，创建你的 `RadioStation` 对象。右键点击 RadioStations 组文件夹并选择 New File...（如图 7–5 所示）。

![](img/322e107ddf8f5cd963a6efafdcd86f38_149_1.png)

- 2. 下一个屏幕（如图 7–6 所示）询问新的文件类型。只需从 Cocoa Touch 组选择 Objective-C class，然后点击 Next。

![](img/322e107ddf8f5cd963a6efafdcd86f38_150_0.png)

**图 7–6.** 选择新的文件类型

- 3. 在下一个屏幕上，输入“RadioStation”作为类名，并选择 NSObject 作为“Subclass Of”。这意味着你的新类将是 NSObject 的子类，如图 7–7 所示。

# 第 7 章：Objective-C 类、对象和方法

![](img/322e107ddf8f5cd963a6efafdcd86f38_151_0.png)

图 7–7. 选择你新对象的子类

- 4. 下一个屏幕询问你要在哪里创建文件。只需点击 Create 按钮即可，因为 Xcode 选择保存文件的位置在当前项目内部，如图 7–8 所示。

![](img/322e107ddf8f5cd963a6efafdcd86f38_152_0.png)

图 7–8. 选择创建文件的位置

- 5. 你的项目窗口现在应该像图 7–9 所示。

![](img/322e107ddf8f5cd963a6efafdcd86f38_152_1.png)

图 7–9. 你的项目窗口

# 编写实现

RadioStation.h 现在定义了实例变量、类方法和实例方法。让我们进入实现文件。

- 1. 你在此使用的实现文件相对于我们的示例进行了简化，但它可以完美运行我们的电台模拟。
- 2. 你的项目窗口现在应该像图 7–10 所示。

![](img/322e107ddf8f5cd963a6efafdcd86f38_153_0.png)

图 7–10. 实现

- (id)initWithName:(NSString*)newName atFrequency:(double)newFrequency {
    self = [super init];
    if (self != nil) {
        _name = newName;
        _frequency = newFrequency;
    }
    return self;
}
- (NSString *)name {
    return _name;
}
- (void)setName:(NSString *)newName {
    _name = newName;
}
- (double)frequency {
    return _frequency;
}
- (void)setFrequency:(double)newFrequency {
    _frequency = newFrequency;
}

```

# 列表 7–4 TheStation 实现文件

```objc
#import "RadioStation.h"

@implementation RadioStation

- (id)initWithName:(NSString*)newName atFrequency:(double)newFrequency {
    self = [super init];
    if (self != nil) {
        _name = newName;
        _frequency = newFrequency;
    }
    return self;
}

- (NSString *)name {
    return _name;
}

- (void)setName:(NSString *)newName {
    _name = newName;
}

- (double)frequency {
    return _frequency;
}

- (void)setFrequency:(double)newFrequency {
    _frequency = newFrequency;
}

@end
```

# 列表 7–5 更新后的 ViewController.h 接口文件

```objc
#import <UIKit/UIKit.h>

@class RadioStation;

@interface ViewController : UIViewController {
    RadioStation *myStation;
    IBOutlet UILabel* stationName;
    IBOutlet UILabel* stationFrequency;
    IBOutlet UILabel* stationBand;
}
@end
```

# 列表 7–6 ViewController.m 文件

```objc
#import "ViewController.h"

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // 初始化代码将放在这里
}

@end
```

