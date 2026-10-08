
对于 iPhone 应用，标签栏显示中的标签最大数量为五个。对于 iPad 应用，如果你有的标签超过了最大值，标签栏控制器会自动显示一个“更多”（More）标签，列出其余的项目。你将在接几个章节中看到它是如何工作的。

## 初始化 UITabBarController 类 (Initializing the UITabBarController class)

`UITabBarController` 类用于为你的应用程序添加标签栏。要初始化标签栏控制器，创建一个视图控制器数组，并将其分配给标签栏的 `viewController` 属性。你在 `applicationDidFinishLaunching:` 中将标签栏控制器的视图添加到窗口中。请看下方的示例代码：

```
(void)applicationDidFinishLaunching:(UIApplication*)app
{
    // 初始化视图控制器
    SomeViewController *firstViewController = ...;
    AnotherViewController *secondViewController = ...;
    YetAnotherViewController *thirdViewController = ...;

    // 初始化数组
    NSArray *viewControllers = [NSArray arrayWithObjects:

firstViewController,
secondViewController,
thirdViewController,
nil;
```

```
// 初始化标签栏控制器
tabController = [[UITabBarController alloc] init];
```

```
// 设置视图控制器
tabController.viewControllers = viewControllers;
```

```
// 将标签栏控制器的视图添加到窗口
[window addSubview:tabController.view];
```

```
// 显示窗口
[window makeKeyAndVisible];
}
```

标签栏按照你添加视图控制器的顺序为视图控制器创建标签。在之前的代码中，`firstViewController` 显示在第一个标签上，`secondViewController` 显示在第二个，`thirdViewController` 显示在第三个上。

## 还有一点 (ONE MORE THING)

> 查看关于 `UITab` 类的 Apple 文档。当你读完这本书时，Apple 文档将是你学习新编程主题的好朋友。养成在书中遇到任何新类或概念时都查看文档的习惯是很好的。你未来的自己会感谢现在如此自律。

## 自定义标签栏按钮 (Customizing the Tab Bar Buttons)

可以通过编辑视图控制器的 `tabBarItem` 属性来自定义标签本身。在之前的代码中，你需要编辑 `navigationItem` 属性来为每个视图控制器自定义导航栏，标签栏项的工作也是类似的。

每个标签可以编辑的两个属性：图标和文本。在设置图标图像时，有几个规则需要记住：

### 第3部分：多视图应用程序 (Part 3: Multi-View Applications)

- 图像尺寸应约为 30x30 像素。如果图像太大，图像会自动缩放以适应。

- 图像的 alpha 值用于确定图标的形状。图像中 alpha 值为 1 的区域将被完全填充。alpha 值为 0 的区域将为空。图像中的颜色会被忽略，因此若要产生特定形状，你需要调整图像的 alpha 值。

![](img/5eb8ee1dd8eb3ab735869e75af92d0ef_235_0.png)

### 定义 (DEFINITION)

图像的 alpha 值决定图像的透明度。alpha 值的范围从 0（完全不可见）到 1（完全可见）。

- PNG 是使用标签的最佳图像格式——以及你应用程序中的其他地方。

![](img/5eb8ee1dd8eb3ab735869e75af92d0ef_235_1.png)

### 在崩溃中学习 (CRASH AND LEARN)

JPEG 图像不支持透明度，因此它们不应用于标签图标。

你不需要编辑现有的 `tabBarItem` 属性，而需要在视图控制器初始化时创建一个新的 `UITabBarItem`。要查看如何设置自定义标签栏项，请检查以下：

```
// 初始化标签栏项
UITabBarItem *tabBarItem = [[UITabBarItem alloc]
initWithTitle:@"Web"
image:[UIImage imageNamed:@"icon.png"]
tag:0];
```

```
// 设置标签栏项
tabController.viewControllers[0].tabBarItem = tabBarItem;
```

## 标签过多 (Too Many Tabs)

正如前面提到的，标签栏空间只能容纳五个标签。但是，如果你超过了五个，标签栏控制器会在末尾自动插入一个“更多”（More）。你可以从以下截图中看到这个标签：

![](img/5eb8ee1dd8eb3ab735869e75af92d0ef_236_0.png)

![](img/5eb8ee1dd8eb3ab735869e75af92d0ef_236_1.png)

编辑按钮

标签溢出视图

标签布局视图控制器

当你有六或更多视图控制器时，会自动显示更多标签。你不需要任何操作来启用更多标签。这种溢出行为是免费提供的。

事实上，用户可以通过点击溢出视图中的编辑按钮来编辑标签顺序。结果视图右所示。

## 结合标签栏与导航控制器

由于导航控制器是 ViewController 的子类，你可以像添加自己的 ViewController 子类一样轻松地将它们添加到标签栏。只需将你的视图控制器封装在 `UINavigationController` 中，并将导航控制器添加到标签栏。例如，让我们采用之前相同的标签栏初始化代码，并将其中一个视图控制器放入导航控制器：

```
(void)applicationDidFinishLaunching:(UIApplication*)app
{
// 初始化视图控制器
    SomeViewController *firstViewController = ...;
    AnotherViewController *secondViewController = ...;
    YetAnotherViewController *thirdViewController = ...;
```

```
// 将第一个视图控制器封装在导航控制器中
INavigationController *navController = 
[[INavigationController alloc]
initWithRootViewController:firstViewController];
```

```
// 初始化数组
NSArray *viewControllers = [NSArray arrayWithObjects:

navController,
secondViewController,
thirdViewController,
nil];
```

```
// 内存管理
[navController release];
```

```
// 像常一样继续标签栏初始化
...
```
