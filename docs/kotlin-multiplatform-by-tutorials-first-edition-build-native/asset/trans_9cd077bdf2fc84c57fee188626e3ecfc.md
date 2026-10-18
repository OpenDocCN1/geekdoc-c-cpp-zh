

## AddTimeZoneDialog

从 `shared-ui` 模块的 `commonMain/kotlin/com/raywenderlich/compose/ui` 文件夹中打开 `AddTimeZoneDialog.kt`。你会看到以下导入语句报错：

```kotlin
import androidx.compose.ui.res.stringResource
import androidx.compose.ui.window.Dialog
import com.raywenderlich.findtime.android.R
```

这三个导入在 `shared-ui` 模块中不存在。删除它们。在导入之后添加：

```kotlin
@Composable
expect fun AddTimeDialogWrapper(onDismiss: onDismissType, content: @Composable () -> Unit)
```

这是一个使用 KMM 的 `expect` 关键字的 Composable 函数。这意味着该模块使用的每个目标平台都需要实现这个函数。现在，用以下代码修改 `AddTimeZoneDialog` 函数的签名以及到第一个 `Column` 之前的代码：

```kotlin
fun AddTimeZoneDialog(
    onAdd: OnAddType,
    onDismiss: onDismissType
) {
    val timezoneHelper: TimeZoneHelper = TimeZoneHelperImpl()

    AddTimeDialogWrapper(onDismiss) {
}
```

这只是使用 `AddTimeDialogWrapper` 函数来包装现有代码。`AddTimeDialogWrapper` 函数将处理平台特定的代码。Android 和桌面端会以不同的方式处理对话框。转到该函数的末尾，添加一个结尾的 `}`。

使用 Desktop Compose 时的一个问题是资源处理。这超出了本章的范围。现在，只需将字符串资源改为硬编码字符串。将：

```kotlin
stringResource(id = R.string.cancel)
```

改为：

```kotlin
"Cancel"
```

将：

```kotlin
stringResource(id = R.string.add)
```

改为：

```kotlin
"Add"
```

在 `shared-ui/src/androidMain/kotlin/com/raywenderlich/compose/ui` 文件夹中，右键单击并创建一个名为 `AddTimeDialogWrapper.kt` 的新 Kotlin 文件。这将是实现 `commonMain` 中定义的 `expect` 的 Android 版本。添加：

```kotlin
import androidx.compose.runtime.Composable
import androidx.compose.ui.window.Dialog
import com.raywenderlich.compose.ui.onDismissType

@Composable
actual fun AddTimeDialogWrapper(onDismiss: onDismissType, content: @Composable () -> Unit) {
    Dialog(
    onDismissRequest = onDismiss) {
    content()
    }
}
```

这会创建一个接受关闭回调函数和对话框内容的函数。需要它的原因是 `Dialog` 是 JC 特有的，而不属于 CM。确保添加文件时，它属于 `com.raywenderlich.compose.ui` 包（如果还不是的话）。右键单击 `desktopMain/kotlin/com/raywenderlich/compose/ui` 并创建相同的类 `AddTimeDialogWrapper.kt`。添加：

```kotlin
import androidx.compose.runtime.Composable
import androidx.compose.ui.Alignment
import androidx.compose.ui.unit.Dp
import androidx.compose.ui.unit.DpSize
import androidx.compose.ui.unit.dp
import androidx.compose.ui.window.Dialog
import androidx.compose.ui.window.DialogState
import androidx.compose.ui.window.WindowPosition
import androidx.compose.ui.window.rememberDialogState
```

```kotlin
@Composable
actual fun AddTimeDialogWrapper(onDismiss: onDismissType, content:
@Composable () -> Unit) {
    Dialog(onCloseRequest = { onDismiss() },
        state = rememberDialogState(
            position = WindowPosition(Alignment.Center),
        ),
        title = "Add Timezones",
        content = {
            content()
        })
}
```

这个类类似，你可能会问为什么需要创建这个包装器。它们都引用了 `import androidx.compose.ui.window.Dialog`。但如果按住 Command 点击这些导入，你会看到它们指向两个不同的文件。CM 插件会对包进行一些替换，使两个库能协同工作，但某些代码必须不同，`Dialog` 就是这样一个例子。这里的 `Dialog` 接受一个关闭回调、状态、标题和内容。幸运的是，代码量不多。大部分 Compose 代码都在 **AddTimeZoneDialog** 中。

## MeetingDialog

与 `AddTimeZoneDialog` 非常相似，你需要修改 `MeetingDialog`。打开 `MeetingDialog.kt` 并删除显示为红色的导入。添加另一个包装器：

