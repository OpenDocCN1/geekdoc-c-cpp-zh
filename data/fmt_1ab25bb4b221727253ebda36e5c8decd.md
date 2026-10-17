
这检查玩家左侧或右侧是否有墙、是否不在地面上，以及他们是否正在跳跃。如果是这样，角色的 `Rigidbody` 速度将被设置为一个新的速度，使用当前的 `Y` 速度，但对 `X`（水平）速度进行更改。

墙的反向方向通过调用新的 `GetWallDirection()` 方法并取反其返回的值计算出来（-1 变成 1，1 变成 -1）。

保存你的更改并返回 Unity。在场景编辑器中复制一些单块预制体，并将副本向上堆叠以建造一些墙壁。在场景编辑器中移动它们时，记住按住 `CTRL` 键以保持它们对齐到 1 个单位的大小。

运行游戏，并对着墙跳跃（`Space` 键）。当你落在墙上时，再次跳跃，向另一个方向移动。有了这种技术，你现在可以扩展规模了！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_365_0.png)

# 挂载角色动画

你已经完成了关于输入的角色控制器（Character Controller），现在将完成动画控制器（Animation Controller）。这将允许你扩展角色控制器来控制动画！如果你需要复习 Unity 的动画，请复阅第 6 章“动画”。

点击 `SoyBoy` `GameObject`，然后打开 `Animator` 窗口。在窗口内部点击 `Parameters`（参数）选项卡。

目前没有参数。你接下来将添加这些参数。

在 `Animator` 窗口的 `Parameters` 区域，连续点击 `+`（加号）图标三次，每次添加三个参数之一：

- `Speed`，类型为 `Float`（浮点型），值为 0.0。
- `IsJumping`，类型为 `Bool`（布尔型），未勾选。
- `OnWall`，类型为 `Bool`（布尔型），未勾选。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_366_0.png)

现在创建状态。首先定义一个从默认 `Entry` 状态到 `IdleAnimation` 的状态更改。右键点击 `Entry` 状态，选择 `Make Transition`（制作过渡），然后点击 `IdleAnimation` 块。

会生成一个从 `Entry` 指向 `IdleAnimation` 的箭头。

现在，你需要让 `IdleAnimation` 成为新的默认状态（由橙色块表示）。右键点击 `IdleAnimation` 并点击 `Set as Layer Default`（设置为层默认值）。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_366_1.png)

此过渡不需要任何条件。它将在游戏开始时发生。

现在创建一个从 `IdleAnimation` 到 `RunAnimation` 的过渡，再次创建一个从 `RunAnimation` 回到 `IdleAnimation` 的过渡。你可能想在窗口中拖动状态块以更好地定位它们。

这是你现在应该拥有的：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_367_0.png)

点击从 `IdleAnimation` 指向 `RunAnimation` 的过渡箭头。`Inspector`（检查器）窗口应会显示此过渡的详情。

点击 `Conditions`（条件）下方的 `+`（加号）图标，并在 `Condition` 下拉菜单中选择 `Speed` 参数。确保勾选设置为 `Greater than`（大于） 0。取消勾选 `Has Exit Time`（退出时间）。这确保了一旦满足参数指标，动画就会立即切换状态。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_367_1.png)

点击从 `RunAnimation` 指向 `IdleAnimation` 的过渡箭头。
点击 `Conditions` 下方的 `+`（加号）图标，在 `Condition` 下拉菜单中选择 `Speed` 参数。这次你想要从跑步过渡回空闲，因此将勾选设置为 `Less than`（小于） 0.05。当玩家松开水平移动控制时，速度将降至 0，并满足此条件。

不要忘记取消勾选 `Has Exit Time` 复选框，因为你希望在条件满足时动画尽可能地退出。

完成所有过渡箭头的创建，你需要根据下面的图片设置这些过渡：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_368_0.png)

在你制作的每一个过渡上，确保在该过渡的 `Inspector`（检查器）中取消勾选 `Has Exit Time` 复选框。

每个状态之间都有相互过渡，但 `SlideAnimation` 和 `IdleAnimation` 之间除外，那里只有一个从滑动到空闲的状态更改。

点击 `Animator` 编辑器中的每个过渡箭头，并按照下表指定的创建条件以完成 `Animator Controller`。

| Idle -> Jump | Jump -> Idle | Run -> Jump | Jump -> Run |
|---|---|---|---|
| IsJumping = true | Speed Less 0.05 | IsJumping = true | IsJumping = false |
| Speed Less 0.5 | IsJumping = false | | Speed Greater 0 |
| | IsOnWall = false | | |

