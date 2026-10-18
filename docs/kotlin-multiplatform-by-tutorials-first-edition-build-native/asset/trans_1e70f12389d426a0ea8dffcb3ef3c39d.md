
Android Studio 的 Kotlin Multiplatform Mobile 模板只生成 Android 和 iOS 目标，因此你需要手动添加桌面平台。

在 **shared-action** 模块中，打开 **build.gradle.kts** 文件。在 `kotlin` 部分中，在 `listOf` iOS 目标之后，添加：

```kotlin
jvm("desktop")
```

现在，转到 `sourceSets`，并在底部添加 `desktopMain` 变量：

```kotlin
val desktopMain by getting
```

同步项目并等待此操作完成。

你仍然需要在 **shared-action** 模块中添加 **desktopMain** 文件夹。一个简单的实现方法是右键点击 **src**，然后选择 **新建 ▸ 目录**。你会看到一个带有几个文件夹建议的新窗口。搜索“desktop”并选择 **desktopMain/kotlin**。

现在你只缺包结构。你可以通过右键点击 **desktopMain/kotlin** 轻松创建此目录。这一次，选择 **新建 ▸ 软件包**。在这个新窗口中，输入：**com.raywenderlich.learn.action**。你还可以移除 Android Studio 在 **androidMain**、**commonMain** 和 **iosMain** 文件夹中生成的 **Platform.kt** 和 **Greeting.kt** 文件。就是这样！你的项目结构将如下所示：

[PAGE 313]

![](img/2f50555a40af4ea8c85f09e577f0c5b9_313_0.png)

图 14.1 - 项目结构

根据你在 Android Studio 的 **项目** 选项卡中选择的视图类型，你可能会看到不同的树状结构。要看到相同的结构，请选择顶部的 **项目** 选项。

![](img/2f50555a40af4ea8c85f09e577f0c5b9_313_1.png)

图 14.2 - Android Studio 项目视图

# 配置 Android 库以发布

要发布 Android 库，你需要对 **shared-action** 模块的 **build.gradle.kts** 文件中 `kotlin` 部分里的 `android()` 目标定义进行更新，改为：

[PAGE 314]

```kotlin
android {
    publishLibraryVariants("release", "debug")
}
```

如果你不定义 Android 发布其库，你的项目将默认使用为桌面创建的库。这是可能的，因为 JVM 支持 Android。然而，这样行不通，因为两个平台上的平台特定代码完全不同。

# 配置多平台 Swift 包

你有多种生成库的方式。由于 Apple 有自己的包管理器——Swift Package Manager——并且现在许多库都通过它提供，本章你将使用它。

