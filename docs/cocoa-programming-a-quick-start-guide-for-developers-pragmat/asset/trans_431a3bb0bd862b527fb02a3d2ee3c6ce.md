
```objc
-(void)awakeFromNib{
    [self addObserver:self
           forKeyPath:@"totalCount"
              options:NSKeyValueObservingOptionNew
              context:NULL];
}
-(void)observeValueForKeyPath:(NSString *)keyPath
                     ofObject:(id)object
                       change:(NSDictionary *)change
                      context:(void *)context {
    NSLog(@"%@", self.totalCount);
}
@end
```

除了 keyPathsForValuesAffectingTotalCount 之外，我们还在 awakeFromNib 方法中注册观察者。我们还有一个 totalCount 的 getter 方法，它返回 countOne 与 countTwo 之和。每当其中任一值发生变化时，都会从 observeValueForKeyPath:ofObject:change:context: 方法中调用它。作为响应，我们只是将总和记录到控制台。¹

本章带你了解了观察的基本原理。² 你注册一个对象，然后等待它被回调。这就像没有通知中心的通知。这只是两个对象之间的关系，并且只有观察者需要知道被观察者。你已经看到了如何向一个属性注册多个观察者，以及如何向多个属性注册单个观察者。最后，你看到了如何设置依赖变量，以便当它所依赖的变量发生变化时，其观察者会得到更新。

尽管 KVO 和 KVC 各自以及组合起来都很酷，但它们真正的威力在于它们所支持的技术。我们将通过 Bindings 从控制器层移除代码，并通过 Core Data 从模型层移除代码。

无论你是在为 Mac OS X 还是 iPhone OS 开发，都可以使用 KVO 和 KVC。如果你主要对为 Mac OS X 开发感兴趣，你会喜欢我们接下来要讲的内容。我们将看看这些技术如何支持绑定，从而让你为控制器层编写更少的代码。不幸的是，目前 iPhone OS 还不支持绑定。

- 1. 参见代码 zip 文件中的 KVO/Counter1，了解你可以移除 totalCount 实例变量和属性，并且仍然获得相同的行为。
- 2. 你可以在 Apple 的 Key-Value Observing Guide [App08] 中找到更多信息。

## 第21章：Cocoa Bindings

到目前为止，我们已经使用 Interface Builder 创建 GUI，并将按钮、标签、表格等连接到控制器和模型。这消除大量样板代码。你不需要继承 NSButton 并在代码中配置其外观和位置。从你使用自定义视图的经历中你会知道，你可以编写那些代码——只是你不必这样做。

Cocoa Bindings 关注控制器层，并问可以移除多少重复代码。事实证明，如果你注意使用符合 KVO 和 KVC 的类，答案是“大部分”。本章大部分时间我们会回到 Interface Builder 中建立连接并输入 keypath。我们会有少量代码要写，但不多。

我们将通过创建一个名为 CounterWithBindings 的新 Cocoa 应用程序来开始本章。你将添加一个名为 Counter 的新 Objective-C 类，声明一个类型为 NSNumber、名为 count 的属性，并合成它。这就是创建模型所需的全部代码。

至于视图，你将把一个步进器和一个文本字段拖到窗口中。随着本章的推进，我们会添加更多内容，但一开始这些就足够了。

剩下的是控制器。在本章中，你不会用代码实现控制器。你将利用 Cocoa Bindings 以及模型符合 KVC 和 KVO 这一事实，使用 Interface Builder 创建控制器。Cocoa Bindings 将让视图和模型通信，而无需我们编写大量样板胶水代码。我们将从回顾上一章的示例开始。

### 21.1 带 Bindings 的计数器的模型和视图

创建一个名为 CounterWithBindings 的新项目。添加一个名为 Counter 的新 Objective-C 类，其中包含属性 count。换句话说，你在头文件模板中添加两行代码：

