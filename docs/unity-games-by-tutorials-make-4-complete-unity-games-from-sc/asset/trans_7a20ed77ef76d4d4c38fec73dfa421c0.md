

# Unity 教程游戏

这通过生成点的数量，限制了你可以生成的外星数量。

请添加以下代码：

```csharp
aliensPerSpawn = (aliensPerSpawn > totalAliens) ?
aliensPerSpawn = totalAliens : aliensPerSpawn;
```

这是另一段预防性代码。如果 `aliensPerRow` 超过了最大值，则生成数量将会减少。这意味着生成事件创建的外星人数量永远不会超过你配置的最大值。

现在是编写实际的生成代码。请添加以下代码：

```csharp
for (int i = 0; i < aliensPerSpawn; i++)
{
}
```

此循环会为每个生成的外星进行迭代。在花括号之间添加以下代码：

```csharp
if (aliensOnScreen < maxAliensOnScreen)
{
    aliensOnScreen += 1;
}
```

这段代码检查 `aliensOnScreen` 是否小于最大值，然后会增加屏幕上的总数。

在 `aliensOnScreen += 1` 之后，添加以下代码：

```csharp
// 1
int spawnPoint = -1;
// 2
while (spawnPoint == -1)
{
    // 3
    int randomNumber = Random.Range(0, spawnPoints.Length - 1);
    // 4
    if (!previousSpawnLocations.Contains(randomNumber))
    {
        previousSpawnLocations.Add(randomNumber);
        spawnPoint = randomNumber;
    }
}
```

这段代码负责寻找一个生成点。

- 1. `spawnPoint` 是生成的生成点索引。因为它引用了一个索引，所以将其设置为 -1，表示尚未选择生成点。
- 2. 这个循环会一直运行，直到找到一个生成点或者生成点不再是 -1。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_132_0.png)

3. 这一行产生一个随机数作为可能的生成点。

4. 接下来，它会检查 `previousSpawnLocations` 数组，查看该随机数是否为活跃的生成点。如果没有匹配，说明你找到了生成点。该数字被添加到数组中并设置 `spawnPoint`，从而打破循环。如果找到匹配，循环将使用新的随机数继续迭代。

现在你已经有了生成点索引，你需要获取实际的 `SpawnGameObject`。再坚持几步！你就要解锁一项成就了。

在 `while` 语句的结束花括号之后添加以下代码：

```csharp
GameObject spawnLocation = spawnPoints[spawnPoint];
```

由于 Inspector（检查器）中已经分配了生成点，这会根据你在上段代码中生成的索引获取该生成点。

现在，生成实际的外星人。添加以下代码：

```csharp
GameObject newAlien = Instantiate(alien) as GameObject;
```

`Instantiate()` 会创建你传递给它的制品的实例。它会创建一个类型为 `object` 的对象，你必须强制转换为 `GameObject`。现在添加以下代码：

```csharp
newAlien.transform.position = spawnLocation.transform.position;
```

这会将外星人置于生成点。保存你的代码并切换回 Unity。

选择 GameManager 并进入 Inspector。将 `Max Aliens on Screen`（屏幕上外星最大数量）设置为 10，`Total Aliens`（总外星数量）设置为 10，`Min Spawn Time`（最小生成时间）设置为 0，`Max Spawn Time`（最大生成时间）设置为 3，以及 `Aliens Per Spawn`（每次生成数量）设置为 1。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_133_0.png)

运行你的游戏并观察 Scene（场景）视图。太棒了！看看那些诡异的生物。成就已解锁！

# Unity 教程游戏

# 第 5 章：管理器与路径规划

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_134_0.png)

- Alien
- Alien(Clone)
- Directional Light
- SpaceMarine
- SpawnPoints
- Spawn
- Spawn
- Spawn
- Spawn
- Spawn
- Spawn
- Alien
- Alien(Clone)
- Alien(Clone)
- Alien(Clone)
- Alien(Clone)
- Alien(Clone)
- Alien(Clone)
- Alien(Clone)
| Max on Play | Mute audio | Gizmos |
| --- | --- | --- |

# Unity 中的路径规划