| Run -> Slide | Slide -> Run | Slide -> Jump | Slide -> Idle |
|---|---|---|---|
| IsOnWall = true | IsOnWall = false | IsJumping = true | IsOnWall = false |
| Speed Greater 0 | IsOnWall = false | IsJumping = false | Speed Less 0.5 | |

最后，选择 `RunAnimation` 块，将动画的速度改为 `2.5`。

接下来，你将修改角色脚本以调整新的动画参数。这将允许动画根据玩家的状态发生变化。

在代码编辑器中打开 `SoyBoyController.cs`。

在 `Update()` 方法中，使用 `Input.GetAxis()` 方法（位于顶部附近），添加：

```csharp
animator.SetFloat("Speed", Mathf.Abs(input.x));
```

在同一个 `Update()` 方法中，更改检查 Y 轴输入的代码：

```csharp
if (input.y >= 1f)
{
    jumpDuration += Time.deltaTime;
}else{
    isJumping = false;
    jumpDuration = 0f;
}
```

改为：

```csharp
if (input.y >= 1f) {
    jumpDuration += Time.deltaTime;
    animator.SetBool("IsJumping", true);
}else{
    isJumping = false;
    animator.SetBool("IsJumping", false);
    jumpDuration = 0f;
}
```

再次在 `Update()` 方法中，在显示 `isJumping = true;` 的代码大括号后添加：

```csharp
if (input.y > 0f)
{
    isJumping = true;
}
```

添加：

```csharp
animator.SetBool("IsOnWall", false);
```

接下来移动到 `FixedUpdate()` 方法并替换此代码：

```csharp
if (IsWallToOrRight && !PlayerIsOnGround)
{
    rb.velocity = new Vector2(-GetWallDirection()) * speed * 0.75f, rb.velocity.y);
}
```

改为：

```csharp
if (IsWallToOrRight && !PlayerIsOnGround && input.y == 1)
{
    rb.velocity = new Vector2(-GetWallDirection()) * speed * 0.75f, rb.velocity.y);
    animator.SetBool("IsOnWall", false);
    animator.SetBool("IsJumping", true);
}
else if (!IsWallToOrRight())
{
    animator.SetBool("IsNotWall", false);
    animator.SetBool("IsJumping", true);
}
if (IsWallToOrRight() && !PlayerIsOnGround())
{
    animator.SetBool("IsNotWall", true);
}
```

保存你的更改并运行游戏，使用一些基础控制。Super Soy Boy 应该在所有状态之间切换，包括在靠墙时滑动和掉落。做得好！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_370_0.png)

# 构建游戏障碍

平台类游戏如果没有可以伤害玩家的障碍就是是不完整的。在本节中，你将制作一个能够将 Super Soy 切碎的锯片障碍！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_370_1.png)

首先创建一个锯片障碍。将其命名为 `Hazard`。从 `Sprites` 文件夹将锯片精灵拖到场景中。

选择锯片 `GameObject`，点击 `Add Component`（添加组件）并选择新的 `C# Script`。在代码编辑器中打开 `Hazard` 脚本。在类顶部添加以下字段：

```csharp
public GameObject playerDeathPrefab;
public AudioClip deathClip;
public Sprite hitSprite;
private SpriteRenderer spriteRenderer;
```

在 `Start()` 方法上方添加以下内容：

```csharp
void Awake()
{
    spriteRenderer = GetComponent<SpriteRenderer>();
}
```

这在脚本启动时缓存了 `SpriteRenderer` 的引用。现在你将实现玩家碰到锯片时发生的逻辑。使用 Unity 2D 方法：

```csharp
void OnCollision2D(Collision2D coll)
{
    // 1. 首先检查 GameObject 是否拥有 "Player" 标签
    if (coll.transform.tag == "Player")
    {
        // 2. 接下来，确定是否已为脚本分配 AudioClip，以及是否存在有效的 Audio Source
        var audioSource = GetComponent<AudioSource>();
        if (audioSource != null && deathClip != null)
        {
            audioSource.PlayOneShot(deathClip);
        }
        // 3. 在碰撞点实例化 playerDeathPrefab
        Instantiate(playerDeathPrefab, coll.contacts[0].point, Quaternion.identity);
        // 4. 用 hitSprite 交换锯片的精灵
        spriteRenderer.sprite = hitSprite;
        // 5. 最后，销毁碰撞对象（玩家）
        Destroy(coll.gameObject);
    }
}
```

设置主粒子系统（Particle System）属性并进行以下更改：

- Duration: 0.15
- Looping: 未勾选
- Start Lifetime: 2
- Start Speed: 10 到 15 之间随机
- Start Size: 0.15
- Start Rotation: 0 到 360 之间随机
- Gravity Modifier: 3

