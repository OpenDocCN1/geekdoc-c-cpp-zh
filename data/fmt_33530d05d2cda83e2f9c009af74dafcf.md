
现在我们有了一个 Cocoa 实现，在设置时我们必须遵循引用计数规则，因此在移动和绘制三角形时，我们需要对三角形添加一个 `retain`。让我们看看实现中的其他差异。

### 创建路径

从 C 函数到 Objective-C 方法的翻译非常直接。例如，这个：

`CGPathMoveToPoint(path, NULL, 0, -173);`

变为以下 `UIBezierPath` 方法：

`[path moveTo:CGPointMake(0,-173)];`

你不需要将路径变量作为参数传递，因为你是在向它发送消息。在整个范围内进行类似的更改以获得三角形的 Cocoa 版本：

```objc
+(UIBezierPath *)triangle {

    UIBezierPath *path = [UIBezierPath bezier];

    [path moveTo:CGPointMake(0,-173)];

    [path addLineToPoint:CGPointMake(200,-173)];

    [path addLineToPoint:CGPointMake(-200,-173)];

    [path close];

    return path;

}
```

每个方法仅仅是 C 函数之上的一个薄薄的封装，但这种方法感觉更整洁。这就是为什么我们展示这种方法。

## 绘制圆和矩形

```objc
UIBezierPath *exclamationPoint = [[self exclamationPoint] retain];

[self centerPath:exclamationPoint];

[self fill:exclamationPoint initWithColor:[UIColor black]];

[exclamationPoint release];

[triangle release];
```

叹号由两个部分组成：顶部和底部的点。使用 `appendPath:` 来由这两个组件构建出叹号：

```objc
- (UIBezierPath *) exclamationPoint {

    UIBezierPath *path = [UIBezierPath bezierPath];

    [path appendPath:[self top]];

    [path appendPath:[self dot]];

    return path;

}
```

顶部是用 `bezierPathWithRect:` 方法创建的矩形，而底部是用 `bezierPathWithOvalInRect:` 创建的圆。

```objc
- (UIBezierPath *) top {

    return [UIBezierPath 
        bezierPathWithRect:CGRectMake(-20, -70, 40, 140)];

}
```

```objc
- (UIBezierPath *) dot {

    return [UIBezierPath 
        bezierPathWithOvalInRect:CGRectMake(-25, 95, 50, 50)];

}
```

从这里开始到本章结束，我们将对顶部进行细微调整以改变叹号的外观。例如，我们可以通过将矩形改为圆角矩形来稍微软化角：

```objc
- (UIBezierPath *) top {

    return [UIBezierPath 
        bezierPathWithRoundedRect:CGRectMake(-20, -70, 40, 140) 
        cornerRadius:8.0];

}
```

# 第 6 章：自定义绘制

![](img/06d76a71c379bfa5e6891245aa6bb22d_125_0.png)

我们可以使用等于矩形宽度一半的圆角来使角更加圆润：

```objc
Drawing/Bezier/Classes/Bezier.m

-(UIBezierPath *) top {

    return [UIBezierPath
        bezierPathWithRoundedRect:CGRectMake(-20, -70, 40, 40)
        cornerRadius:20.0];

}
```

这看起来就像我们在矩形的两端都放置了一个半圆：

![](img/06d76a71c379bfa5e6891245aa6bb22d_125_1.png)

接下来，我们将修改路径并从圆的弧添加到路径中。

## 6.4 不规则路径

我们将修改叹号顶部部分的路径，使其在底部变细。主要目的是确保它不是由矩形构建的：

![](img/06d76a71c379bfa5e6891245aa6bb22d_125_2.png)

Drawing/Bezier/Classes/Bezier.m

```objc
- (UIBezierPath *) top {

    UIBezierPath *path = [UIBezierPath bezierPath];

    [path moveTo:CGPointMake(-30, -70)];

    [path addLineTo:CGPointMake(30, -70)];

    [path addLineTo:CGPointMake(5, 70)];

    [path addLineTo:CGPointMake(-5, 70)];

    [path closePath];

    return path;

}
```

你已经看到如何从其他路径构建路径，以及如何从线条和曲线构建路径。组件部分虽然简单，但它们的组合可以非常强大且复杂。例如，对以下高亮部分进行更改，将叹号顶部和底部的线段替换为半圆。

![](img/06d76a71c379bfa5e6891245aa6bb22d_126_0.png)

Drawing/Bezier7/Classes/Bezier.m

