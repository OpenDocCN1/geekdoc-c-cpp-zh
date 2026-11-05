

上面，变量 `canFire` 在函数 `ResetFire()` 中被重置。该函数由 `Firing()` 函数末尾的 `Invoke` 语句调用，该语句将变量 `fireDelayTime` 作为调用前的延迟传递。这意味着在 `fireDelayTime` 设定的延迟之后，该敌人将被允许再次发射武器。这种暂停的存在是为了避免在敌人可以发射的每一帧都有一连串的弹丸从敌人光束枪中不断射出。这样，我们只会得到间歇性的火力脉冲。

## 11 菜单和用户界面

本章首先对所有示例游戏中使用的主要菜单进行全面分解。主菜单结构应为任何主菜单系统提供完美的起点。

本章的第二部分将介绍游戏内 UI。

### 11.1 CanvasManager 类/画布管理

CanvasManager 是一个专门用于在用户界面画布之间切换的类，例如当你想从主菜单移动到子菜单（如选项菜单）时。它依赖于一个名为 CanvasGroup 的组件，该组件由 Unity 作为引擎的一部分提供。CanvasGroup 让我们可以设置整个 Canvas 的 alpha 透明度级别，同时还提供启用或禁用交互性或启用或禁用 Canvas 对射线投射的阻挡的方法。

CanvasManager 在 `_UICanvasGroups` 中保存了一个 Canvas GameObject 数组，然后你可以使用 `ShowCanvas(index)`、`HideCanvas(index)` 和 `HideAll()` 函数根据需要切换它们。CanvasManager 类也可以处理淡入淡出，如果你在其 `_FadeCanvasGroup` 变量中提供一个 Canvas。例如，你可以拉伸一个简单的 UI Panel GameObject 来填充一个 Canvas，然后让 Canvas 拉伸以填充屏幕。这个 Canvas 构成了你的 `_FadeCanvasGroup`，你可以使用 CanvasManager 的 `FaderOn()`、`FaderOff()`、`FadeIn()` 和 `FadeOut()` 函数让它覆盖游戏视图。

**CanvasManager.cs:**

```csharp
using System.Collections;
using UnityEngine;
namespace GPC
{
    public class CanvasManager : MonoBehaviour
    {
        public CanvasGroup[] _UICanvasGroups;
        public float fadeDuration = 0.25f;
        public float waitBetweenFadeTime = 0.1f;
        [Space]
        public CanvasGroup _FadeCanvasGroup;
        private int currentGroup;
        private int lastGroup;
    }
}
```

CanvasManager 继承自 MonoBehaviour 以使用 Unity 的内置函数。

```csharp
void Awake()
{
    HideAll();
}
```

我们希望 CanvasManager 做到的第一件事就是隐藏存储在 `_UICanvasGroups` 列表中的所有画布，这样我们就不会在 Scene 开始时让所有用户界面画布重叠在一起。

接下来，`HideAll()` 函数循环遍历以隐藏所有画布：

```csharp
public void HideAll()
{
    currentGroup = 0;
    lastGroup = 0;
    for (int i = 0; i < _UICanvasGroups.Length; i++)
    {
        _UICanvasGroups[i].alpha = 0;
        _UICanvasGroups[i].interactable = false;
        _UICanvasGroups[i].blocksRaycasts = false;
    }
}
```

如上所示，我们还将每个 Canvas 的 alpha 设置为 0，同时将 CanvasGroup 的 `interactable` 和 `blocksRaycasts` 属性设置为 false。这样画布不仅会被隐藏，而且也不会干扰场景中的其他 UI。

我们也可以使用 `HideCanvas()` 函数来隐藏单个画布，接下来：

```csharp
public void HideCanvas(int indexNum)
{
    StartCoroutine(FadeCanvasOut(_UICanvasGroups[indexNum], fadeDuration));
}
```

我们画布的淡入淡出在很大程度上依赖于协程。此类中有三个不同的协程：`FadeCanvasOut`、`FadeCanvasIn` 和 `StartFadeCanvasSwitch`。上面，隐藏画布的代码使用 `FadeCanvasOut` 并传入我们希望它影响的 CanvasGroup 组件的引用，后面跟着我们希望它淡入所需的时间（以秒为单位）。

