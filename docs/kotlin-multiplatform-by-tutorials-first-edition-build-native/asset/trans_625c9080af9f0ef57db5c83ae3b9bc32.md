
组件。然而，由于它的可扩展性以及处理软件开发中各种问题的能力，它在专业人士中非常受欢迎——尤其是当他们想要创建大型应用程序时。

![](img/2f50555a40af4ea8c85f09e577f0c5b9_152_0.png)

上面的圆圈代表了应用程序中软件的不同层级。关于此图，有两条原则需要牢记：

- 1. 最里面的圆最抽象，最外面的圆最具体。这被称为**抽象原则**。抽象原则规定内层圆应包含业务逻辑，外层圆应包含实现细节。换句话说，离中心越近，对特定平台的依赖就越少。
- 2. 整洁架构的另一条原则是**依赖规则**。这条规则规定每个圆只能依赖于最近的内层圆——这正是让架构运转起来的关键。这使基于整洁架构的代码相当解耦，因此也易于测试。

整洁架构的基本组件如下，从外层圆向内层圆解释：

- **表示层与框架层**：最外层通常包含特定于平台的框架和工具。使用 SwiftUI 制作界面？就是这里。使用 Room 作为数据库？它也属于这里。这一层的代码通常无法在平台之间共享。
- **控制器或表示器**：这一层相当于你在 MVC 中的 Controller 或 MVVM 中的 ViewModel。它们接收来自外层的数据，并将其传递给下一层。你可以将 MVVM 和 MVC 与整洁架构结合使用。这也是一件好事，因为你的控制器或 ViewModel 的职责会减少。
- **用例或交互器**：这一层定义了用户可以触发的操作。前一层的对象可以访问用例，并且只能调用已定义的交互。在整洁架构的原始定义中，这一层是你放置业务逻辑的地方。由于你可以自由地添加自己的层，你也可以将这一职责委托给更内层的部分。
- **实体**：所有数据源的抽象定义。它可以包含一些业务逻辑。

在创建 Organize 应用时，你将使用 MVVM 设计模式。你可以自由选择任何你更喜欢的设计模式用于你的应用程序。

## 共享业务逻辑

当你尽量减少重复编写的代码时，KMP 的优势就显现出来了。在上一章中，你为“关于设备”页面编写了两次逻辑。这些代码完全可以放在共享模块中，所有平台都能加以利用。

## 创建 ViewModel

在 Android Studio 中打开入门项目。它基本上是上一章的最终项目。

在 shared 模块中 commonMain 文件夹的 presentation 目录下，创建一个新文件并将其命名为 `BaseViewModel.kt`。

用这行代码填充文件：

```
expect abstract class BaseViewModel()
```

你对该行代码很熟悉。不过，这次它定义的是一个抽象类，我们应用中的所有 ViewModel 都将继承它。接下来，你将在三个平台上实现该类的具体实现。

将光标放在类名的中间，按 Alt+Enter。Android Studio 将帮助你创建所有需要的 actual 文件。重复此过程，直到类名下方表示文件缺失错误的红线消失。

![](img/2f50555a40af4ea8c85f09e577f0c5b9_154_0.png)

图 7.3 - 在 expect 类名上按 Alt+Enter

> **注意：** 如果 Android Studio 未能自动为你创建所需的 actual 文件，请不要担心。在缺失平台文件夹中的同一包内，创建一个同名文件即可。

打开 **BaseViewModel.kt** 的 Android 版本，并将内容替换为这行代码：

```
actual abstract class BaseViewModel : ViewModel()
```

不要忘记导入所需的包：

```
import androidx.lifecycle.ViewModel
```

在 Android 上，ViewModel 应继承 *Lifecycle* 版本的 `ViewModel`，以便它们能够适应设备上的配置变更。

如果这对 iOS 开发者来说有点困惑，这里做一个简短的解释：

