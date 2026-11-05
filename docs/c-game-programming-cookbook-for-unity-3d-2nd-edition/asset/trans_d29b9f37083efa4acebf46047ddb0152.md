
```
public int FindNearestWaypoint(Vector3 fromPos,
Transform exceptThis, float maxRange)
{
    if (_transforms == null)
        GetTransforms();

    // the 'current' distance variable is just used to hold
    // we are comparing, so that we can find the
    closest
    distance = Mathf.Infinity;
    int tempIndex = 0;

    // Iterate through them and find the closest
    one
    for (int i = 0; i < totalTransforms; i++)
    {
        // grab a reference to a transform
        Transform _tempTR =
        (Transform)_transforms[i];

        // calculate the distance between the
        current transform and the passed in transform's position vector
        diff = (_tempTR.position - fromPos);
        curDistance = diff.sqrMagnitude;

        // now compare distances - making
        sure that we are not
        if (curDistance < distance &&
        _tempTR != exceptThis)
        {
            if (Mathf.Abs(_tempTR.
            position.y - fromPos.y) < maxRange)
            {
                // set our current
                'winner' (closest transform) to the transform we just found
                _closest = _tempTR;
                // store the index of
                this waypoint
                tempIndex = i;
                // set our "winning"
                distance to the distance we just found
                distance = curDistance;
            }
        }
    }

    // now we make sure that we did actually find
    something, then return it
    if (_closest)
    {
        // return the waypoint we found in
        this test
        return tempIndex;
    }
    else
    {
        // no waypoint was found, so return
        -1 (this should be accounted for at the other end!)
        return -1;
    }
}
```

`GetWaypoint()` 返回通过整数 `index` 传入的索引所对应的路径点的变换。

```
public Transform GetWaypoint(int index)
{
    if( shouldReverse )
    {
```

这是该类中唯一使用 `shouldReverse` 的地方。当 `shouldReverse` 为 true 时，`GetWaypoint` 会反转路径点的索引编号（即，使用 `GetWaypoint` 获取索引编号为零的路径点将返回路径中的最后一个路径点，而不是第一个）。

要反转传入此函数的索引，可以通过用 `totalTransforms` 中的变换总数减去变量 `index` 来修改它。

```
// send back the reverse index'd waypoint
index = (totalTransforms - 1) - index;

if(index<0)
    index=0;
```

显然，在尝试访问路径点变换并将其作为返回值发送出去之前，重要的是要确保它们已经设置好；因此，需要快速检查以确保 `Transforms` 不为 null。如果 `Transforms` 为 null，我们就知道没有可用的变换，因此会调用 `GetTransforms()` 来完成所有设置：

```
// make sure that we have populated the transforms list, if not, populate it
if(_transforms==null)
    GetTransforms();
```

如果请求的索引过高，则不会返回错误的路径点，而是返回 null 值。请求端的代码随后可以检查 null 返回值并采取相应操作：

```
if(index>totalTransforms - 1)
    return null;
```

现在一切都已正确设置，变换列表包含路径点且索引编号在范围内，剩下要做的就是返回数组中的变换：

```
return (Transform)_transforms[index];
}
```

路径点控制器脚本中的最后一部分是 `GetTotal()`，其他脚本使用它来了解有多少个路径点：

```
public int GetTotal()
{
    return totalTransforms;
}
```

## 9 配方
声音与音频

在本章中，我们将了解音频混音器，构建一个充当基础声音管理器（BaseSoundManager）的脚本，并讨论如何为框架的武器系统添加音频。

### 9.1 音频混音器与在 Unity 中混音音频

音频平衡是让游戏音效听起来专业的重要部分。要让声音的音量达到良好的平衡可能很困难，例如使你在音乐之下仍能听到所有重要的声音，或者使激光的声音不会比爆炸声还大，等等。Unity 提供了一套出色的工具包，用于平衡音频以及一些效果，以帮助获得你的作品所需的那种音景。

