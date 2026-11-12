
如果比如说你的 Activity 标题是动态的，但在 Activity 启动后不会改变，那么这个方法就是你想深入视图层级并设置标题的地方。这个方法不适合配置那些可能在应用处于后台时、或另一个 Activity 启动到其上方时发生变化的数据。

进一步说，如果你的应用在后台运行，而系统资源不足，你的应用可能会被终止。如果发生这种情况，当应用回到前台时，系统会在同一个 Activity 的新实例上调用 onCreate 方法。

onCreate 方法也是你为 Activity 调用 setContentView 的唯一机会。正如你之前所见，这就是你告诉系统希望此屏幕使用哪种布局的方式。一旦可以开始设置 UI 数据，就调用 setContentView。这些数据可以是从设置列表内容到设置 TextView 或 ImageView 内容的任何内容。

```java
public void onStart()
```

启动时，你的 onStart 方法会在 onCreate 之后立即被调用。如果你的应用被放入后台（原因可能是另一个应用启动到了你的应用之上，或用户按下了 Home 键），那么在你恢复时、Activity 能够与屏幕交互之前，onStart 会被调用。除非应用即将开始使用屏幕时我有某些特定内容需要检查，否则我倾向于避免重写 onStart。

```java
public void onResume()
```

onResume 是 Activity 生命周期中，Activity 获准访问屏幕时调用的最后一个方法。如果 Activity 处于后台期间 UI 元素发生了变化，那么这个方法就是确保 UI 与手机状态同步的地方。

当 Activity 启动时，此方法会在 onCreate 和 onStart 之后调用。当 Activity 再次回到前台时，无论它之前处于什么状态，都会调用 onResume。

## 太棒了，你的 Activity 现在运行起来了！

经过所有这些设置、配置和工作之后，你的 Activity 现在对用户可见了。各种东西被点击，数据可能被解析并显示，列表被滚动，事情正在发生！然而，派对总有结束的时候（也许是因为用户按下了 Back 键），而你需要收尾。

### onPause()

onPause 是应用离开屏幕时系统调用的第一个方法。如果你有任何进程或循环（例如动画）只应在 Activity 位于屏幕上时运行，那么 onPause 方法就是停止它们的理想位置。如果你在当前显示的 Activity 之上启动了另一个 Activity，那么你的 Activity 会收到 onPause 调用。

请记住，如果系统需要资源，你的进程可能在 onPause 方法被调用后的任何时间被终止。这不是正常情况，但你需要意识到它可能发生。

onPause 方法很重要，因为它可能是你得到的唯一警告：你的 Activity（甚至整个应用栈）即将消失。你应当在此方法中将任何重要信息保存到磁盘、数据库或偏好设置中。

一旦 Activity 真正离开屏幕，你就会收到 Activity 生命周期中的下一个调用。

### onStop()

当 Android 调用你的 onStop 方法时，它表示你的 Activity 已正式离开屏幕。此外，当用户离开你的 Activity 去与另一个 Activity 交互时，也会调用 onStop。这不一定意味着你的 Activity 正在关闭（尽管也可能如此）。你只能假定用户已离开你的 Activity 去了另一个 Activity。如果你在 Activity 内执行任何只应在它处于活动状态时运行的持续进程，那么此方法就是你尽一个好公民的职责、将其关闭的机会。

### onDestroy()

onDestroy 是你在消亡之前的最后一次方法调用。这是你的 Activity 在走向天空中的伟大垃圾回收器之前清理自身事务的最后机会。

你的 Activity 可能一直在后台运行的任何后台进程（例如获取/解析数据）都必须在此方法调用中关闭。

然而，仅仅因为 onDestroy 被调用，并不意味着你的 Activity 会被彻底销毁。因此，如果你有一个正在运行的线程，即使在 onDestroy 方法被调用之后，它也可能继续运行并占用系统资源。

## 附加环节——数据保留方法

如前所述，如果系统需要资源，你的进程可能在 onPause 之后的任何时间被终止。然而，用户永远不应知道这种淘汰已经发生。为了实现这一点，Android 给了你两次保存状态数据以供以后使用的机会。

### onSaveInstanceState(Bundle outState)