在 Android 上，当配置发生变化时——例如设备旋转、用户更改系统级主题或语言区域——系统会重新创建所有视图组件。然而，系统会在内存中保留从 AndroidX 的 Lifecycle 包继承的 ViewModel 的同一实例。因此，你可以将视图数据保存在 ViewModel 中，并将其应用到新创建的视图组件上，用户不会察觉到任何变化。

对于 iOS 和桌面端，你不需要继承任何东西。Android Studio 为这些平台生成的 actual 文件已经足够了。它们看起来像这样：

```
actual abstract class BaseViewModel actual constructor()
```

## 创建 AboutViewModel

既然你有了一个基础的 viewmodel，是时候创建具体的版本了。首先在 commonMain 文件夹的 presentation 目录下创建一个名为 `AboutViewModel.kt` 的文件。

定义该类并使其继承你之前创建的 BaseViewModel。

```
class AboutViewModel: BaseViewModel() {
    }
```

在类内部，创建一个 Platform 类的实例，并按 Alt + Enter 导入它。

```
private val platform = Platform()
```

在 AboutViewModel 类内部定义一个数据类，用于保存“关于”页面每一行显示的数据：

```
data class RowItem(
    val title: String,
    val subtitle: String,
)
```

接下来，创建一个生成“关于”页面项的函数。你在上一章中为每个平台编写了相同的逻辑三次。稍后你会将它们全部移除。

```
private fun makeRowItems(platform: Platform): List<RowItem> {
    val rowItems = mutableListOf(
        RowItem("Operating System", "${platform.osName} ${platform.osVersion}"),
        RowItem("Device", platform.deviceModel),
        RowItem("CPU", platform.cpuType),
    )
    platform.screen?.let {
        rowItems.add(
            RowItem(
                "Display",
                "${max(it.width, it.height)} × ${min(it.width, it.height)} @${it.density}x"
            ),
        )
    }
    return rowItems
}
```

最后，创建一个实例属性来存储该函数的结果，以避免重新创建数据。毕竟，这些数据永远不会改变，而是相对静态的。

```
val items: List<RowItem> = makeRowItems(platform)
```

这将是 ViewModel 的公共 API。

## 在视图层中使用 AboutViewModel

### Android

打开 androidApp 模块中的 AboutView.kt。

移除 `makeItems()` 方法，因为类似实现现在已存在于 AboutViewModel 中。

接下来，编辑 AboutView 方法的定义，以考虑 viewmodel：

```
@Composable
fun AboutView(
    viewModel: AboutViewModel = AboutViewModel(),
    onUpButtonClick: () -> Unit
) {}
```

现在为 `viewModel` 参数提供一个默认值。在后面的章节中，你将向代码中引入依赖注入并改进这种实例化方式。

之后，更新 ContentView 方法如下：

```
@Composable
private fun ContentView(items: List<AboutViewModel.RowItem>) {
    LazyColumn(
        modifier = Modifier.fillMaxSize(),
    ) {
        items(items) { row ->
            RowView(title = row.title, subtitle = row.subtitle)
        }
    }
}
```

你将把该函数渲染所需的 items 作为参数注入。你还移除了现在不必要的 `makeItems` 方法调用。

现在 `ContentView` 方法需要一个参数，回到 AboutView 的实现中传递 items。将 ContentView() 替换为：

```
ContentView(items = viewModel.items)
```

构建并运行 Android 应用。它和之前一样工作，但这次使用了 viewmodel。

![](img/2f50555a40af4ea8c85f09e577f0c5b9_157_0.png)

### iOS

打开 Xcode 项目并切换到 AboutView.swift。

在文件顶部，确保通过添加这行代码来导入共享模块：

```
import shared
```

接下来，在 AboutView 结构体内部，为 viewmodel 添加一个属性：

```
@StateObject private var viewModel = AboutViewModel()
```

你用 `@StateObject` 指令来注解该属性，以便让 SwiftUI 创建

