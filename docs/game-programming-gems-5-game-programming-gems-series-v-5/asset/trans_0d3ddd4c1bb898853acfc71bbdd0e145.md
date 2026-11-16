

还有一种方法可以由从 world 类派生的类来实现。

```
virtual bool isValidIndex(const GPIndex& index);
```

该方法默认返回 true；其目的是让我们知道特定的 GPIndex 是否在此 GPWorld 中有效。GP 会自动使用此方法。当 GP 要为给定的 GPIndex 创建 GPtile 时，它会检查该 GPIndex 是否有效，如果索引有效，GPWorld 将通过其方法 BuildFile() 创建 GPtile（如前所述，如图 1.7.10 所示）。如果索引无效，GPWorld 不会创建任何内容，且 GetTile() 方法将返回 false。对 GPIndex 是否落在 GPWorld 内部的验证，加上错误检查，旨在避免随后的错误加载或其他影响。

![](img/672fe9a2d008ba627b1991e15d70f43e_129_0.png)

图 1.7.10 序列图。

一个 world 可以包含 GPtile，这些 GPtile 包含所有必要信息，尽管它们是不同类型的信息（全局概念）；或者，另一方面，GP 中可以存在许多不同的 GPworld，每种数据类型一个，即每个 GP 实例一个（特定概念）。

GP 几乎已经形成，我们只需三个简单步骤：

- 1. 定义 GPIndex。
- 2. 实现 GPtile 的 Load / Unload 方法。
- 3. 实现 GPWorld 的 BuildFile 方法。

## 窗口：在世界中导航

一旦我们拥有 world（GPWorld），并且可以仅通过其位置（GPIndex）获取其中的任何块（GPtile），我们只需知道想要加载和卸载哪些块。为此，GP 提供了 GPwindow。借助它，我们可以使用 GPtile 的 GPIndex 在 GPWorld 中导航，而无需了解其中包含的信息（参见图 1.7.11）。

GPwindow 有三个主要属性：

- CenterIndex：位于 GPwindow 中心的 GPtile 的 GPIndex
- Radius：指示中心 GPtile 周围的 GPtile 数量
- GPTilesList：包含 GPWindow 中的所有 GPtile

![](img/672fe9a2d008ba627b1991e15d70f43e_130_0.png)

图 1.7.11 GPwindow。

GPwindow 的初始化非常简单：

- 1. 为其提供对 GPworld 的引用。
- 2. 给 GPwindow 一个 GPIndex，用于定位它。
- 3. 给它一个 Radius。

之后，GP 会自动填充 GPtileslist，以给定的 GPIndex 为中心，使用该 GPIndex 的 getNextIndex() 和 getPreviousIndex() 方法，并指示 GPWorld 加载整个列表，如图 1.7.12 所示。

![](img/672fe9a2d008ba627b1991e15d70f43e_131_0.png)

图 1.7.12 已加载的 GPwindow。

要导航，我们只需通过其更新方法 Update() 向 GPwindow 提供位置。每次调用此方法时，它都会检查新位置是否在中心 GPtile 内，即是否包含在中心 GPindex 中。如果新位置在中心 GPtile 内，GPwindow 不会自行更新；否则，我们将包含新位置的 GPindex 作为新中心，GPwindow 将随其新中心和半径进行更新。

在更新过程中，tiles list 会被修改，添加 GPwindow 内的新 GPtile，并移除不在其中的 GPtile。GPwindow 指示 GPWorld 加载新的 GPtile，并卸载其列表中删除的 GPtile。此过程是自动的，对用户透明，并且与 tiles 中包含的信息类型完全独立，如图 1.7.13 所示。

如果修改了半径，更新过程相同，但请注意，在这种情况下，中心保持不变。

![](img/672fe9a2d008ba627b1991e15d70f43e_132_0.png)

图 1.7.13 GPwindow 更新过程。

最后，我们已准备好使用 GP。以下是所有步骤：

