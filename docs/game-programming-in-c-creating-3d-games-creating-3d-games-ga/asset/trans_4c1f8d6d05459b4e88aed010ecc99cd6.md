
void OnUpdateWorldTransform() override;

SoundEvent PlayEvent(const std::string& name);

void StopAllEvents();

private:

std::vector<SoundEvent> mEvents2D;

std::vector<SoundEvent> mEvents3D;

};

AudioComponent::PlayEvent 函数首先在 AudioSystem 上调用 PlayEvent。然后检查事件是否为 3D，以确定应将 SoundEvent 存储在哪个向量中。最后，如果事件是 3D，则在其上调用 Set3DAttributes：

单击此处查看代码图片

```
SoundEvent AudioComponent::PlayEvent(const std::string& name)
{
    SoundEvent e = mOwner->GetGame()->GetAudioSystem();

    // Is this 2D or 3D?
    if (e.Is3D())
    {
        mEvents3D.emplace_back(e);

        // Set initial 3D attributes
        e.Set3DAttributes(mOwner->GetWorldTransform());
    }
    else
    {
        mEvents2D.emplace_back(e);
    }

    return e;
}
```

`AudioComponent::Update` 函数（此处省略）会移除 `mEvents2D` 或 `mEvents3D` 中不再有效的任何事件。（`IsValid` 返回 `false`。）

接下来，添加 `OnUpdateWorldTransform` 的重写。请回顾，每次拥有者角色计算其世界变换矩阵时，都会通过调用此函数来通知每个组件。对于 `AudioComponent`，它需要在世界变换发生变化时，每次更新 `mEvents3D` 中任何 3D 事件的 3D 属性：

**单击此处查看代码图片**

```
void AudioComponent::OnUpdateWorldTransform()
{
    Matrix4 world = mOwner->GetWorldTransform();
    for (auto& event : mEvents3D)
    {
        if (event.IsValid())
        {
            event.Set3DAttributes(world);
        }
    }
}
```

最后，`AudioComponent::StopAllEvents`（同样在此处省略）只需对两个向量中的每个事件调用 stop，并清空向量。`AudioComponent` 的析构函数会调用此函数，但游戏可能存在其他希望仅为角色停止声音事件的情况。

有了这些添加，你可以将 `AudioComponent` 附加到角色并在音频组件上播放声音事件。`AudioComponent` 随后会根据需要自动更新关联事件的 3D 属性。

## 第三人称游戏中的监听者

直接使用摄像机位置和方向的监听者适用于第一人称游戏，因为摄像机是从玩家角色的视角出发的。然而，对于摄像机跟随玩家角色的第三人称游戏，情况并不那么简单。图 7.2 展示了第三人称游戏的侧视图。玩家角色位于位置 P，摄像机位于位置 C。位置 A 表示紧邻玩家角色的音效。位置 B 表示靠近摄像机的音效。

![](img/e9afcec1487716b0ef80d7e7c09869c8_527_0.png)

### 图 7.2 第三人称游戏中的音效

现在假设监听者使用摄像机位置和方向，如上述代码所示。在这种情况下，声音 A 和 B 都会听起来位于前方。这很好，因为两个音效都在屏幕上可见，所以作为玩家，你应该感知到声音位于前方。然而，声音 B 会比声音 A 听起来更近。这似乎很奇怪，因为你期望紧邻玩家的声音更响亮。即使没有声音 B，任何紧邻（甚至位于）玩家的声音始终会应用一定的衰减，这可能会让声音设计师感到沮丧。

如果监听者改用玩家位置和方向，那么声音 A 会比声音 B 响亮。然而，声音 B 听起来会像是在后面，因为它位于玩家后面。这非常奇怪，因为声音在屏幕上，所以你期望它听起来位于前方。

你实际上想要的是基于玩家位置的衰减，但基于摄像机的方向。Guy Somberg 描述了一个解决此问题的绝佳方案（他的书列在章节末尾的“附加阅读”部分），这只需要一点向量数学。给定位于位置 P 的玩家、位于位置 C 的摄像机和位于位置 S 的声音，首先计算两个向量——一个是从摄像机到声音的向量，另一个是从玩家到声音的向量：

