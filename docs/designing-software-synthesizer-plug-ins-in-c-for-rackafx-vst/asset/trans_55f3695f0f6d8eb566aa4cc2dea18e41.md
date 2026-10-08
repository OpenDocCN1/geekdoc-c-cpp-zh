

```objc
NSView *returnView = uiFreshLoadedView;
// 清空指针。这是一个工厂方法。

// 一旦视图被创建
// 并交接后，工厂就不再保留它的记录。
uiFreshLoadedView = nil;
return [returnView autorelease];

@end
```

CocoaSynth.plist 文件包含正确的信息。它被用于识别工厂的属性，这些属性与我们重写的 `GetProperty` 方法相关，用以通知程序我们支持 Cocoa GUI。请检查 `CocoaSynth.plist` 文件并确保字段已正确设置；**粗体**的字段随不同的合成器而异，而其他字段保持不变。其中一个来自 MiniSynth：

-- CFBundleExecutable CocoaFilterView
- CFBundleIdentifier developer.audiunit.yourname.MiniSynth
- CFBundlePackageType BNDL
- NSMainNibFile CocoaView
- NSPrivateClass MiniSynthViewFactory

该字段至关重要——这是你使用工厂的地方。如果它与你在 `GetProperty` 方法中暴露的工厂不匹配，你的 GUI 将不会显示或导致宿主机崩溃。

## 2.45 事件监听器

该对象更为复杂，但主要是因为我们的合成器有许多控制控件（大部分为  0–40 个左右），并且我们需要符合一种事件回调方案。我们需要为每个控制组准备 `IBOutlets`。接下来，我们需要 `IBActions` 作为动作处理程序。与其为每个控制控件编写单独的句处理器，我们只需实现两个：分别用于旋钮（knob）和选项菜单控件。我们还设置了控件使其存储参数的索引。通过这种方式，我们可以让处理程序变得非常短。

我们还需要某种方式与我们的“伙伴”音频插件（Audio Plug-in）进行通信。通信需要是双向的——当用户移动控件时，我们需要通知插件；当用户使用预设或更改插件状态时，我们需要相应地更新我们的控件。这些通过事件监听器回调方案（Event Listener Callback scheme）来实现。

要建立事件监听系统，你需要实现一些方法并调用一些 AU 函数。首先，我们需要实现一个供宿主机查询的方法，以确定我们想要支持什么种类型的事件。事件包括：

- 参数更改：用户移动控件并更改参数
- 手势：这些包括鼠标点击和移动
- 属性更改：属性如混响尾迹时间或你对 Cocoa GUI 的支持发生了变化

对于我们的合成器，我们只关心参数更改，因此我们使用常量设置事件类型并调用 `AUEventListenerAddEventType` 来注册它。

```objc
void addParamEventListener(AUEventListenerRef listener,
    void* refCon, AudioUnitEvent *inevent)
```

```objc
// 将事件类型设置为 kAudioUnitEvent_ParameterValueChange
inevent->mEventType = kAudioUnitEvent_ParameterValueChange;
```

```objc
// 注册它
verify_noerr(AUEventListenerAddEventType(listener, refCon,
inevent));
```

下一步是创建 `AUEventListener` 向它传递一个选择器（selector），指向你实现的回调函数。然后你告诉 `AUEventListener` 关于你所有的参数，它会为每个参数设置一个私有的监听器（Listener）。你还定义了一个私有的监听器函数，通过告诉控件更新其位置来响应。事件监听器回调命名为 `AUEventListenerDispatcher`，但你可以随心命名。查看创建 `AUEventListener` 的函数调用：

你需要理解的两个参数是：第一个命名回调方法，第二个是指向 `self` 的指针。该指针将以 `void*` 的伪装传递给回调函数，这是回调函数中的标准技巧，因为该函数是独立的，位于任何其他对象定义之外。如果这对你来说新鲜，请访问网站获取更多关于回调的信息。回调函数声明在 `View.cpp` 文件的顶部，对象实现之外：

```objc
verify_noerr(AUEventListenerCreate(AUEventListenerDispatcher,
self,
CFRunLoopGetCurrent(),
CFRunLoopDefaultMode,
```