```
Download Bindings/CounterWithBindings/Counter.h

#import <Cocoa/Cocoa.h>

@interface Counter : NSObject {
    NSNumber *count;
}
@property(copy) NSNumber *count;

@end
```

你还需要在实现文件中添加一行代码来合成属性 count：

```
Download Bindings/CounterWithBindings/Counter.m

#import "Counter.h"

@implementation Counter

@synthesize count;

@end
```

我们有一个定义了单个属性的单个类。在本章第一部分，这个应用程序中不会有其他代码。

现在让我们创建视图。将一个步进器和一个文本字段拖到主窗口中。和之前一样，使用 Attributes inspector 将步进器的行为设置为 Value Wraps。调整窗口大小，使其看起来像这样：

![](img/9355405953264484a02198b0e3d25b7e_334_0.png)

好。现在我们有了模型和视图。让我们创建控制器。

### 21.2 创建并连接 NSObjectController

在 Interface Builder 中，从 Library 中拖出一个 Counter 对象，并将其放到 Document 窗口中。这就是你的模型实例。

**Joe 问……**

**用代码不是更好吗？**

根据你的背景，这确实可能感觉如此。现在很多逻辑都转移到了你用 Interface Builder 设置的文件中。当遇到问题时，你不能使用你一直以来的技术。最初，定位问题会更难。另一方面，你也不太可能因为在本应是样板代码的地方犯错而造成这些问题。

Cocoa Bindings 可能令人害怕。但很快你就会知道出错时应该去哪里查找。如果你回想早期编程的日子，那时也是如此。你必须学会去哪里找问题。你可能盯着看了很久，才发现你本意是输入 ==，却输入了 =。所以，这与其说是新的挫折，不如说是老问题的新前沿。

接下来，从 Library 中拖一个 NSObjectController 到 Document 窗口。回想本书早期的示例。控制器位于模型和视图之间。控制器坚持充当中间人。你需要按照以下三个步骤配置控制器：

- 1. 连接到对象控制器所控制的对象。
- 2. 指定对象控制器负责哪些键。
- 3. 将每个元素绑定到对象控制器所控制的属性。

**连接控制器**

对象控制器需要知道它正在控制哪个对象。点击对象控制器，然后在 Connections inspector 中查看其 content outlet。将此 content 连接连接到 Counter 对象。你可以（并且很快就会）拥有多个相同类型的对象。这一步就是在指定对象控制器负责哪一个对象。

**选择键**

接下来，你需要让绑定到 NSObjectController 的对象可以使用 count 键。选择对象控制器，并使用 Attributes inspector 将类名设置为 Counter。注意有两种模式。我们在这里使用类模式，因为 Counter 是一个类。当我们用 Core Data 构建数据模型时，我们将使用实体模式。

你必须明确指定对象控制器将提供哪些键用于绑定。这里只有一个可能的选择。使用加号添加键 count。

![](img/9355405953264484a02198b0e3d25b7e_336_0.png)

**绑定组件**

点击文本字段以选中它，并使用 ⌘ 4 或直接点击检查器的第四个标签页来打开其 Bindings inspector。

![](img/9355405953264484a02198b0e3d25b7e_337_0.png)

在 Value 部分，选中“Bind to”复选框，并使用下拉列表选择 Object Controller。控制器键是 selection，模型键路径是 count。对步进器执行相同操作。

步进器和文本字段都绑定到 count 的值。点击 Build & Run。点击步进器，你可以看到文本字段的值发生了变化。到目前为止，这似乎不是什么很大的收益。但事实确实如此。

当你点击步进器时，它的值绑定到 count 的值，因此 count 会自动更新。类似地，文本字段绑定到 count 的值。每当 count 的值变化时，文本字段会自动更新。这些连接通过控制器建立。这里发生了很多活动。在下一节中，我们将添加更多小部件，以便更清楚地说明这一点。

### 21.3 绑定更多对象

向视图中添加一个圆形滑块和一个水平滑块。使用对象控制器将每个都绑定到 count。
