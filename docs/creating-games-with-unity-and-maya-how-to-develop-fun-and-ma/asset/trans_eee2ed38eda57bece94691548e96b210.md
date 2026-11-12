
- **步骤 10：** 将 Audio Reverb Zone 组件添加到 Sound-ReverbZone。在 Hierarchy 中选中 Sound-ReverbZone，选择 Component>Audio>Audio Reverb Zone。Inspector 中将出现一个新组件。在 Scene 视图中，调整 Min Distance 和 Max Distance 球体（蓝色方块可用于调整这些区域的大小），使其大致与图 11.3 匹配。

![图 11.3 调整混响区。](img/0285f88bc840f313779e011725b623a5_349_0.png)

- **步骤 11：** 在 Inspector 中，将 Reverb Preset 改为 Hangar。
- **步骤 12：** 测试。戴上耳机运行游戏，听听当玩家处于 Audio Reverb Zone 内时音频如何变化。根据喜好调整 Min Distance、Max Distance 和 Reverb Presets。
- **步骤 13：** 按需添加更多声音。例如，我在门口入口附近使用机械轰鸣声添加了另一个音源。务必调整音量以及 Min 和 Max 距离，使其恰到好处。调整、测试，再调整。
- **步骤 14：** 整理音源。创建一个新的 GameObject（确保其位于 Transform Position 0,0,0），并将其重命名为 Sounds。将目前创建的所有声音 GameObject 都设为此新 Sounds 的子对象（在 Hierarchy 中，只需将它们拖到 Sounds 上）。

### 为什么？

场景中开始出现大量漂浮的对象。花点时间整理一下，就可以隐藏我们不需要的对象集合。

## 脚步声

到目前为止，我们已经创建了环境声音，这很好，也有助于让场景更具沉浸感。但还有其他声音（例如脚步声）也能帮助让场景栩栩如生。

处理脚步声之类的声音有很多方法。在第三人称游戏中，脚步声的精确时机可能非常重要——我们会希望声音在角色的脚（我们能看到）落地的准确时刻播放

一种预制体，然后可以将其拖到 Hierarchy 中并使用。如果对核心 GameObject 做了任何更改，所有预制体都会更新以反映这一更改。尤其是在 Maya 和 Unity 之间来回切换时，保持预制体连接会有极大帮助，因为当新的 .fbx 导入时，在 Maya 中所做的更新会自动传播到场景中。不过，在本例中，这个场景里只会有一个 First Person Controller，所以丢失这个预制体连接并无大碍；继续断开它即可。

- **步骤 17：** 试试这个快捷方式。在 Project 面板中，将脚步声音频剪辑向上拖动并放到 Sound-Footsteps GameObject 上。这会“自动”向该 GameObject 添加一个 Audio Source 组件。这其实与使用 Component>Audio>Audio Source 方法相同——只是更快。
- **步骤 18：** 确保音频剪辑设置为 Play on Awake 和 Loop。记住，这两个选项都可以在 Sound-Footsteps GameObject 的 Audio Source 组件的 Inspector 中找到。
- **步骤 19：** 运行游戏并调整音量。这会有点奇怪，因为现在运行游戏时，脚步声会一直播放。忽略这个小问题，为声音剪辑调出合适的音量。稍后我们会让声音不再持续播放。

## 编写声音脚本

现在，我们有了走过时听到的声音。我们也有了在玩家穿过场景时一直跟随玩家的声音。现在我们需要花点时间，让这个声音仅在需要时——也就是我们移动时——播放。

这里的流程如下：首先，让 Audio Source 处于非活动状态，这样它就不会播放。然后，我们将构建一个简单的脚本，在玩家移动时激活 Audio Source；更准确地说，是在按下移动角色的按键时激活它。

- **步骤 20：** 停用 Sound-Footsteps 的 Audio Source 组件。方法是：在 Hierarchy 面板中选择 Sound-Footsteps。然后在 Inspector 面板中，取消勾选 Audio Source 组件。务必保持 Play on Awake 和 Loop 仍处于勾选状态。
- **步骤 21：** 创建一个新的 JavaScript。在 Project 面板中，选择 Create>JavaScript。也可以通过 Assets>Create>JavaScript 完成。Project 面板中会出现一个新图标，名为 NewBehaviourScript（Unity 由欧洲人构建，因此元音拼写有点古怪）。注意，它旁边的图标上有一个小小的 JS，表示“JavaScript”。将此脚本重命名为 SoundFootstepsControl。
- **步骤 22：** 打开脚本。在 Project 面板中双击该脚本即可。这会打开另一个应用程序。默认情况下，在 PC 上会是 UniSciTE，在 Mac 上会是 Unitron。你将在那里看到脚本的基本内容（图 11.5）。

![图 11.5 UniSciTE 中显示的脚本基本内容。](img/0285f88bc840f313779e011725b623a5_352_0.png)

- **步骤 23：** 输入以下文本：

