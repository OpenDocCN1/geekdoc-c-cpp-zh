
`playerName + ". Exception: " + exception.Message`;

```
return new List<PlayerTimeEntry>();
```

```
}
}
```

```c
public void SaveTime(decimal time)
{
    // 3
    var times = LoadPreviousTimes();
    // 4
    var newTime = new PlayerTimeEntry();
    newTime.entryDate = DateTime.Now;
    newTime.time = time;
    // 5
    var bFormatter = new BinaryFormatter();
    var filePath = Application.persistentDataPath +
        "/" + playerName + "_times.dat";
    using (var file = File.Open(filePath, FileMode.Create)) {
        times.Add(newTime);
        bFormatter.Serialize(file, times);
    }
}
```

# 第 14 章：保存数据

这是大量的新代码！本质上，这些代码处理时间与二进制格式化文件之间的保存和加载。

- 1. 使用 `try...catch` 语句尝试加载保存的时间条目。你通过组合玩家名称（存储在 `PlayerPrefs` 中）和 `Application.persistentDataPath` 来构建文件路径。`using` 语句打开文件的文件流，以便使用二进制格式化器对象读取任何现有条目。你使用 `Deserialize()` 方法通过传递已打开的文件流来解包——一下——文件中的数据。如果读取成功，它将返回玩家条目列表。
- 2. 如果反序列化失败，`catch` 语句会找到错误。在这里，你记录了一条信息消息并向调用者返回一个空列表。这很重要，因为玩家可能还没有记录或保存过时间，例如第一次玩时。
- 3. 在保存时间时，你先通过 `LoadPreviousTimes()` 方法获取现有的条目。
- 4. 你创建了一个 `PlayerTimeEntry` 对象的实例。然后，你将传递给方法的当前日期用于 `entryDate` 和 `time` 属性字段。
- 5. 你创建了一个二进制格式化器对象来执行神奇的序列化——又称为打包——将玩家时间条目列表写入文件。你通过组合玩家名称和 `Application.persistentDataPath` 创建文件路径。同样，`using` 语句打开文件。但这次它使用了 `FileMode.Create` 选项，这允许你在相同路径创建新文件或覆盖现有文件。最后，在将新的时间条目添加到现有列表中。

> 注意：上述代码中的 `using` 语句是 C# 中的特殊语句，可以用于处理实现了 `IDisposable` 接口的对象。框架提供的大多数文件和 IO 相关操作都支持此。

如果支持，将这些操作封装在 `using` 语句中是一个好习惯。一旦 `using` 语句内部的操作完成，任何创建的对象都会被销毁。

在上面的情况下，由于你正在打开并写入文件，当 `using` 语句完成时，你会正确关闭文件访问。因此，在之后写入文件时，你不应该遇到文件锁定问题。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_390_0.png)

# Unity 游戏教程

既然你已经添加了用于保存和加载运行时数据的结构，现在你需要一种方法在游戏中显示之前的成绩时间。

回到 Unity 并打开 Game 场景。在主 Canvas GameObject 上创建一个新的 Text GameObject。将其命名为 PreviousTimes。

如下所示设置你的 UI 文本组件的锚点（anchor）和位置：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_391_0.png)

在 Text 组件中，将 `Font` 设置为 orbitron-medium，`Font Size` 设置为 16，`Line Spacing` 设置为 1.2 并设置为右对齐。使用 `Best Fit`，`Max Size` 为 16，并将 `Color` 设置为纯白色，你也可以清空“New”文本值。

保存场景。返回 GameManager.cs，在类的底部添加以下内容：

```csharp
public void DisplayPreviousTimes() {
  // 1
  var times = LoadPreviousTimes();
  var topThree = times.OrderBy(time => time.time).Take(3);
  // 2
  var timesLabel = GameObject.Find("PreviousTimes").GetComponent<Text>();
  // 3
  timesLabel.text = "BEST TIMES \n";
  foreach (var time in topThree) {
    timesLabel.text += time.entryDate.ToShortDateString() + ": " + time.time + "\n";
  }
}
```

这段代码将在新创建的 PreviousTimes UI Text 组件中填充时间记录。以下是详细说明：