此类还提供了使用 `HideCanvas` 的替代方法。你可以只传入要隐藏的 CanvasGroup 的索引号，或者传入索引号后跟一个布尔值 true 或 false 来表示画布是否应通过淡出效果淡出，或者是否应立即消失。替代的 `HideCanvas` 函数如下所示：

```csharp
public void HideCanvas(int indexNum, bool doFade)
{
    if (doFade)
    {
        StartCoroutine(FadeCanvasOut(_UICanvasGroups[indexNum], fadeDuration));
    }
    else
    {
        _UICanvasGroups[indexNum].alpha = 0;
        _UICanvasGroups[indexNum].interactable = false;
        _UICanvasGroups[indexNum].blocksRaycasts = false;
    }
}
```

上面，如果 `doFade` 为 true，我们使用协程，但如果为 false，则 Canvas 的 alpha、`interactable` 和 `blocksRaycasts` 属性将直接从 `_UICanvasGroups` 数组中保存的引用设置。

现在我们可以在隐藏画布之后显示它们：

```csharp
public void ShowCanvas(int indexNum)
{
    lastGroup = currentGroup;
    currentGroup = indexNum;
    StartCoroutine(FadeCanvasIn(_UICanvasGroups[indexNum], fadeDuration));
}

public void ShowCanvas(int indexNum, bool doFade)
{
    lastGroup = currentGroup;
    currentGroup = indexNum;
    if (doFade)
    {
        StartCoroutine(FadeCanvasIn(_UICanvasGroups[indexNum], fadeDuration));
    }
    else
    {
        _UICanvasGroups[indexNum].alpha = 1;
        _UICanvasGroups[indexNum].interactable = true;
        _UICanvasGroups[indexNum].blocksRaycasts = true;
    }
}
```

再次如上所示，存在两个版本的相同函数——一个只接受 Canvas 的索引，另一个接受索引和一个额外的布尔值来指定淡入淡出模式，与 `HideCanvas()` 的方式相同。

`HideCanvas()` 和 `ShowCanvas()` 之间的唯一区别是，上文我们调用协程 `FadeCanvasIn()` 而不是来自 `HideCanvas()` 函数的 `FadeCanvasOut()`——并且在处理无淡入淡出代码时，alpha 设置为 1 而不是 0。

接下来是 `LastCanvas()`：

```csharp
public void LastCanvas()
{
    TimedSwitchCanvas(currentGroup, lastGroup);
}
```

通常你需要提供一种方法从子菜单返回到主菜单，或返回到上一个屏幕。为了加快具有此行为的菜单的开发过程，我们提供了 `LastCanvas()` 函数，它将当前显示的 Canvas 更改为上一个。它使用变量 `lastGroup` 来跟踪之前打开的内容。由于这只是一个单级系统，如果你需要从多级菜单返回，你需要进一步扩展它或手动设置下一个应显示的菜单。

在 `LastCanvas()` 中，注意它这次没有使用协程，而是使用了一个名为 `TimedSwitchCanvas()` 的函数来协调切换画布的时机。`TimedSwitchCanvas` 接受两个数组索引值——第一个是要隐藏的画布，第二个是要显示的画布。`TimedSwitchCanvas()` 将执行淡出、暂停（由 Inspector 可访问的 `waitBetweenFadeTime` 变量指定），然后淡入新的画布。这意味着要淡出一个 UI 画布并淡入另一个画布，我们可以使用 `TimedSwitchCanvas()` 而无需处理淡入淡出之间的时序。

接下来是 `FadeIn()` 和 `FadeOut()` 函数：

```csharp
public void FadeOut(float timeVal)
{
    StartCoroutine(FadeCanvasIn(_FadeCanvasGroup, timeVal));
}

public void FadeIn(float timeVal)
{
    StartCoroutine(FadeCanvasOut(_FadeCanvasGroup, timeVal));
}
```

`FadeIn()` 和 `FadeOut()` 使用 `FadeCanvasIn` 和 `FadeCanvasOut` 协程来淡入或淡出特定的 Canvas——其引用保存在变量 `_FadeCanvasGroup` 中。如本节前面所述，CanvasManager 提供了使用上述代码轻松淡入或淡出场景的方法。

当场景首次加载时，淡入淡出画布需要覆盖屏幕才能使淡出效果正常工作，因此我们还需要函数根据需要将淡入淡出画布打开或关闭：

```csharp
public void FaderOn()
{
    _FadeCanvasGroup.alpha = 1;
}
```