此方法会向你传递一个 Bundle 对象，你可以将以后需要用来把 Activity 恢复到当前状态的任何数据放入其中。你可以通过调用 outState.putString 或 outState.putBoolean 之类的方法来完成。每个存储的值在存入时都需要一个字符串键，取出时也需要相同的字符串键。你需要负责重写自己的 onSaveInstanceState 方法。如果你声明了它，系统就会调用它；否则，你就错过了机会。

当你之前被终止的 Activity 被恢复时，系统会再次调用你的 onCreate 方法，并把用 onSaveInstanceState 构建的 Bundle 交还给你。

只有当系统认为你之后可能需要恢复 Activity 时，才会调用 onSaveInstanceState。例如，如果用户按下了 Back 键，它就不会被调用，因为设备显然不需要稍后恢复这个确切的 Activity。因此，此方法不是保存用户数据的地方。只应暂存对此屏幕特定实例的 UI 很重要的临时信息。

### onRetainNonConfigurationInstance()

当用户在竖屏和横屏模式之间切换时，你的 Activity 会被销毁，并创建一个新实例（经历完整的方法调用关闭—启动周期）。当 Activity 因配置变更（最常见的是设备旋转）而被销毁并重新创建时，onRetainNonConfigurationInstance 让你有机会返回任意对象，以便在新的 Activity 实例中通过调用 getLastNonConfigurationInstance 重新获取该对象。

这种策略有助于加快屏幕旋转的过渡。如果你的 Activity 需要花费大量时间获取它计划显示到屏幕上的数据，请记住这一点。相反，你可以使用 getLastNonConfigurationInstance 获取之前显示的数据。

### 保持简单，聪明点

到现在，你已经知道 Activity 可能在几乎没有通知的情况下被终止。onSaveInstanceState 给了你保存基本类型数据以供以后使用的机会。这明确意味着，你的整个 Activity 必须能够将其所有重要信息压缩成一系列基本类型数据。这进一步强化了一个观念：Activity 必须非常简单，并且*不能*包含任何对自身之外的应用很重要的复杂数据。避免在 Activity 中保留装满数据的大型 Java 集合，因为它可能会在几乎没有通知的情况下被终止。

现在你应该基本了解：

- 创建新 Activity 的步骤
- Activity 是如何启动的
- Activity 的生命周期

你已经具备跟上后续章节中更复杂主题所需的知识。别担心，我很快就会回到 Activity 这个话题。

Intent 是一个类。在 Android 平台中，Intent 构成了在应用组件之间传递信息的主要通信协议。在设计良好的 Android 应用中，组件（Activity、内容提供器或服务）永远不应直接访问任何其他组件的实例。因此，Intent 就是这些部分能够通信的方式。

这本书相当大的一部分都可以专门用来讲解 Intent 类的创建、使用和细节。为了简洁并让你尽快上手，本章只介绍一些基础知识。在本书其余部分请留意 Intent。它们可能是整个 Android 中最常用的类。

有两种主要方式告诉 Android 系统，你希望接收由系统、其他应用甚至你自己的应用发出的 Intent：

- 在 `AndroidManifest.xml` 文件中注册 `<intent-filter>`
- 在运行时向系统注册 `IntentFilter` 对象

无论哪种情况，你都需要告诉 Android 系统你想监听哪些事件。

发送 Intent 的方式也多得数不胜数。你可以将它们广播给整个系统，也可以将它们定向到特定的 Activity 或服务。然而，为了启动一个服务或 Activity，它必须在清单文件中注册（你在前面关于启动新 Activity 的演示中已经看到了一个示例）。

让我们看看在实践中如何使用 Intent。

### 清单注册

为什么不在运行时注册所有内容呢？如果某个 Intent 已作为清单的一部分声明，系统会启动你的组件，以便它能够接收该 Intent。运行时注册的前提是你的应用已经在运行。因此，任何时候你希望应用因某个事件而被唤醒并采取行动，都要在清单中声明它。如果某些内容只应在应用运行时接收，那么在你的特定组件启动后，注册一个 IntentFilter（在 XML 中声明时写作 intent-filter，在 Java 代码中则是 IntentFilter）。