- 1. 使用 `LoadPreviousTimes()` 方法收集现有时间。`times.OrderBy(time => time.time).Take(3)` 是一个 LINQ 查询，它按时间从快到慢排序，然后取前三个。
- 2. 找到 PreviousTimes 文本组件。
- 3. 将其更改以显示找到的每个时间，使用字符串 `"\n"` 使用换行符分隔条目。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_391_1.png)

## 第 14 章：保存数据

注意：LINQ 代表 Language Integrated Query（集成语言查询）。它是一种查询语言，允许你轻松地查询和操作数据。有很多实用的查询表达式，通常你可以将它们链在一起。有关 LINQ 的更多信息请参阅：https://en.wikipedia.org/wiki/Language_Integrated_Query

二进制序列化的最后拼图是在玩家到达目标时保存关卡运行时时间——那碗热腾的面条。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_392_0.png)

打开 Timer.cs 脚本并添加以下变量声明：

```csharp
public decimal time;
```

将 `Update()` 中的代码修改为：

```csharp
time = System.Math.Round((decimal) Time.timeSinceLevelLoad, 2);
timerText.text = time.ToString();
```

通过在更新计时器 Text 值之前将时间存储在新变量中，你让其他能够访问该时间值。

打开 Goal.cs 脚本。在 `OnCollisionEnter2D()` 方法底部，检查 Player 标签的 `if` 语句内部，添加以下内容：

```csharp
// 1
var timer = FindObjectOfType<Timer>();
// 2
GameManager.instance.SaveTime(timer.time);
```

这保存了玩家到达目标时的时间。

- 1. `FindObjectOfType` 在关卡场景中找到计时组件实例。这里指定了泛型 `Timer`。此 Unity 方法找到类型为 `Timer` 的脚本第一个实例。由于每个关卡只有一个用于跟踪关卡时间的 Timer 脚本，因此返回了该实例。
- 2. 你创建的新的 `SaveTime` 方法位于 GameManager 单例上，将来自 Timer 脚本的当前关卡运行时传入。

最后，你需要一个触发器来显示关卡的任何之前的运行时。在 GameManager.cs 中，在 GameManager 类底部添加以下内容：

```csharp
private void OnSceneLoaded(Scene scene, LoadSceneMode loadsceneMode) {
  if (scene.name == "Game") {
    DisplayPreviousTimes();
  }
}
```

代码检查场景是否为 Game，如果是，则显示之前的成绩。接下来，在 `Start()` 方法中添加此内容：

- `SceneManager.sceneLoaded += OnSceneLoaded;`

该行将 `OnSceneLoaded()` 挂钩到 Unity SceneManager 的 `sceneLoaded` 事件，该事件在场景加载时触发。`OnSceneLoaded()` 检查场景名称。当结果为 Game 场景时，调用 `DisplayPreviousTimes()`。

保存更改并运行游戏。

玩到关卡结束。现在当你跳进那碗面（即目标精灵）时，你将触发保存方法。

当关卡重启时，三个最快的时间将会显示，因为游戏调用了 `DisplayPreviousTimes()`，读取保存的时间文件并将结果馈入 PreviousTimes 文本组件。如果你还没有玩过三次，那么还需要额外尝试几次三个时间才会出现。成功！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_393_0.png)

# Unity JSON 序列化用法

Unity 的 JSON 序列化提供了一种保存和加载数据的简单方法。这是一个代表关卡的 JSON 示例：

```json
{
  "levelName": "buzzsaw",
  "cameraSettings": {
    "position": [0, 0, -10],
    "rotation": [0, 0, 0]
  },
  "levelItems": [
    {
      "type": "hazard",
      "position": [5, 0, 0],
      "rotation": [0, 0, 0]
    },
    {
      "type": "platform",
      "position": [-2, 2, 0],
      "rotation": [0, 0, 0]
    }
  ]
}
```

现在 Unity 可以在 Inspector（检器）面板中选取并显示 LevelName。保存脚本并查看 Inspector 中的 Level 以确认它已存在。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_397_0.png)

你肯定想要编辑器中有一个 Save（保存）按钮，用于将场景中的关卡保存为 JSON 文件。将以下代码添加到 `OnInspectorGUI()` 方法中：

```
if (GUILayout.Button("Save level"))
{
}
```