```csharp
function Update () {
    if (Input.GetButton("Vertical") ||
        Input.GetButton("Horizontal")) {
        audio.enabled = true;
    } else {
        audio.enabled = false;
    }
}
```

### 提示与技巧

注意那个奇怪的 || 符号。它是表示“或”的脚本符号，通常在美国键盘上通过按 Shift-\（Backspace 键正下方的按键）输入。另请注意，以“if (Input.GetButton)”开头的那一行是一整行，直到“||”才结束。

### 为什么？

好吧，我知道我说过我们不会深入探讨这里发生的事情，但它值得快速看一下。

“function Update”只是表示“检查每一帧”。因此，脚本告诉 Unity 每一帧都检查“是否”玩家正在按 Vertical 或 Horizontal 按钮。如果按了，它就把音频组件设置为启用（audio.enabled=true），这意味着音频正在播放。如果玩家没有按这两个按钮中的任何一个（else），它就把音频组件设置为未启用（audio.enabled=false），从而关闭声音。

Vertical 和 Horizontal 是 Unity 的 Input 部分（Edit>Project Settings>Input）中已经定义的两个输入。现在不用太担心这一点，不过 Horizontal 是横向移动的 A 和 D 键，Vertical 是 W 和 S 键。因此，当按下 W、A、S 或 D 时，音频剪辑就会启用，声音就会播放。

- **步骤 24：** 保存脚本（File>Save）。返回 Unity 时，打开 Console（Window>Console），Unity 会指向错误所在的行号。返回去修正。

![](img/0285f88bc840f313779e011725b623a5_354_0.png)

## Unity 简介

### 脚本基础与图形用户界面

在本章中，我们将开始让这个游戏真正成为一款游戏！现在我们已经导入了游戏关卡和游戏角色，并用灯光和声音填充了这些关卡，是时候开始让事物具有交互性了。

游戏的力量正是从这里开始显现；没有脚本部分，游戏只是漂亮的图片，或者充其量是可漫游的模型。虽然这两者都有市场，但与引人入胜的游戏市场相比，它们都相形见绌。

虽然强大的图形元素通常是沉浸式游戏体验的重要组成部分，但它们并不是让游戏有趣的主要驱动力。图形性能孱弱的 Wii 就是一个完美例证：图形表现弱，但有趣的玩法推动了大幅增长和高额利润。现在，随着 PS3 Move 系统和 Xbox 的 Kinect 的出现，我们或许会看到 Wii 控制范式与强大图形相结合；这注定会是电子游戏演进中令人兴奋的时期。但我离题了……

另外，脚本也可以附加到空的 GameObject 上，这些 GameObject 除了承载脚本之外没有其他功能。因此，举例来说，可以在场景中创建一个名为 Script Holder 的空 GameObject，然后将场景中生效的所有脚本（或其中大部分）附加到该对象上。这有几个好处；例如，如果其他人接手了这个项目，他们就知道该去哪里了解游戏的功能。我的软件开发同事总是使用这类机制；他们擅长阅读代码，而且代码会相互迭代，因此觉得这种方法要快得多。不过，对初学者来说，这可能会很难。要知道某个对象是否受到脚本影响，唯一的方法就是通读脚本；试图从这些“茶叶”中看出端倪可能是一项令人生畏的任务。另一个重要的好处是，这种方法通常可以保持预制体完整。当脚本挂在预制体上时，会破坏它，或者只是使它不再与原始对象关联。通过将脚本放在别处，那些预制体就可以得到维护，这可以让资源更新这件事稍微轻松一些。

对我们来说，在本书中，我们会两种方法都使用一点。实际上，最简单的方法就是直接将脚本放到你想要影响的对象上；但从长远来看，包含脚本的脚本容器确实能带来一些真正的好处。

### 关于这种方法的说明

在这些脚本教程的过程中，我们将通过具体的基于项目的实践来研究概念。有时，这意味着我们在第一遍时不会使用绝对最高效的方法，因为最高效的方法有时更难理解。这意味着有时我们会先创建一个脚本，然后在学到更多后再回头优化我们的方法。

### 脚本工具

以下部分介绍了一些可用于脚本的工具。

### 编辑器

Unity 本身并不编辑脚本。虽然你可以在 Unity 内查看脚本内容，但资源的实际编辑是在其他应用程序中完成的。在 Mac 上，内置编辑器是 Unitron。在 PC 上，内置编辑器是 UniSciTE。还有许多其他编辑器可以使用；实际上，任何基本文本编辑器（例如记事本）都可以用来编辑脚本，因为它们只是基本文本。一些更复杂的脚本编辑器（MonoDevelop、Unity Script Editor 或 UnityDevelop）内置了一些非常优雅而强大的功能来辅助脚本编写。

UniSciTE 和 Unitron 都“理解”Unity 的 JavaScript，因此会为正在编写的脚本提供一些视觉提示。这通常包括诸如对识别出的术语进行颜色编码这样简单的提示，也可以包括编辑器在尝试猜测你的意思时给出的建议选项。在这些
