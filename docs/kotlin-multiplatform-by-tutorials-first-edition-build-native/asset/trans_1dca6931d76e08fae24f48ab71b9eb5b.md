
你可以安全地删除 _iosAppUITestsLaunchTests.swift_。打开 **iosAppUITests.swift** 并删除类的所有内容。你将在这里编写几个测试函数。

首先，在测试类中将应用实例作为属性存储。

```
private let app = XCUIApplication()
```

其次，重写 `setUp` 函数。系统会在运行每个测试前调用该方法。它类似于在 Kotlin 中使用 `annotation` `@BeforeTest` 标记测试函数。

```
override func setUp() {
    continueAfterFailure = false
    app.launch()
}
```

此函数在出现错误时阻止测试继续运行，然后启动应用，以便你可以运行测试。

接下来，编写一个测试函数来检查 **About** 按钮是否存在。

```
func testAboutButtonExistence() {
    XCTAssert(app.buttons["About"].exists)
}
```

Xcode 测试框架中的断言函数通常以 `XCTAssert` 开头。这是最简单的用法，需要一个布尔参数。查询应用中的所有按钮，并查找标题为 **About** 的按钮。

> **注意**：Xcode 测试函数必须以 `test...` 开头，否则 Xcode 无法识别它们为测试函数，也就不会运行它们。

## Android UI Testing with Jetpack Compose

对 Compose 布局的测试与基于 View 的 UI 测试不同。基于 View 的 UI 工具包定义了 View 的属性，例如它占据的矩形区域、属性等。在 Compose 中，某些 composable 可能会向层级结构中发出 UI。因此，你需要一种新的匹配 UI 元素的机制。

幸运的是，Jetpack Compose 的创建者预见了这一点，并提供了必要的工具来测试布局。

打开 androidApp 模块中的 build.gradle.kts，在 dependencies 块中添加以下内容：

```
androidTestImplementation(
    "androidx.compose.ui:ui-test-junit4:${rootProject.extra["composeVersion"]}")
debugImplementation(
    "androidx.compose.ui:ui-test-junit4:${rootProject.extra["composeVersion"]}")
```

在 `android` 块的 `defaultConfig` 部分，添加以下内容以指示系统如何运行测试：

```
testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
```

现在同步项目。接下来，创建包和文件。在 src 目录下，创建这些嵌套文件夹：

androidTest/java/com/raywenderlich/organize/android/

你将复制主目录的相同包结构。

接下来，创建一个名为 AppUITest.kt 的 Kotlin 文件，并定义一个同名的类：

```
class AppUITest {
    @get:Rule
    val composeTestRule = createAndroidComposeRule<MainActivity>()
}
```

添加一个类型为 `AndroidComposeTestRule` 的属性。`createAndroidComposeRule` 为你提供的活动创建测试规则。它会启动该活动，以便你可以运行测试。

你要编写的第一个测试是检查 **About** 按钮是否存在。如你记得，该按钮位于应用的右上角，并带有一个 i 图标。你可以通过一种称为 Semantics 的机制来匹配该元素。Semantics 为 UI 提供意义——无论是简单的按钮还是一组 composables。Semantics 框架主要用于无障碍设置，但测试可以利用其关于 UI 层级的信息。

你通过 Modifier 向 composables 添加 semantics。

打开 RemindersView.kt，在 Toolbar composable 的 IconButton 上添加 semantics 修饰符。IconButton 将：

1. 使用你定义的 semantics 查找 **About** 按钮，并模拟点击操作。
2. 检查屏幕上是否有包含 **About Device** 内容的文本。About 页面标题为 **About Device**，只有在该页面显示时才会出现。这种做法并不理想，因为如果你为应用本地化，测试会失败。使用 semantics 始终是更好的选择。
3. 如果你为按钮设置了 content description（如工具栏中的 **Up Button**），你可以直接使用它而无需设置和查询 semantics。你可以查找按钮并执行点击操作。
4. 关闭 **About** 页面后，应用应回到 **Reminders** 页面。检查页面标题以确认情况。

运行测试，它将通过。

## Desktop UI Testing

由于 Android 和 Desktop 的 UI 代码本质上相同，测试也会非常相似。但设置略有不同。 starter project 已经为你提供了相应的代码。需要考虑的差异包括：

- 测试依赖不同。此外，使用 JUnit 测试 Desktop Compose 布局的库处于实验阶段，你需要选择加入才能使用它。查看 **desktopApp** 模块中的 **build.gradle.kts**。

```
named("jvmTest") {
    dependencies {
        @OptIn(org.jetbrains.compose.ExperimentalComposeLibrary::class)
        implementation(compose.uiTestJUnit4)
        implementation(compose.desktop.currentOs)
    }
}
```

- 许多断言函数尚未实现。例如，assertIsDisplayed() 在 Desktop 上没有实现。你可以改用 assertExists()。

- 由于 Desktop 上没有 Activity 来托管你的测试，你需要自己搭建基础。打开 desktopApp 模块中的 AppUITest.kt。主要有两个区别：首先，你需要使用更通用的 createComposeRule() 来创建测试规则；其次，有一个 setUp 方法在所有测试之前运行。这里，你将发射一个类似于应用的 composable 供测试使用。主要区别在于不存在窗口。

```
@Before
fun setUp() {
    composeTestRule.setContent {
    var screenState by remember { mutableStateOf(Screen.Reminders) }
    }

    when (screenState) {
    Screen.Reminders ->
    RemindersView(
    onAboutButtonClick = { screenState = Screen.AboutDevice }
    )
    Screen.AboutDevice -> AboutView()
    }
}
```

- 由于没有窗口，第二个测试函数的实现如下：

```
@Test
fun testOpeningAboutPage() {
    //1
    composeTestRule
    .onNodeWithText("Reminders")
    .assertExists()

    //2
    composeTestRule
    .onNodeWithContentDescription("aboutButton")
    .performClick()

    //3
    composeTestRule.waitForIdle()
}
```

