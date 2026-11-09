
```objective-c
targetRect = NSMakeRect(0, 0, self.bounds.size.width-buttonWidth,
    self.bounds.size.height-buttonHeight);
[self drawSomeButtons];
}
-(void) mouseDown: (NSEvent *) theEvent {
[self removeTheButtons];
[self drawSomeButtons];
}
-(void) drawSomeButtons {
    for (int i = 0; i < buttonCount; i++) {
        //Create a button at a random point
        CGPoint thisPoint = CGPointMake(arc4random() % (int)targetRect.
            size.width, arc4random() % (int)targetRect.size.height);
        newButton = [[NSButton alloc]
            initWithFrame:NSMakeRect(thisPoint.x, thisPoint.y,
                buttonWidth, buttonHeight)];
        //Define the button style and set the title string
        [newButton setButtonType:NSMomentaryPushInButton];
        [newButton setBezelStyle: NSRoundedBezelStyle];
        [newButton setTitle: [NSString stringWithFormat:@"%i", i+1]];
        //Set a target/action method that
        //is triggered when the button is clicked
        [newButton setAction: @selector(buttonWasPressed:)];
        [newButton setTarget:self];
        //Add the button to the container view
        [self addSubview:newButton];
    }
}
-(void) removeTheButtons {
    //Get an array of subviews
    NSArray *theSubviews = [NSArray arrayWithArray:[self
        subviews]];
    //Remove them all with a single line of code
    [theSubviews
        makeObjectsPerformSelector:@selector(removeFromSuperview)];
}
-(void) buttonWasPressed: (id) sender {
    //When a button is pressed, log the title
    thisButton = (NSButton *) sender;
    NSLog(@"Pressed: %@", thisButton.title);
}
- (void)drawRect:(NSRect)dirtyRect {
    // Not used in this example - we're not drawing custom graphics
}
@end
```

图16.7展示了修改后的视图。当你点击一个按钮时，一个通用的方法会将其标题字符串（恰好也是其编号）记录到控制台。当你点击视图的其他位置时，按钮位置会被随机打乱。

### 图16.7

一个带有随机按钮的视图。点击视图可更改排列。当按钮被点击时，控制台会记录按钮编号。

![](img/2b293e29fc15b0797f113b85dd429b6e_434_0.png)

代码中的关键点包括：

- 对任何对象调用`removeFromSuperview`方法，会将其从视图层次结构中移除，同时释放其内存并将其从显示中移除。
- 在根视图上调用`addSubview:`方法并传入一个对象作为参数，会将该对象添加到层次结构中并显示出来。
- 按钮通过`alloc/init`创建，并伴随额外的初始化代码。通过调用`addSubview:`将它们添加到视图中。
- 按钮是活跃的。为每个按钮设置目标和动作，将其链接到名为`buttonWasPressed:`的方法，当用户点击按钮时触发。可以从按钮标题文本中读取按钮编号。
- 对数组中的按钮运行`makeObjectsPerformSelector:`方法，只需一行代码即可将它们全部移除，不需要枚举。
- 几何结构`NSRect`和`CGPoint`分别表示矩形和点。这些结构将在后面更详细地解释。

![](img/2b293e29fc15b0797f113b85dd429b6e_435_0.png)

**提示**  
这个应用程序并不试图避免按钮重叠；有时按钮会重叠在一起。尝试修改项目，使按钮永远不会出现在彼此上方。可能的解决方案有很多，可能需要一些枚举。

## 在视图中处理鼠标事件

查找鼠标位置通常很有用，无论是在单击或拖动事件期间，还是在视图内跟踪光标时。NSView支持多种鼠标跟踪方法，其中大多数在NSResponder中定义。要将它们添加到项目中，可以像下面所示这样实现自定义处理程序。你也可以从网站（www.wiley.com/go/cocoadeveloper）下载鼠标处理程序项目，查看完整示例。

mouseDown: 事件会被自动捕获。你可以通过以下代码获取窗口内的坐标：

```objective-c
- (void) mouseDown: (NSEvent *) theEvent {
    NSPoint mouseLocation = [theEvent locationInWindow];
    NSLog (@"Mouse position: %.0f, %.0f", mouseLocation.x,
        mouseLocation.y);
}
```

通常需要将坐标转换为某个子视图的坐标，并限制点击范围，使应用程序忽略子视图外部的点击。要转换坐标，请使用：