这添加了一个自定义的、点击的 GUI 按钮。保存脚本，然后确认你在 Level GameObject 中看到了它。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_397_1.png)

太棒了！你正在取得进展，但如果现在点击它不会发生任何事情。你很快就会处理这个问题。

# 定义关卡的 JSON 对象的层级结构

为了序列化和反序列化自定义关卡数据，你需要将 Unity 类及其关联数据映射到 JSON 结构中。你将创建三个新脚本，将数据映射到关将作为关卡文件的 JSON 层级结构中的不同部分。

在 Scripts 文件夹中创建三个新脚本，并命名为 LevelDataRepresentation.cs、ItemRepresentation.cs 和 CameraSettingsRepresentation.cs。按照所示所示对每个脚本进行修改。

LevelDataRepresentation:

```
using UnityEngine;
using System;
[Serializable]
public class LevelDataRepresentation
{
    public Vector2 playerStartPosition;
    public CameraSettingsRepresentation cameraSettings;
    public LevelItemRepresentation[] levelItems;
}
```

# LevelItemRepresentation.cs:

```cs
using UnityEngine;
using System;
[Serializable]
public class LevelItemRepresentation{
    public Vector3 rotation;
    public Vector3 scale;
    public Vector2 position;
    public string prefabName;
    public int spriteOrder;
    public string spriteLayer;
    public Color spriteColor;
}
```

# CameraSettingsRepresentation.cs:

```cs
[Serializable]
public class CameraSettingsRepresentation{
    public string cameraTrackTarget;
    public float trackingSpeed;
    public float cameraZDepth;
    public float minX;
    public float minY;
    public float maxX;
    public float maxY;
}
```

每个脚本允许 Unity JSONUtility 类序列化和反序列化描述关卡的信息。

保存你的工作。

这是一张实用的图，显示了每个类（又称脚本）如何映射到 JSON 数据。这包含了保存关卡的一个小部分：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_398_0.png)

# 为游戏组件构建并嵌套数据类

每个关卡文件都使用一个基础 LevelDataRepresentation 对象在 JSON 中存储以下项目：

- playerStartPosition: Super Soy Boy 生成的位置。
- cameraSettings: 一个包含如何配置平滑跟随摄像机信息的对象，包括跟随速度和边界。
- levelItems: 关卡项目数组。对于关卡场景中根关卡 GameObject 下创建的每个对象，此数组中的项都描述了该项目是什么、它的位置、旋转角度、精灵图颜色等。

默认情况下，Unity 的 Json 无法序列化相机设置或关卡对象，因为它们不是简单类型。因此，它们被表示为主 LevelDataRepresentation.cs 类中的嵌套字段。

相反，这些对象由具有简单类型字段的类表示。Unity 的 JSONUtility 将能够理解它们！

例如，查看 LevelDataRepresentation.cs 类。LevelItemRepresentation.cs 类的实例表示存储在 levelItems 数组中的每个项。该脚本具有这些简单类型字段：

```
public Vector3 rotation;
public Vector3 scale;
public Vector2 position;
public string prefabName;
public int spriteOrder;
public string spriteLayer;
public Color spriteColor;
```

这种 `[Serializable]` 类的嵌套正是你让复杂对象能够序列化或反序列化并与 JSON 良好交互的方法。

# 在编辑器中解析关卡并将其保存到磁盘

打开 LevelEditor.cs。在 `using` 大括号上方添加以下代码（`GUILayout.Button("Save level")`）：

```
// 1
Level level = (Level)target;
level.transform.position = Vector3.zero;
level.transform.rotation = Quaternion.identity;
// 2
var levelRoot = GameObject.Find("Level");
// 3
```
var ldr = new LevelDataRepresentation();
var levelItems = new List<LevelItemRepresentation>();
```

以下是该代码块的说明：

- 1. 获取 Level 组件的句柄，并将 Level GameObject 的位置和旋转设置为 0，确保所有内容都从场景中的原点定位。
- 2. 将 LevelRoot 建立为 Level GameObject 的引用，它是关卡项目的父级。
- 3. 创建 LevelDataRepresentation 和 LevelItemRepresentation 的新实例。

在最后部分代码的 `List<LevelItemRepresentation>();` 下添加以下内容：