Unity 的音频混音器允许你将声音组织成组，然后管理这些组，而不是处理单个声音。例如，你可能有一个音乐组、一个常规音效组，也许还有第三个环境背景音频组。Unity 为你提供了一个基本的混音台，你可以在游戏过程中实时调整每个组的音量，以正确平衡它们。使用音频混音器的另一个优势是你可以使用效果。

为项目创建音频混音器后，你可以使用音频混音器窗口（Window > Audio > Audio Mixer）查看正在发生的情况并调整滑块（图 9.1）。

### 9.1.1 混音音频

要在 Unity 中访问音频混音器，请使用菜单 Window/Audio/Audio Mixer。混音器在左侧显示混音器、快照、组和视图的列表。窗口的主要部分将显示当前所选混音器内各组的滑块。

![](img/e4b578cd512539e7261e070d87b6550a_164_0.png)

图 9.1 音频混音器窗口允许你更改不同音频组之间的平衡。

### 9.1.2 公开混音器属性以通过脚本修改它们

如果你想更改音频混音器的属性，例如其音频电平，你需要公开这些属性，以便可以通过脚本访问它们。为此，请通过菜单 Window/Audio/Audio Mixer 打开音频混音器。在左侧选择要编辑的混音器，然后选择要公开其属性的组。在 Inspector 中，右键单击要公开的字段名称。例如，在图 9.2 中，我们选择了音效组 Attenuation 下的 Volume 属性。应出现一个菜单，顶部选项是将属性公开给脚本。从菜单中选择此选项。该属性现在

![](img/e4b578cd512539e7261e070d87b6550a_164_1.png)

图 9.2 Inspector 显示当前所选音频混音器的属性。你可以单击字段将其公开给代码。

将公开给脚本，但它会有一个默认名称——MyExposedParam——这并不是最具描述性的名称。要重命名公开的属性，请查看音频混音器面板，并在其右上角找到 Exposed Parameters 按钮（图 9.3）——单击 Exposed Parameters，Unity 应会显示所选混音器的任何公开参数。要重命名，请右键单击要重命名的属性，然后从菜单中选择 Rename。

![](img/e4b578cd512539e7261e070d87b6550a_165_0.png)

图 9.3 Exposed Parameters 菜单显示公开的参数，并允许你重命名它们或从脚本中取消公开它们。

如果你以后想取消公开某个参数，请单击 Exposed Parameters，然后右键单击要取消公开的参数。从菜单中选择 Unexpose。

### 9.1.3 音频效果

Unity 提供各种音频效果；你可以将其添加到音频混音器中，使声音更有趣或帮助动态平衡它们。要添加效果，首先通过菜单 Window/Audio/Audio Mixer 打开音频混音器。选择要添加效果的组。在音频混音器面板中，每个音频面板底部都有一个 Add 按钮。单击 Add 显示效果菜单。此时，让我提请注意 Duck Volume 效果。Duck Volume 将从另一个音频组接收输入，并降低其所附加组的音量。你可能已经在商业电子游戏和电视节目的对话中听到过这种效果的实际应用，因为它最常用于在播放对话时降低音乐音量。为实现这一点，你需要将音乐和对话通过两个音频组传送。你的音乐组将附加 Duck Volume 效果。你的对话组将附加 Send 效果。在选中对话组的 Inspector 中，Send 效果有一个名为 Receive 的字段，可让你选择哪个组应接收音频电平。将其设置为音乐通道意味着 Duck Volume 效果可以获取该组的电平并相应地压低音乐音量。将音频闪避与通知声音一起使用也可以使突出重要声音的过程更加容易。

### 9.2 BaseSoundManager 类

在本节中，我们构建一个名为 BaseSoundManager 的基础声音管理类。其规范为：

- 必须能够从单个类管理多个音频剪辑
- 能够从 3D 空间中的设定位置播放音频剪辑