```objc
- (UIBezierPath *) top {

    UIBezierPath *path = [UIBezierPath bezierPath];

    [path moveTo:CGPointMake(-30, -70)];

    [path appendPath:[UIBezierPath bezierPathWithArcCenter:CGPointMake(0, -70) radius:30 startAngle:M_PI endAngle:2*M_PI clockwise:YES]];

    [path addLineTo:CGPointMake(30, -70)];

    [path addLineTo:CGPointMake(5, 70)];

    [path appendPath:[UIBezierPath bezierPathWithArcCenter:CGPointMake(0, 70) radius:5 startAngle:0 endAngle:M_PI clockwise:YES]];

    [path addLineTo:CGPointMake(-30, -70)];

    return path;

}
```

对于每个圆弧，我们指定圆的中心和半径以及以弧度为单位的起始结束角度。我们还需要指示从开始到结束是顺时针还是逆时针移动。在我们的情况下，我们顺时针遍历每个弧。这部分部分是因为我们是沿着路径顺时针移动的。如果我们逆时针遍历弧，在末端就会是凹处而不是凸起。

![](img/06d76a71c379bfa5e6891245aa6bb22d_127_0.png)

如果你沿着相反的方向移动路径，你会得到凹处而不是凸起。尽管曲线看起来是平滑的，但实际上并非如此。不过请记住，本章的目的是介绍实用的技术。

## 6.5 使用贝塞尔曲线

`UIBezierPath` 类允许你绘制两种类型的曲线：二次和三次曲线。二次曲线由端点和一个控制点指定。起点是当前点，初始方向由第一个控制点设置。终点再次是第一个参数，结束方向由第二个控制点设置。结果是平滑连接每个侧的曲线。

```objc
[exclamationPoint release];

[triangle release];
```

```objc
(void)drawRect:(CGRect)rect {

  [self drawInCurrentContext];

}
```

如果我们进行编译并运行，将得到与之前相同的结果，但现在我们可以设置 PDF 上下文并使用 `drawInCurrentContext` 将我们的警告绘制到 Documents 目录下的 PDF 中。第一步，`pathToWarningFile` 返回我们将创建的路径，并使用 `applicationDocumentDirectory` 来保存 PDF。

```objc
Drawing/Bezier12/Classes/BezierView.m

(NSString *)applicationDocumentDirectory {

  return [[NSString searchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) lastObject];

}
```

```objc
-(NSString *)pathToWarningFile {

  return [[self applicationDocumentDirectory] stringByAppendingPathComponent:@"Warning.pdf"];

}
```

这为我们提供了 Documents 目录中 `Warning.pdf` 文件的路径。将其作为第一个参数传递给 `UIGraphicsBeginPDFContextToFile`，该函数用于创建并配置当前文本，以便创建一个将要保存的 PDF。另外两个参数是 `CGRect` 类型的页大小，以及一个包含文档信息的可选 `NSDictionary`。我们使用视图的尺寸作为页面的尺寸。你可以使用 `CGRectMake()` 来创建一个 `CGRect`，或者使用 `CGRectZero` 创建一个 8.5 x 11 英寸或 612 x 792 像素的页面。

与其将 PDF 保存到文件，你也可以使用 `UIGraphicsBeginPDFContextToData` 函数将 PDF 写入 `NSData` 对象中。我们将写入文件。

你首先创建一个新的 PDF，然后像绘制到屏幕上一样绘制到 PDF 页面。我们将在整个文档中使用完全相同的页面信息，以便我们可以使用 `UIGraphicsBeginPDFPage()` 方法。在创建新页面时，你可以使用 `UIGraphicsBeginPDFPageWithInfo()` 函数来更改页面信息。

如果你需要另一个页面，就再次开始这两个函数中的另一个。当你完成最后一页时，就结束 PDF 上下文。在我们简单的示例中，我们只有一个页面。以下是创建 PDF 的代码：

```objc
Drawing/Bezier12/Classes/BezierView.m

(void)drawRect:(CGRect)rect {

    [self drawInCurrentContext];

    UIGraphicsBeginPDFContextToFile([self pathToWarningFile], self.frame, nil);

    UIGraphicsBeginPDFPage();

    [self drawInCurrentContext];

    UIGraphicsEndPDFContext();

}
```

我们用于写入 PDF 的代码与写入屏幕的代码完全相同。唯一的区别在于，我们从设置上下文并创建一个新页面开始，并在结束时关闭上下文。在模拟器中编译并运行。你可以通过以下应用程序的路径找到你创建的 PDF：`Library/Application Support/iPhone Simulator/3.2/Applications`。你会看到一系列带有编号的目录。进入每个目录，直到找到我们的应用程序。找到与 Bezier 应用程序对应的目录，并查看其 `Documents` 目录。你应该能找到 `Warning.pdf` 文件。它包含了该符号。

| Bezier | Warning.pdf | 预览: |
| --- | --- | --- |
| Documents | | |
| Library | | |
| tmp | | ![⚠️] |

你可以在 Apple 的《iPad 编程指南》[App10b] 中的“图形与绘图”部分读到关于写入 PDF 的知识。