```kotlin
@Composable
expect fun MeetingDialogWrapper(onDismiss: onDismissType, content:
@Composable () -> Unit)
```

这与其他对话框包装器一样。现在用以下代码修改 `MeetingDialog` 方法直到 `Column`：

```kotlin
fun MeetingDialog(
    hours: List<Int>,
    onDismiss: onDismissType
) {

    MeetingDialogWrapper(onDismiss) {
```

这为对话框添加了一个包装器。确保像之前一样添加一个结尾的 `}`。

将：

```kotlin
stringResource(id = R.string.done)
```

改为：

```kotlin
"Done"
```

在 `src/androidMain/kotlin/com/raywenderlich/compose/ui` 文件夹中，右键单击并创建一个名为 `MeetingDialogWrapper.kt` 的新 Kotlin 文件。这将是实现 `commonMain` 中定义的 `expect` 的 Android 版本。添加：

```kotlin
import androidx.compose.runtime.Composable
import androidx.compose.ui.window.Dialog

@Composable
actual fun MeetingDialogWrapper(onDismiss: onDismissType, content:
    @Composable () -> Unit) {
    Dialog(
    onDismissRequest = onDismiss) {
    content()
    }
}
```

这会创建一个接受关闭回调函数和对话框内容的函数。右键单击 `desktopMain/kotlin/com/raywenderlich/compose/ui` 并创建相同的 `MeetingDialogWrapper.kt` 类。添加：

```kotlin
import androidx.compose.runtime.Composable
import androidx.compose.ui.unit.Dp
import androidx.compose.ui.unit.DpSize
import androidx.compose.ui.window.Dialog
import androidx.compose.ui.window.rememberDialogState

@Composable
actual fun MeetingDialogWrapper(onDismiss: onDismissType, content:
    @Composable () -> Unit) {
    Dialog(
    onCloseRequest = { onDismiss() }, title = "Meetings",
    state = rememberDialogState(),
    content = {
    content()
    })
}
```

这添加了一个关闭处理器、标题“Meetings”、对话框状态和内容。

要运行新的桌面应用，你需要创建一个新的配置。从

![](img/2f50555a40af4ea8c85f09e577f0c5b9_115_0.png)

运行桌面应用：

![](img/2f50555a40af4ea8c85f09e577f0c5b9_115_1.png)

等等，这是什么？

![](img/2f50555a40af4ea8c85f09e577f0c5b9_115_2.png)

好消息是应用运行了。坏消息是没有任何内容。你知道为什么吗？没错——你从未在 `Main.kt` 中添加任何内容。回到桌面模块中的 `Main.kt`。在 `Surface` 内部，添加：

```kotlin
AppTheme {
    MainView()
}
```

这会显示错误。有什么想法吗？看一看 **desktop/build.gradle.kts** 文件。看起来你需要取消注释 **shared-ui** 项目。你需要停止运行桌面应用才能执行其他 Gradle 任务。点击红色停止按钮，取消注释 **shared-ui** 项目并重新同步 Gradle。

现在，在 `Main.kt` 中添加缺失的导入，然后重新运行应用。

![](img/2f50555a40af4ea8c85f09e577f0c5b9_116_0.png)

图 5.7 - 桌面时区屏幕

![](img/2f50555a40af4ea8c85f09e577f0c5b9_116_1.png)

图 5.8 - 桌面时间段屏幕

> **注意：** 窗口背景可能因你的计算机是否使用深色主题而有所不同。

构建并运行桌面应用。你会看到按钮不再被裁剪：

![](img/2f50555a40af4ea8c85f09e577f0c5b9_118_0.png)

## Windows

你的应用可以有单个窗口或多个窗口。如果只有一个窗口，可以使用 `singleWindowApplication` 而不是 `application`。对于多个窗口，需要为每个窗口调用 `Window` 函数。

在桌面模块中打开 `Main.kt`。在 `fun main()` 之前，添加：

```kotlin
data class WindowInfo(val windowName: String, val windowState: WindowState)
@OptIn(ExperimentalComposeUiApi::class)
```

添加所需的导入。`WindowInfo` 类仅保存窗口名称和窗口状态。

删除 `val windowState = rememberWindowState()`，然后添加：

```kotlin
var initialized by remember { mutableStateOf(false) }
var windowCount by remember { mutableStateOf(1) }
val windowList = remember { SnapshotStateList<WindowInfo>() }
// Add initial window
if (!initialized) {
    windowList.add(WindowInfo("Timezone-${windowCount}",
        rememberWindowState()))
    initialized = true
}
```

添加所需的导入，如 `import androidx.compose.runtime.*`。该代码

