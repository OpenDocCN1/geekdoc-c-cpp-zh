

## 在桌面端实现 Platform

打开 **desktopMain** 文件夹中的 **Platform.kt**。

用以下代码块替换实际的实现：

```
actual class Platform actual constructor() {
    //1
    actual val osName = System.getProperty("os.name") ?: "Desktop"

    //2
    actual val osVersion = System.getProperty("os.version") ?: "---"

    //3
    actual val deviceModel = "Desktop"

    //4
    actual val cpuType = System.getProperty("os.arch") ?: "---"

    //5
    actual val screen: ScreenInfo? = null

    //6
    actual fun logSystemInfo() {
        print("($osName; $osVersion; $deviceModel; $cpuType)")
    }
}

actual class ScreenInfo actual constructor() {
    //7
    actual val width = 0
    actual val height = 0
    actual val density = 0
}
```

## 共享更多代码

你可能已经注意到，`logSystemInfo` 方法实际上反复使用了相同的字符串。为了避免这种代码重复，你可以借助 Kotlin 扩展函数。

打开 commonMain 文件夹中的 Platform.kt。如你所知，你无法在这里定义的属性或函数中添加实现，但没人说你不能使用 Kotlin 扩展函数。

在文件末尾添加以下代码：

```
val Platform.deviceInfo: String
    get() {
        var result = "($osName; $osVersion; $deviceModel; "
        screen?.let {
            result += "${it.width}x${it.height}@${it.density}x; "
        }
        result += "$cpuType"
        return result
    }
```

现在回到各平台的实际文件，在 `logSystemInfo` 函数中使用这个属性。

在 androidMain 的 Platform.kt 中：

```
actual fun logSystemInfo() {
    Log.d("Platform", deviceInfo)
}
```

在 iosMain 的 Platform.kt 中：

```
actual fun logSystemInfo() {
    NSLog(deviceInfo)
}
```

在 desktopMain 的 Platform.kt 中：

```
actual fun logSystemInfo() {
    print(deviceInfo)
}
```

## 更新用户界面

现在 Platform 类已经就绪，你在共享模块中的工作也完成了。KMP 会负责创建框架和库，你可以将它们用于每个需要说明的平台。这些内容在接下来的章节中也会对你有帮助。下面是它的样子：

## Android

你将在 androidApp 模块中完成所有任务。应用的基本结构已经为你准备好了。一些重要的文件需要解释，这些文件在接下来的章节中也会对你有帮助。下面是它的样子：

![](img/2f50555a40af4ea8c85f09e577f0c5b9_139_0.png)

在根文件夹中，有 AppScaffold.kt 和 AppNavHost.kt。这两个文件设置了应用的屏幕，并让它们之间的导航按预期工作。如果你感兴趣的话，不妨看一看。

应用有两个主屏幕：RemindersView（目前只显示简单的“Hello World”）和 AboutView（你将在本章中设置它）。打开它吧。

在这里，ContentView 是所有重要操作发生的地方。用以下代码片段替换其实现：

```
@Composable
private fun ContentView() {
    val items = makeItems()

    LazyColumn(
    modifier = Modifier.fillMaxSize(),
    ) {
    }
```

```
```kotlin
items(items) { row ->
    RowView(title = row.first, subtitle = row.second)
}
}
```

```

这里，你从 `makeItems` 函数中获取想要显示的项，并将它们放入 `LazyColumn`（基本上就是一个列表视图）。从 **Compose** 库导入 `Modifier`、`LazyColumn` 和 `fillMaxSize`。为 `items` 方法添加以下导入：

```
```kotlin
import androidx.compose.foundation.lazy.items
```

```

你很快就会实现 `RowView`。

在 `ContentView` 下方添加 `makeItems`：

```
```kotlin
private fun makeItems(): List<Pair<String, String>> {
    //1
    val platform = Platform()

    //2
    val items = mutableListOf(
        Pair("Operating System", "${platform.osName} ${platform.osVersion}"),
        Pair("Device", platform.deviceModel),
        Pair("CPU", platform.cpuType)
    )

    //3
    platform.screen?.let {
        val max = max(it.width, it.height)
        val min = min(it.width, it.height)

        items.add(Pair("Display", "${max}x${min} @${it.density}x"))
    }

    return items
}
```

+   1. 首先，你初始化了一个之前创建的 `Platform` 类的实例。
+   2. 接下来，你创建了包含标题和来自 `platform` 信息的成对数据，并将它们存储在一个可变列表中。
+   3. 尽管你知道 `screen` 属性在 Android 上不会是 null，但在面对可空属性时，稳妥总比后悔好。

从 `kotlin.math` 导入 `max` 和 `min`。作为这个应用的最后一个部分，添加 `RowView` 可组合函数，如下所示：

```
```kotlin
@Composable
```
```

