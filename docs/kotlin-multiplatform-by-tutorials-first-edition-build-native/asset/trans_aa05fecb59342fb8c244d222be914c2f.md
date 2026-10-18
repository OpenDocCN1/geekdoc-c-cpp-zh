
## 创建 Common 模块的 Platform 类

打开 **Platform.kt**，在 **commonMain** 文件夹中。将 `expect` 类定义替换为以下内容：

```kotlin
expect class Platform() {
    val osName: String
    val osVersion: String

    val deviceModel: String
    val cpuType: String

    val screen: ScreenInfo?

    fun logSystemInfo()
}

expect class ScreenInfo() {
    val width: Int
    val height: Int
    val density: Int
}
```

通过编写这段代码，你向 KMP 承诺会提供这些信息。如上所示，这里没有任何实现。你只定义需要的内容，就像定义 `interface` 或 `protocol` 一样。

> **注意**：你使用了 Kotlin 的构造函数简写语法 `Platform()`，这意味着 KMP 现在期望你在项目中为构造函数、属性和方法提供实现。

你可能会惊讶于没有把 `Platform` 或 `ScreenInfo` 定义为 `data class`，因为它们看起来像是典型的数据持有类。

原因是 `data class` 在 Kotlin 中会自动生成一些实现。因此，这里不能使用 `data class`，因为 `expect` 类不应该有实现。

你也不能在 `expect class` 内部定义嵌套类。因此，你把 `ScreenInfo` 类放在 `Platform` 定义之外。你也可以新建一个文件。把它们放在同一个文件里同样可行。

在代码行号区，点击带有字母 **A** 的黄色菱形，这将让你跳转到项目中实际实现的平台文件。

# _Kotlin Multiplatform by Tutorials_ _第 6 章：连接平台特定 API_

如果文件尚未放在相应位置，或者你尚未实现实际定义，可以在 **expect** 类名上点击 **Alt+Enter**，Android Studio 会帮助你完成。

# 在 Android 上实现 Platform

打开 **Platform.kt**，位于 **androidMain** 文件夹中。

你会看到 Android Studio 已经在提醒你完成这个承诺。毕竟 KMP 仍在起步阶段，像幼儿一样！

将整个类定义替换为以下代码块：

+   5. 通过 `Build` 的 `SUPPORTED_ABIS` 属性可以获取设备的 CPU 类型。由于在某些旧版本的 Android 中结果可能为 `null`，因此提供默认值。
+   
+   6. 初始化一个 `ScreenInfo` 实例并将其赋值给 `screen` 属性。由于你在期望文件中声明该属性为可空，所以必须显式指定类型，否则类型会是非空的。而且，你在期望文件中承诺该属性可为空，应当遵守承诺。关于其可空的原因在实现桌面部分会说明白。
+   
+   7. 像 `interface` 一样，这里提供函数实现。目前，你将使用 Android 的 `Log` 类把所有属性输出到控制台。确保导入 `android.util.Log`。你可以安全地展开可空的 `screen` 属性，因为你在前面已经用非空值初始化了它。
+   
+   8. 你为 `ScreenInfo` 以及其默认构造函数提供了实际实现。
+   
+   9. 获取屏幕属性时，需要 `DisplayMetrics` 对象。可以使用下面的代码块获取。这里可以有额外的属性或方法。请确保导入 `android.content.res.Resources`。
+   
+   0. 使用之前定义的 `metrics` 属性获取屏幕宽、高和密度。导入 `kotlin.math.round` 以使用 `round` 函数。

接下来，你将实现 iOS 特定的代码。

# 在 iOS 上实现 Platform

当你在实际文件中时，可以点击带有字母 **E** 的黄色菱形，跳转到期望定义。在 **Platform.kt**（androidMain 文件夹中）内，点击黄色图标返回到 **common** 目录中的文件。从那里，点击 **A** 图标跳转到 iOS **actual** 文件。

你要添加的代码基本与之前相同，但这次会调用 iOS 框架，如 `UIKit`、`Foundation` 和 `CoreGraphics` 来获取所需信息。

将实际实现替换为以下代码块：

```kotlin
actual class Platform actual constructor() {
    // ...
}

actual class ScreenInfo actual constructor() {
    //7
    actual val width =
CGRectGetWidth(UIScreen.mainScreen.nativeBounds).toInt()
    actual val height =
CGRectGetHeight(UIScreen.mainScreen.nativeBounds).toInt()
    actual val density = UIScreen.mainScreen.scale.toInt()
}
```

+   1. `UIKit` 中有一个名为 `UIDevice` 的类，你可以通过它查询当前设备的信息。这里，你询问界面 idiom 以区分 iOS 与 iPadOS。`UIUserInterfaceIdiom` 枚举还有其他情况，为了简化，你在 else 块中使用 Kotlin/Native `Platform` 类获取信息。
+   2. 你可以使用 `UIDevice` 获取操作系统版本。
+   3. 这可能是本书中最笨拙的代码块。但别担心：KMP 通常不会如此复杂，它只是展示事情可能有多糟糕。Objective‑C 的核心是 C。有些老旧 API 可以追溯到 1990 年代。由于它们低层且使用频率不高，Apple 从未为它们提供更友好的接口。其中一个是 C 结构体 `utsname`。Unix 爱好者，欢呼吧！这里，你通过 Kotlin/Native 调用 C 函数。有多疯狂！在下面的代码块中，你使用 `memScoped` 块和 `alloc()` 函数分配内存，然后把指针传给 `uname` 函数，它填充操作系统信息。随后，你把包含机器名称的 C 字符串转换为 `NSString`，再自动转换为 Kotlin `String`。完成了！ sigh
+   4. 获取 CPU 类型时，你可以再次查询 C 代码，或者如这里，直接使用 Kotlin/Native `Platform` 类。
+   
+   5. 你初始化了一个 `ScreenInfo` 实例并将其赋值给 `screen` 属性。和 Android 实现一样，请显式写出类型。
+   
+   6. 函数实现：`MODULES/Platform/Platform.cpp`
