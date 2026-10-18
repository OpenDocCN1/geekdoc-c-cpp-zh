

## 6. 如果它与当前时区相同，那么你就知道它是合适的。
## 7. 检查该小时是否有效。
## 8. 如果遍历完每个小时，并且它是一个合适的小时，就将其添加到我们的列表中。
## 9. 返回小时列表。

导入 `min` 和 `max` 方法。现在，你已经为 Time Finder 应用编写好了业务逻辑！Android、iOS、桌面端和 Web 平台都可以共享它。

构建应用以确保它仍然可以编译。你可以再次尝试同时运行 Android 和 iOS。你会看到 iOS 构建失败，并出现如下所示的错误：

图 2.5 - Xcode 构建错误详情

请记住，你已经移除了 `greet` 方法。你会如何修复这个问题？

# 挑战

iOS 应用无法工作了。找出问题的原因，修复错误并让 iOS 应用重新正常工作。

# 要点

- Gradle 是大多数 KMP 项目的构建系统。
- 你用 Kotlin 编写 Gradle 构建文件。
- 你使用 **buildSrc** 模块来定义变量和插件。
- 你在 **shared** 模块中编写业务逻辑。
- **kotlinx-datetime** 库是一个用于处理日期和时间的多平台库。

# 接下来去哪里？

在本章中，你学习了如何使用 **buildSrc** 模块来设置项目，从而更轻松地更改版本。你还学习了如何在 **shared** 模块中处理日期和时间，使其适用于所有平台。

- Gradle：https://gradle.org/
- Kotlinx Datetime：https://github.com/Kotlin/kotlinx-datetime
- buildSrc：https://docs.gradle.org/current/userguide/organizing_gradle_projects.html#:

在下一章中，你将开始为 Find Time 项目构建 UI。

# Kotlin Multiplatform by Tutorials 第 3 章：开发 UI：Android Jetpack Compose

如果你查看 `setContent` 的源码，你会发现它是 `ComponentActivity` 上的一个扩展方法。该方法的最后一个参数就是你的 UI。这个参数的类型是 `@Composable`，这是一个特殊的注解，你需要在所有的 Compose 函数上使用它。一个 Compose 函数大致如下所示：

```
@Composable
fun showName(text: String) {
    Text(text)
}
```

最重要的部分是 `@Composable` 注解。它告诉 JC 这是一个可以绘制在屏幕上的函数。`Composable` 函数不会返回任何值。重要的是，你希望大多数函数都是无状态的。这意味着你将想要显示的数据传入，函数并不存储这些数据。这使得函数绘制得非常快。请参阅本章末尾的**接下来去哪里**一节，以了解更多关于 Compose 的工作原理。

你将开发一个多平台应用，让用户能够选择多个时区，并找出适合所有这些时区所有人的最佳会议时间。第一个屏幕如下所示：

在这里，你会看到本地的时区、时间和日期。其下方是两个不同的时区：纽约和伦敦。你的用户正试图找到这三个地点的共同会议时间。

> **注意**：这仅仅是原始的时区字符串代码。如果你有兴趣，可以挑战自己，将这些字符串代码替换为更具可读性的字符串。

当用户想要添加时区时，他们会点击悬浮操作按钮（FAB），然后会出现一个对话框，让他们选择所有想要的时区：

接下来是搜索屏幕，它允许用户选择一天中的开始和结束时间，并包含一个搜索按钮来显示可用的时间段。

## 主题

你需要学习的首批 Compose 函数之一就是主题。这是你为应用使用的配色方案。在 Android 中，通常会有 style.xml 或 theme.xml 文件，用于指定颜色、字体以及 UI 样式的其他方面。在 Compose 中，你使用主题函数。由于你已包含 Material Compose 库，你可以使用 MaterialTheme 类作为设置颜色、字体和形状的起点。Compose 还能告诉你系统是否正在使用深色主题。首先，在 androidApp 模块中，在与 MainActivity 相同的层级创建一个新包，并将其命名为 theme。

接下来，在该包中创建一个名为 **Colors.kt** 的新文件。添加以下代码：

```
import androidx.compose.ui.graphics.Color

val primaryColor = Color(0xFF1e88e5)
val primaryLightColor = Color(0xFF6ab7ff)
val primaryDarkColor = Color(0xFF005cb2)
val secondaryColor = Color(0xFF26a69a)
val secondaryLightColor = Color(0xFF64d8cb)
val secondaryDarkColor = Color(0xFF00766c)
val primaryTextColor = Color(0xFF000000)
val secondaryTextColor = Color(0xFF000000)
```

这部分定义了一些主色和次色。你可以在左侧边距看到这些颜色。如果你想要不同的配色方案，可以更改它们。接下来，右键单击 theme 目录，创建一个名为 **Typography.kt** 的新 Kotlin 文件。添加以下代码：

```
import androidx.compose.material.Typography
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.text.TextStyle
import androidx.compose.ui.text.font.FontFamily
import androidx.compose.ui text.font.FontWeight
import androidx.compose.ui.unit.sp

// 1
val typography = Typography(
```

## 类型

在进入主屏幕之前，你需要一些将在整个应用中使用的类型。在 ui 文件夹中，创建一个名为 Types.kt 的新文件。添加以下代码：

```
import androidx.compose.runtime.Composable

// 1
typealias OnAddType = (List<String>) -> Unit
// 2
typealias onDismissType = () -> Unit
// 3
typealias composeFun = @Composable () -> Unit
// 4
typealias topBarFun = @Composable (Int) -> Unit

// 5
@Composable
fun emptyComposable() {
}
```

1. 定义一个名为 OnAddType 的别名，它接收一个字符串列表并且不返回任何内容。
2. 定义一个在关闭对话框时使用的别名。
3. 定义一个 Composable 函数。
4. 定义一个接收整数的函数。
5. 定义一个空的 Composable 函数（用作顶部栏的默认变量）。

现在你已经设置好颜色和文本样式，是时候创建你的第一个屏幕了。

## 主屏幕

在 androidApp 模块的 ui 文件夹中，创建一个名为 MainView.kt 的新 Kotlin 文件。你将首先创建一些辅助类和变量。首先，添加你需要的导入语句（这样可以节省一些导入时间）：

```
import androidx.compose.foundation.layout.padding
import androidx.compose.material.BottomNavigation
import androidx.compose.material.BottomNavigationItem
import androidx.compose.material.FloatingActionButton
import androidx.compose.material.Icon
import androidx.compose.material.Scaffold
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Add
import androidx.compose.material.icons.filled.Language
import androidx.compose.material.icons.filled.Place
```

