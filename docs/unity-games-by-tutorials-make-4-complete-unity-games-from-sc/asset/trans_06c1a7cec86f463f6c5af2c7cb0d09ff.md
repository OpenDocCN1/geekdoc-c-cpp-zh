

```cs
piece.transform.position = li.position;
piece.transform.rotation = Quaternion.Euler(
  li.rotation.x, li.rotation.y, li.rotation.z);
piece.transform.localScale = li.scale;
```

以下是你编写的内容：

- 1. 读取所选关卡的 JSON 文件内容 —— `selectedLevel` 是玩家点击相应按钮后关卡所在的路径。`JsonUtility` 是一个将 JSON 内容反序列化为 `LevelDataRepresentation` 实例的类。它还设置了所有嵌套字段，因此该对象包含了反序列化的所有关卡层级结构。
- 2. 将 `levelData.levelItems` 转换为填充完全的 `LevelItemRepresentation` 实例数组。
- 3. 对于遍历数组的每一个项，脚本根据 `prefName` 值定位正确的制体，并从 `Resources/Prefabs` 文件夹中加载它。
- 4. 实例化该制体的克隆体。当制体带有精灵（sprite）时，将根据该项 JSON 文件中的精灵数据进行配置。
- 5. 创建 Level GameObject 对象，然后根据关卡文件中的数据设置其位置、旋转和缩放。

在 `foreach` 循环的底部有 `piece.transform.localScale = li.scale;`。添加以下代码，每个代码块都需要一个对应的右大括号：

```cs
var SoyBoy = GameObject.Find("SoyBoy");
SoyBoy.transform.position = levelData.playerStartPosition;
Camera.main.transform.position = new Vector3(
SoyBoy.transform.position.x, SoyBoy.transform.position.y,
Camera.main.transform.position.z);
```

场景层级（Hierarchy）中始终有一个 `SoyBoy` GameObject。然而，当它加载时，Super SoyBoy 可能处于不同的起始位置 —— 这可能会是一个真实问题。

这段代码定位 SoyBoy 并将其放置在 JSON 文件中保存的 `playerStartPosition` 位置。接下来，它将相机定位到与 SoyBoy 对齐，这样关卡加载时视图正对准那块小豆腐。

现在，你只需要一些代码来根据关卡的设计和保存方式设置相机的平滑跟随（Smooth Follow）脚本设置。

在你最后添加的设置相机位置的代码下方添加以下代码：

```cs
// 1
var cameraSettings = FindOfType<CameraLerpToTransform>();
// 2
if (cameraSettings != null) {
    cameraSettings.cameraDepth = levelData.cameraSettings.cameraDepth;
    cameraSettings.cameraTarget = GameObject.Find(levelData.cameraSettings.cameraTarget).transform;
    cameraSettings.maxX = levelData.cameraSettings.maxX;
    cameraSettings.maxY = levelData.cameraSettings.maxY;
    cameraSettings.minX = levelData.cameraSettings.minX;
    cameraSettings.minY = levelData.cameraSettings.minY;
    cameraSettings.trackingSpeed = levelData.cameraSettings.trackingSpeed;
}
```

- 1. 使用 `FindObject()` 方法定位平滑跟随脚本 `LerpToTransform`。
- 2. 检查是否找到了平滑跟随脚本，如果是，则根据 JSON 文件中的值填充速度、边界和跟踪目标的设置。

现在，你需要在 Game 场景加载时调用 `LoadLevelContent()`。

将 `GameManager.cs` 中现有的 `OnSceneLoaded()` 方法替换为以下内容：

```cs
private void OnSceneLoaded(Scene scene,
    LoadSceneMode loadsceneMode)
{
    if (!string.IsNullOrEmpty(selectedLevel))
    && scene.name == "Game") {
        Debug.Log("Loading level content for: " + selectedLevel);
        LoadLevelContent();
        DisplayPreviousTimes();
    }
    if (scene.name == "Menu") {
        DiscoverLevels();
    }
}
```

这段代码在加载包含 `GameManager.cs` 单例的场景时运行。通过检查场景名称是否为 "Game" 并确保 `selectedLevel` 已赋值，你确保了接下来的代码只有在 Game 场景加载且 `selectedLevel` 值被设置后才会运行。

最后，最后一行代码在调用 `DiscoverLevels()` 之前检查场景是否已设置为 "Menu"。此检查确保了脚本确实发现了所有的关卡文件，并知道有多少不同的按钮准备好加载相关的关卡路径。

保存 `GameManager.cs` 并从 Menu 场景运行游戏。

从 Menu 关卡选择器中选择一个保存为 JSON 的自定义设计关卡。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_410_0.png)

关卡从文件加载并完全重构。

恭喜！你现在拥有了一个功能完整的关卡加载器，具备设计和保存自定义关卡的能力，并在菜单的关卡选择器滚动面板中显示它们。

# 收尾工作

还有一些事情需要处理。还记得你之前用二进制序列化实现的那些最佳记录吗？嗯，它们只对一个关卡有效。

无论你创建并玩了多少关卡，所有关卡的最佳时间都是相同的。

目前，保存到二进制文件的最佳时间是与你选择的任何名称以及后缀 `times.dat` 拼接的。

| 名称 | 修改日期 | 类型 | 大小 |
| --- | --- | --- | --- |
| sean_times.dat | 26/08/2016 18:59 | DAT 文件 | 1 KB |

如果将最佳时间与关卡名称绑定，效果会更好。

将最佳时间与关卡名称绑定，效果会更好。

打开 `GameManager.cs`。在 `SaveTime()` 中，用以下内容替换定义 `filePath` 的行：

```cs
var levelName = Path.GetFileName(selectedLevel);
filePath = Application.persistentDataPath + "/" + levelName + "_times.dat";
```

现在，可以随时回到 Menu 场景。你还去除了 JSON 扩展名。然后你用关卡名称创建了 `timesLabel` 内容。

从 Menu 场景再次运行游戏。玩两个不同的关卡几次，注意你的运行用时是针对每个关卡的特定的。

# 太棒了！

如果你再次查看存储的运行时文件，你会发现它们现在按照你预期的命名规则！

| 名称 | 修改日期 | 类型 | 大小 |
| --- | --- | --- | --- |
| John_basic.level.json.times | 12/09/2016 00:28 | DAT 文件 | 1 KB |
| John_my other level.json.times | 12/09/2016 00:30 | DAT 文件 | 1 KB |
| John_times.dat | 11/09/2016 23:20 | DAT 文件 | 1 KB |

好了，这是脚本的最后部分，这非常简单！

玩家应该能够轻松返回 Menu 场景并使用关卡选择界面。

在 `GameManager.cs` 中添加此 `Update()` 方法：

```cs
void Update()
{
    if (Input.GetKeyDown(KeyCode.Escape))
    {
        SceneManager.LoadScene("Menu");
    }
}
```

这段代码检查是否按下 Escape 键，如果是则加载 Menu 场景。

# 接下来？

你在这一章中涵盖了大量内容。这里是一些亮点：

- * 保存数据的三种方法：PlayerPrefs、二进制序列化和 Unity 的 JSON 序列化。
* 使用上述每种方法的时机。
* 保存供玩家查看、滚动和选择的特定文件数据。
* 构建自定义的、可分享的游戏关卡。

你可能也提升了 C# 技能。