```objective-c
NSPoint mousePositionInPanel =
    [self convertPoint: mouseLocation toView: aTargetSubview];
```

转换之后，点击`aTargetSubview`的左下角会返回0,0。

要对子视图进行命中测试，请使用 mouse:inRect: 方法：

```objective-c
NSRect targetBounds = [aTargetSubview bounds];
if ( [self mouse: mousePositionInPanel inRect: targetBounds]) {…
```

如果鼠标点击发生在子视图内部，则条件中的代码会运行。子视图外部的点击将被忽略。

使用 mouseDragged: 接收左键拖动事件。你可以使用前面展示的相同代码读取鼠标位置。

![](img/2b293e29fc15b0797f113b85dd429b6e_436_0.png)

### 警告

**mouseDragged:**事件即使鼠标被拖出窗口框架之外也会持续到达。命中测试对于拖动事件变得更加关键；否则，你可能会在屏幕上拖动数值和对象，即使你并不想这样做。

使用**mouseMoved:**事件来捕获未按下左键时的鼠标光标位置。**mouseMoved:**跟踪默认是不启用的。要启用它，请在视图的`awakeFromNib:`方法中添加以下代码：

```objc
- (void) awakeFromNib {
    [[self window] setInitialFirstResponder: self];
    [[self window] makeFirstResponder: self];
    [[self window] setAcceptsMouseEvents: YES];
}
```

这会告诉根窗口对象将鼠标移动消息传递给视图进行处理。**mouseMoved:**跟踪在整个屏幕范围内处于活动状态，你应该对窗口边界进行命中测试以限制鼠标操作。

这只是可用鼠标方法中的一小部分。完整列表定义在NSResponder和NSView类参考中。其他有用的方法包括：

- `mouseUp:` 当左键释放时发送。
- `mouseEntered:` 当光标进入跟踪区域时发送。
- `mouseExited:` 当光标退出跟踪区域时发送。

使用`NSTrackingArea`类来定义跟踪区域对象。

## 理解Cocoa图形系统

要创建Cocoa图形，你必须理解：

- 点、矩形和其他基本数据如何打包到数据结构中，以及如何设置和读取其中的数据
- 点和其他元素如何组合以创建形状对象
- 形状对象如何绘制到视图中
- 颜色和渐变如何创建和管理
- 图像如何加载并绘制到视图中

本节其余部分将介绍这些基本技术和概念。

## 理解并定义基本几何

在Cocoa中，几何数据是正式且结构化的。没有像更简单语言中的`plot (x,y)`、`line (x1, y1, x2, y2)`或其他简单图形原语。点和矩形——`rect`——值被包装在数据结构中，这些结构在方法和函数中使用。所有组件都是浮点数。Cocoa坐标使用左下角原点。表16.2介绍了Cocoa的关键图形数据结构。请注意，这些不是类或对象——它们是标准的C结构体或对象属性。

| 数据结构 | 描述 |
|---|---|
| `NSPoint` | 任意x,y坐标对。使用`point.x`和`point.y`访问各个坐标。 |
| `NSSize` | 定义矩形的大小。使用`size.width`和`size.height`访问组件。 |
| `NSRect` | 具有`NSPoint`原点和`NSSize`的矩形。使用`rect.origin.x/y`访问原点，使用`rect.size.width/height`访问大小组件。 |
| `Frame` | 一个`NSRect`，其原点相对于对象的父视图定义。更改`origin`会移动对象在父视图中的左下角锚点。 |
| `Bounds` | 一个`NSRect`，其原点设置为0,0。使用`bounds`访问子视图的内部坐标。`frame`和`bounds`通常具有相同的大小。更改frame会拉伸内容。 |

![](img/2b293e29fc15b0797f113b85dd429b6e_437_0.png)

> **注意**
> 
> 没有`NSLine`结构，因为在Cocoa中没有直接绘制直线的方法。直线是使用更复杂的`NSBezierPath`对象定义的，该对象可以从线段、弧线和复杂曲线构建任意形状。

## 使用几何数据结构

一个常见的问题是获取视图的`NSRect`。要返回大小，请使用：

```
NSRect boundsRect = view.bounds;
```

然后你可以访问`boundsRect`的组件来查找宽度和高度。

你也可以直接访问组件。

```
float thisWidth = view.bounds.size.width;
```

要返回相对于矩形左下点在父视图中的位置，请使用：

```
NSPoint thisOrigin = view.frame.origin;
```