- 1. 定义 GPindex。
- 2. 实现 GPtile 的 Load() 和 Unload() 方法。
- 3. 实现 GPworld 的 BuildFile 方法。
- 4. 初始化 GPwindow，分配：
  - GPworld
  - 一个中心
  - 一个半径
- 5. 更新 GPwindow 的位置。

## 多窗口，多用户

GP 以自然且透明的方式支持多用户。正确的术语是多窗口，因为每个用户可以拥有多个 GPwindow，并且可以同时存在多个用户（参见图 1.7.14）。GP 将每个 GPwindow 视为不同的用户。当 GPwindow 向 GPWorld 请求加载或卸载 GPtile 时，会执行一些简单的检查：

```
GPtile::Load(): If the GPtile is already loaded, the world does nothing.
```

```
GPtile::Load(): The GPtile is unloaded only if there are not other GPwindows that need it. After unloading the tile, the world destroys the tile.
```

整个过程对用户是透明的，用户只需在必要时负责更新本地拥有的 GPwindow（或 GPwindows）。

![](img/672fe9a2d008ba627b1991e15d70f43e_133_0.png)

图 1.7.14 多窗口，多用户。

## 优化：多线程分页

GP 的一项优化是避免 GPWorld 立即执行 GPtile 的 Load() 和 Unload() 方法的调用。World 将在单独的线程中执行这些任务，以避免加载/卸载过程与系统其余部分发生干扰，从而提高性能。

为此，World 维护一个 GPtile 列表。当 GPwindow 向 GPWorld 请求加载（或卸载）GPtile 时，GPWorld 将此 GPtile 添加到列表，并将其标记为可加载（或可卸载）。在加载/卸载线程的主循环中，列表中的每个元素都会被移除并处理。

## 结论

本文介绍了一个完整的、多用户的通用分页系统（GP），能够以简便高效的方式管理任何类型的信息，并优化系统资源。GP 的范围是全局的，因此可以集成到任何需要管理信息加载和卸载的其他系统中。

GP 的设计遵循了 [Lakos96] 和 [Alexandrescu01] 的一些设计建议。GP 的实现采用了 [Meyers96] 的一些建议。

## 参考文献

- [Alexandrescu01] Alexandrescu, Andrei. Modern C++ Design. Addison Wesley, 2001.
- [Lakos96] Lakos, John. Large-Scale C++ Software Design. Addison Wesley, 1996.
- [Meyers96] Meyers, Scott. More Effective C++. Addison Wesley, 1996.

## 1.8 大规模基于栈的状态机

James Boer

author@boarslair.com

在本文中，我们探讨了传统状态对象与基于栈的管理和排队系统的独特结合。这些结合成了所谓的基于栈的状态机。这种机制远优于传统状态机，尤其是在处理传统上混乱的逻辑流时，例如深度嵌套的用户界面屏幕。基于栈的状态机也使处理其他棘手的状态相关问题变得简单，例如如何在不到处编写特例代码的情况下实现全局状态（如游戏暂停状态），或者在状态中构建内在知识，以便在执行完毕时知道应该返回到哪里。还演示了一个高级状态管理器系统，增加了诸如排队状态命令、延迟状态转换和集中式状态时序功能等功能。状态按预期表示为层次化的 C++ 对象，并设计为在进入和退出时自动处理诸如了解前一个和下一个状态以及堆叠事件（将状态推入或弹出其他状态之上）等细节。这个系统是管理大规模状态系统（例如程序内的全局应用程序状态或游戏状态概念）的一种极其有效的方式。

## 传统状态机代码及相关问题

任何游戏最基本的任务之一是表示内部“状态”，该状态表示当前呈现给用户的可视和逻辑元素。通常，游戏分为两个不同的状态部分：前端用户界面状态和游戏内状态。例如，前端中的每个用户界面屏幕都应被视为唯一状态，因为每个屏幕都有独特的功能以及到其他状态的独特转换。对话框和其他用户必须交互的主要屏幕元素也可能被视为唯一状态，尽管这些元素有将在后面解决的特定问题。