```
PlayerToSound = S - P
CameraToSound = S - C
```

PlayerToSound 向量的长度是衰减所需的距离。归一化的 CameraToSound 向量是正确的朝向。将归一化的 CameraToSound 向量与 PlayerToSound 的长度进行标量乘法，可得到声音的虚拟位置：

```
VirtualPos = ||PlayerToSound|| \frac{CameraToSound}{||CameraToSound||}
```

```
VirtualPos = ||PlayerToSound|| \frac{CameraToSound}{||CameraToSound||}
```

这个虚拟位置（如图 7.3 所示）既能提供正确的衰减，*也*能提供正确的声音方向。监听者本身随后直接使用摄像机，与之前一样。

![](img/e9afcec1487716b0ef80d7e7c09869c8_529_0.png)

### 图 7.3 带有虚拟位置的第三人称游戏音效

请注意，如果其他计算（如本章后面讨论的遮挡）需要声音的真实世界位置，则此方法可能不可行。

## 多普勒效应

想象你站在街角。当警车接近时，警笛声的音调会升高。相反，警车驶过后，声音的音调会降低。这就是多普勒效应，如图 7.4 所示。

![](img/e9afcec1487716b0ef80d7e7c09869c8_530_0.png)

### 图 7.4 多普勒效应

**多普勒效应**（或多普勒偏移）发生是因为声波在空气中传播需要时间。当警车越来越近时，每个声波起始位置更近，这意味着声波到达时更加密集。这会导致感知到的频率增加，从而使音调升高。当警车正好位于监听者旁边时，可以听到声音的真实音调。最后，当警车驶离时，会发生相反的效果：声波到达时间隔更远，从而导致音调降低。多普勒效应适用于所有类型的波，但声波是最容易观察到的。

在游戏中，多普勒效应可以为车辆等物体创建更逼真的声音。FMOD 可以自动计算多普勒音调偏移；只需在 `setListenerAttributes` 和 `set3DAttributes` 中传入正确的速度即可。这意味着游戏可能需要更基于物理的运动方法，使用力，如第 3 章“向量与基础物理”中简要讨论的那样。

还可以通过低级 API 访问一些额外的多普勒参数。set3DSettings 函数设置这些参数：

单击此处查看代码图片

```
mLowLevelSystem->set3DSettings(
    1.0f, // Doppler scale, 1 = normal, higher exagg
    50.0f, // How many game units = 1 meter (our game
    1.0f // (Not for Doppler, leave at 1)
);
```

## 混音与效果

数字化声音的一个优势是播放期间的操作很容易。你已经在播放过程中操纵声音，以考虑声音相对于监听者的位置。数字信号处理（DSP）一词是指对信号进行计算操作。对于音频，调整信号的音量或音调是一种 DSP 类型。

游戏中另外两种常见的 DSP 效果是混响和均衡。混响模拟声音在封闭区域内反弹。例如，在洞穴内部的音效会产生回声，因为声波在墙壁上反弹。**均衡**，另一方面，试图将声音的音量水平归一化到一组范围内。

FMOD Studio 允许配置 DSP 效果链。换句话说，声音可以在输出前通过多个修改信号的阶段。虽然每个声音事件可以有自己的 DSP 链，但更常见的方法是将声音分组为类型。然后，不同的组可以应用不同的效果。

## 总线

在 FMOD Studio 中，**总线**是声音的分组。例如，你可能有一个用于音效的总线、一个用于音乐的总线和一个用于对话的总线。每个总线可以单独附加不同的 DSP 效果，并且在运行时可以调整总线。例如，许多游戏为不同类别的声音提供单独的音量滑块。使用总线可以轻松实现这一点。

默认情况下，每个项目都有一个由根路径 `bus:/` 指定的主总线。但是，声音设计师可以添加任意数量的其他总线。因此，就像在银行加载时加载事件描述一样，你可以同时加载总线。首先，向 `AudioSystem` 添加一个总线映射：

单击此处查看代码图片

```
std::unordered_map<std::string, FMOD::Studio::Bus*> r
```