然而，没有官方插件可以从 KMM 项目生成 Swift Package。因此，你需要使用[多平台 Swift 包](#)插件。在 **starter** 项目中，你有一个包含此库更新版本的 **plugins** 文件夹。打开 **settings.gradle.kts** 文件将其包含到项目中：

```
includeBuild("plugins/multiplatform-swiftpackage-m1_support")
```

> **注意：** 此定制版插件支持 Apple M1 架构，并在内部使用 KMM **XCFramework** 函数来生成 Frameworks。

同步项目。现在，打开 **shared-action** 中的 **build.gradle.kts**，并在 `plugins` 部分添加：

```
id("com.chromaticnoise.multiplatform-swiftpackage-m1-support")
```

你可以定义一些参数来配置你的 Swift 包。为此，在 `kotlin` 部分之前添加：

```kotlin
//1
multiplatformSwiftPackage {
    //2
    xcframeworkName("SharedAction")
    //3
    swiftToolsVersion("5.3")
    //4
    targetPlatforms {
        iOS { v("13") }
```

[PAGE 315]

```kotlin
}
//5
outPutDirectory(File(projectDir, "sharedaction"))
}
```

以下是具体说明：

+   1. 此函数允许你配置生成的 Swift 包。
+   
+   2. 你可以通过设置 `xcframeworkName` 为生成的框架定义特定名称。否则，它将默认使用模块的名称。
+   
+   3. 顾名思义，它对应生成的包所需的 Swift 工具版本。
+   
+   4. `targetPlatforms` 定义框架应支持的平台和操作系统版本。在这种情况下，它将在所有版本为 13 或更高的 iOS 设备和模拟器上工作。
+   
+   5. 默认情况下，**swiftpackage** 是 Swift 包的输出文件夹。你可以通过 `outputDirectory` 参数定义不同的位置和名称。

此插件允许你生成可在 **iosApp** 上使用的 Swift Package Manager Manifest 和 XCFramework。

为了让 Framework 生成为“SharedAction”，你还需要设置 `XCFramework` 名称及其 `baseName`。转到 iOS 目标部分并更新：

```kotlin
val xcf = XCFramework("SharedAction")
listOf(
    iosX64(),
    iosArm64(),
    iosSimulatorArm64()
).forEach {
    it.binaries.framework {
        baseName = "SharedAction"
        xcf.add(this)
    }
}
```

同步项目。打开终端，在项目根文件夹中运行：

```shell
./gradlew shared-action:createSwiftPackage
```

你应该会看到：

[PAGE 316]

查看 **shared-action** 文件夹。你会看到一个新的 **sharedaction** 目录，其中只包含一个文件：**Package.swift**。由于项目不包含任何代码，因此没有生成 **XCFrameworks**。

在 **shared-action/commonMain** 中创建一个 **PlatformAction.kt** 文件，并再次执行 `createSwiftPackage` 命令。执行完毕后，返回 **sharedaction** 文件夹。你现在有了适用于 **arm64** 和 **arm64_x86_‑_64** 模拟器的 **XCFrameworks**。

就是这样！你的模块已准备好生成 Swift 包。

你也可以在 **shared** 模块上进行相同的更新。类似于你在 **shared-action** 上的操作，打开 **shared/build.gradle.kts** 文件并添加 `plugin`：

```
id("com.chromaticnoise.multiplatform-swiftpackage-m1-support")
```

然后是其配置：

```
multiplatformSwiftPackage {
    xcframeworkName("SharedKit")
    swiftToolsVersion("5.3")
    targetPlatforms {
    iOS { v("13") }
}
```

上述命令只允许你为 **shared-action** 模块生成 Swift 包。如果你想为两个共享模块生成，只需不添加库名作为前缀即可：

```
./gradlew createSwiftPackage
```

既然你已经配置好了一切，是时候将代码从应用 UI 移到 Multiplatform 了。由于 **shared-action** 模块将处理打开链接的用户操作，请在你于 **commonMain** 内创建的 **PlatformAction.kt** 中添加：

```
public expect object Action {
```

[PAGE 317]

```kotlin
public fun openLink(url: String)
}
```

这是 UI 将调用的对象。

或者，你可以直接定义 `openLink` 函数，而不将其添加到 `object` 中：

```
public expect fun openLink(url: String)
```

你可以直接从 **androidApp** 和 **desktopApp** 调用此函数，因为你是直接引用它的。然而，从 **iosApp** 访问时，你需要通过以下方式：

```
PlatformActionKt.openLink(url: "\\(item.link)")
```

由于没有定义类，编译器在生成框架时会创建一个类，并使用类名加上文件扩展名作为其名称。虽然你可以定义不同的名称，但总会带有 **kt** 前缀——这不是最讨喜的名称，尤其是当你试图说服 iOS 团队采用用 Kotlin 编写的共享模块时。:-)

Android Studio 会提示自动生成缺失的文件。现在先忽略它。在某些 IDE 版本中，此功能不能按预期工作，最终会在错误的目录中创建文件。为避免任何意外错误，你将手动添加所有这些文件。

为 **androidMain**、**iosMain** 和 **desktopMain** 创建一个 **PlatformAction.kt** 文件。它们应该位于每种平台相同的目录中：**com.raywenderlich.learn.action**。

定义一个空的 `actual` 函数：

```
public actual object Action {

  public actual fun openLink(url: String) {}
}
```

为不同目标实现 `openLink` 函数：

+   - **androidApp**：打开 **MainActivity.kt** 文件，滚动直到看到 `openEntry` 函数。将其内容复制并粘贴到你在 **shared-action/androidMain** 中创建的 `openLink` 函数中：

```
public actual fun openLink(url: String) {
```