外星人已经到达，但它们不仅仅是装饰。它们需要移动起来！这看起来像是一项简单的任务，对吧？你可以为外星人设置一个目标，每帧让它们朝目标移动。问题解决！

当然，这没那么简单。首先，你必须不断让外星人面向太空士兵。其次，当外星人撞到柱子时，会发生真实的问题。外星人会一直向柱子走，直到某些情况导致它们改变方向。当一个柱子挡住整个移动时，这很荒唐。年前你可以这样做，但现代玩家期望更好的体验。那么该怎么办？你的第一个直觉可能是编写路径规划代码。例如，你可以编写代码让外星人在离开柱子后朝太空士兵移动。这行不通，但你正在处理一个边缘情况。如果添加另一个地板会发生什么？你必须应用类似的修复，否则你的代码会变成一团乱码。幸好，有一个更好的方法。

# Unity 的导航系统

事实证明 Unity 提供了开箱即用的路径规划解决方案。它的导航系统由四个对象组成：

- 1. Mesh：代表可行走区域。这适用于平坦和三维地形，如楼梯。
- 2. Agent：使用 Mesh 的代理。你给它一个目标，它将通过 NavMesh 找到路径。
- 3. Mesh Link：地图上的快捷，例如角色可以跨越的间隙。
- 4. Obstacle：代理应该避开的障碍物。代理将使用路径规划绕过它们。

为了追逐太空士兵，你首先需要在整个地板上覆盖 NavMesh 并将其标记为可行走区域。点击 Window\Navigation。Unity 将显示导航窗口（默认出现在 Inspector 右侧面板）。注意这些标签页：

- Agents：定义不同的代理尺寸。
- Areas：定义区域掩码，类似于物理层。
- Bake：配置 NavMesh 的属性。
- Object：列出你添加到 NavMesh 的 GameObject。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_135_0.png)

# Unity 教程游戏

选择 Object 标签页，并在其中选择 Renderers 图标为 Hierarchy 应用过滤器。现在，它只会显示带有渲染器的 GameObject。你可以在搜索字段中看到它：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_136_0.png)

你可以通过其他类型过滤 Hierarchy。要移除过滤器，只需点击清除按钮（不要点错）。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_136_1.png)

在 PC 上按 Control 或在 Mac 上按 Command 并选择 Floor_Piece、Floor_Piece_001、Floor_Piece_002、Floor_Piece_003、Glass_Floor。

导航窗口会出现一些选项。勾选 Navigation Static 告诉选定的网格不要移动。不要勾选 Generate Mesh Links，否则选定的 GameObject 之间会产生链接。最后，你会看到 Navigation 选项——这是你正在构建的导航网格。现在你正在处理 Walkable 掩码，也可以切换到 Not Walkable（不可行走）或 Jump（跳跃）。当你在 Areas 标签页创建掩码时，你的自定义掩码也会出现在这个下拉列表中。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_136_2.png)

点击 Bake 标签页，然后点击视图底部的 Bake 按钮。这保存了网格。

# Unity 教程游戏

# 第 5 章：管理器与路径规划

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_137_0.png)

现在你有了盟行走的地方！点击 Bake 按钮后，竞技场将变成浅蓝色。这表示你获得了一个可行走的 NavMesh。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_137_1.png)

如果你看不到蓝色的导航网格，请检查 Scene 视图中的 Show NavMesh 复选框。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_137_2.png)

如果你选择了不同的导航区域，如 Jump，那么颜色将会是橙色。

# Unity 教程游戏

点击 Areas 查看所有可用的区域和颜色：

| Agents | Areas | Bake | Object | Name Cost |
| --- | --- | --- | --- | --- |
| Built-in 0 | Walkable | | | 1 |
| Built-in 1 | Not Walkable | | | 1 |
| Built-in 2 | Jump | | | 2 |
| User 3 | | | | 1 |
| User 4 | | | | 1 |
| User 5 | | | | 1 |
| User 6 | | | | 1 |
| User 7 | | | | 1 |

切换导航窗口时，这些漂亮的颜色会“消失”，稍后我们会学习 Bake 标签页。