开启粒子系统上的 `Emission`（发射）部分，并将 `Rate over Time` 设置为300。开启 `Shape`（形状）部分，并将 `Shape` 设置为 `Cone`（锥体），Angle 为35，Radius 为

在场景中创建一个 `GameObject`。将其命名为 `DeathParticleSystem` 并为其添加粒子系统组件。将 `Transform` 组件的 X 轴旋转改为 -90。

你需要的最后一个引用是 `Hazard` 脚本上的 `Player Death Prefab`。这是当玩家碰到障碍时实例化的粒子效果。

保存脚本，回到 Unity 查看锯片 `GameObject` 上的 `Hazard` 脚本。从 `Sprites` 文件夹将锯片-hit 精灵拖到锯片 `GameObject` `Hazard` 脚本中的 `Hit Sprite` 字段。同样地，将 `Sound` 文件夹中的 `ssb_death` 音剪辑拖到 `Death Clip` 字段。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_372_0.png)

## Unity Games by Tutorials 第 13 章：更多 Unity 2D

# Unity 教程游戏制作

0.2. 启用“随时间变化的颜色”（Color over Lifetime）部分，并将颜色渐变设置为从纯白色（100% 透明度）变为 0% 的透明度值。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_373_0.png)

最后，展开渲染器（Renderer）部分，使用选择器将材质（Material）更改为 `Sprite-Default`。将排序层（Sorting Layer）设置为 `Foreground`（前景），并将层级（Order in Layer）值设置为 10。

使用场景视图（Scene view），在选中 `DeathParticleSystem` `GameObject`，点击编辑器视图右下角的播放（Play）按钮。你应该看到一簇“血迹”粒子向空中喷射。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_373_1.png)

将 `DeathParticleSystem` `GameObject` 拖入 `Assets/Prefabs` 文件夹以将其转换为制体（prefab），然后从层级视图（Hierarchy view）/场景中移除它。

在场景编辑器中选中你的 `Buzzsaw` `GameObject`，在项目视图中编辑 `Prefabs` 文件夹，然后将你的新 `DeathParticleSystem` 制体引用拖到 `Hazard` 脚本上的 `Player Death Prefab` 字段中。

点击检查器（Inspector）窗口中 `GameObject` 顶部的 `Apply`（应用），以将 `Buzzsaw` 的更改应用到其底层制体上。你的 `Hazard` 脚本现在看起来应该是这样的：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_373_2.png)

# Unity 教程游戏制作

锯片陷阱中最后需要添加的是旋转。你将通过添加一个简单的旋转脚本来实现这一点。

在 `Scripts` 文件夹中创建一个名为 `RotationScript` 的新 `C#` 脚本，并在代码编辑器中打开它。

在类顶部添加以下变量：

```
public float rotationsPerMinute = 640f;
```

在 `Update()` 方法中，添加以下内容：

```
transform.Rotate(0, 0, rotationsPerMinute * Time.deltaTime,
    Space.Self);
```

这将根据 `rotationsPerMinute` 的值使它挂载的 `GameObject` 绕 Z 轴旋转。保存脚本并返回 Unity 编辑器。

将新的 `RotationScript` 挂载到 `Buzzsaw` `GameObject`，然后点击检查器中的 `Apply` 按钮，将你所做的更改应用到底层制体对象。

在层级窗口中选中 `SoyBoy` `GameObject`，并将 `GameObject` 的标签（tag）设置为 `Player`。将更改应用到 `SoyBoy` 制体。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_374_0.png)

运行游戏，你应该能看到一个旋转得很好的锯片。触碰锯片，Super SoyBoy 就会爆炸成一喷大豆粒子！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_374_1.png)

## 为游戏添加声音

一个包含持续奔跑、跳跃和在墙壁间弹跳的游戏需要一首高能量的复古风背景乐。幸运的是，启动项目已经包含了一首供你使用！

你将循环该轨道以为 Super Soy Boy 提供关卡音乐。在 Unity 中循环单条音乐轨道非常简单。

在场景层级中创建一个名为 `Music` 的新 `GameObject`，并为其添加一个 `Audio Source` 组件。

从 `Sound` 文件夹，将 `supersboy.ogg` 音频片段拖入 `Music` `Audio Source` 组件的 `AudioClip` 字段中。启用 `Loop`（循环）属性，并将 `Volume`（音量）属性调低至 0.45。

现在你将为 Super Soy Boy 接一些音效（SFX）。

在代码编辑器中打开 `SoyBoyController.cs`，并在脚本顶部添加以下变量：

```
public AudioClip runClip;
```