## 6.7 总结

`UIBezierPath` 类让绘图变得更容易且更强大。你始终有机会使用绘图程序生成一个图像文件，并在应用程序中使用它。如果绘图代码并不复杂，那么你应该倾向于自己绘图，而不是引入这样的图像。⁴

- 你将在 Jeff LaMarche 的一篇博客中看到对 Joe Cowan 评论的讨论。请从这个网站开始：http://iphonedevelopment.blogspot.com/2010/05/some-advice.html。

# 第 7 章

# 电影播放器

iPad 的核心设计是为媒体消费而设计的；巨大的手持屏幕非常适合图形显示，尤其是视频。在 iPhone 上，你只能在全屏查看器中显示视频，而 iPad 的 SDK 允许你将视频直接构建到应用程序中，并对其周围的用户体验进行完全自定义。SDK 还暴露了播放器的状态，因此你可以直接控制视频，并将其播放与你应用程序的其他部分进行协调。

在接下来的两个章节中，我们将探索电影播放器控制器：将其嵌入应用程序中、在其上方叠加其他视图、创建我们自定义的播放控制和播放列表、生成导航缩略图以及流媒体内容。如果你过去用过视频播放器框架，可能会发现它们很难使用。有了 Apple 的新框架，我们将拥有一个运行快速的复杂播放器。

## 7.1 为电影设置视图

在接下来的几页中，我们将从零开始在 iPad 应用程序中播放视频。一旦完成这一步，我们将退后一步详细查看 `MPMoviePlayerController` 架构，并让我们的实现变得更有趣。我们已经在 `MoviePlayer` 文件夹中为你准备了一个项目（如果你倾向于真正从零开始，可以创建一个基于视图的项目）。打开项目，你会发现我们已经在 `Resources` 目录下添加了一个名为...的视频

![](img/06d76a71c379bfa5e6891245aa6bb22d_133_0.png)

图 7.1：设置电影播放器视图

BigBuckBunny_640x360.m4v.¹ 我们还把 `MediaPlayer` 框架添加到了你的 `frameworks` 文件夹中。

我们将首先关注实例化一个 `MPMoviePlayerController` 来管理我们视频的播放。该类管理播放的所有细节，并提供一个你可以添加到视图层次结构以显示视频的视图。`MPMoviePlayerController` 还可以全屏显示我们的视频内容（我们将在本章稍后介绍这一点）。

让我们从在 Interface Builder 中打开 `MoviePlayerViewController.xib` 文件并添加一个可以包含 `MPMoviePlayerController` 视频的视图开始。首先选择 ModelAndViewController 的主视图，并将其背景颜色重置为纯黑色。然后从 Interface Library 拖入一个 `UIView` 到视图中。

1. 取决于你的分发
2. 为了确保我们没有理解，`MoviePlayerViewController` 是我们为应用程序编写的主视图控制器；`MPMoviePlayerController` 是 iOS 3.2 的一个类，由 Apple 编写，用于管理视频播放。

我们定义了一个名为 `viewFor` 的输出，并将其声明为属性。不要忘记在 `MoviePlayerViewController.m` 中添加同步。

```objc
movieplayer/Classes/MovieViewController.m

@synthesize viewFor;
```

现在让我们通过回到 Interface Builder 中的 `MoviePlayerViewController.xib` 文件来连接各个。我们将连接刚刚声明的 `IBOutlet`（对于 `viewFor`）。为此，按住 Control 点击 File Owner 并拖到新视图上。当连接弹出出现时，选择 `viewFor`，正如我们在下一页中所所示。

## 认识 MPMoviePlayerController

完成 Interface Builder 的工作后，让我们专注于代码。我们将通过在 `MoviePlayerViewController.h` 头文件中声明来添加 `MPMoviePlayerController` 类的实例。我们需要导入电影播放器的 `MPMoviePlayerController.h` 文件，以及 `player` 的属性声明。既然在这里了，我们还添加一个名为 `movieURL` 的方法声明（我们稍后会回到这里）。

```objc
movieplayer/MoviePlayer/Classes/MovieViewController.h

#import <UIKit/UIKit.h>
#import <MediaPlayer/MPMoviePlayerController.h>
```

```objc
@interface MoviePlayerViewController : UIViewController {

    UIView *viewFor;
    MPMoviePlayerController *player;
}
```

```objc
@property (nonatomic, retain) IBOutlet UIView *viewFor;
@property (nonatomic, retain) MPMoviePlayerController *player;
-(NSURL *)movieURL;
@end
```

让我们来看 `MoviePlayerViewController` 的实现。
我们从 `viewDidLoad` 方法开始并实例化 `MPMoviePlayerController`。让我们添加代码然后逐一分析：

```objc
movieplayer/MoviePlayer1/Classes/MoviePlayerViewController.m
```
