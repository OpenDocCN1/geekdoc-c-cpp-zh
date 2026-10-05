

# 挂载角色动画

你已经完成了关于输入的角色控制器（Character Controller），现在将完成动画控制器（Animation Controller）。这将允许你扩展角色控制器来控制动画！如果你需要复习 Unity 的动画，请复阅第 6 章“动画”。

点击 SoyBoy GameObject，然后打开 Animator 窗口。在窗口内部点击 Parameters（参数）选项卡。

目前没有参数。你接下来将添加这些参数。

在 Animator 窗口的 Parameters 区域，连续点击 +（加号）图标三次，每次添加三个参数之一：

- Speed，类型为 Float（浮点型），值为 0.0。
- IsJumping，类型为 Bool（布尔型），未勾选。
- OnWall，类型为 Bool（布尔型），未勾选。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_366_0.png)

现在创建状态。首先定义一个从默认 Entry 状态到 IdleAnimation 的状态更改。右键点击 Entry 状态，选择 Make Transition（制作过渡），然后点击 IdleAnimation 块。

会生成一个从 Entry 指向 IdleAnimation 的箭头。

现在，你需要让 IdleAnimation 成为新的默认状态（由橙色块表示）。右键点击 IdleAnimation 并点击 Set as Layer Default（设置为层默认值）。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_366_1.png)

此过渡不需要任何条件。它将在游戏开始时发生。

现在创建一个从 IdleAnimation 到 RunAnimation 的过渡，再次创建一个从 RunAnimation 回到 IdleAnimation 的过渡。你可能想在窗口中拖动状态块以更好地定位它们。

这是你现在应该拥有的：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_367_0.png)

点击从 IdleAnimation 指向 RunAnimation 的过渡箭头。Inspector（检查器）窗口应会显示此过渡的详情。

点击 Conditions（条件）下方的 +（加号）图标，并在 Condition 下拉菜单中选择 Speed 参数。确保勾选设置为 Greater than（大于） 0。取消勾选 Has Exit Time（退出时间）。这确保了一旦满足参数指标，动画就会立即切换状态。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_367_1.png)

点击从 RunAnimation 指向 IdleAnimation 的过渡箭头。
点击 Conditions 下方的 +（加号）图标，在 Condition 下拉菜单中选择 Speed 参数。这次你想要从跑步过渡回空闲，因此将勾选设置为 Less than（小于） 0.05。当玩家松开水平移动控制时，速度将降至 0，并满足此条件。

不要忘记取消勾选 Has Exit Time 复选框，因为你希望在条件满足时动画尽可能地退出。

完成所有过渡箭头的创建，你需要根据下面的图片设置这些过渡：

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_368_0.png)

在你制作的每一个过渡上，确保在该过渡的 **Inspector**（检查器）中取消勾选 **Has Exit Time** 复选框。

每个状态之间都有相互过渡，但 **SlideAnimation** 和 **IdleAnimation** 之间除外，那里只有一个从滑动到空闲的状态更改。

点击 **Animator** 编辑器中的每个过渡箭头，并按照下表指定的创建条件以完成 Animator Controller。

| Idle -> Jump | Jump -> Idle | Run -> Jump | Jump -> Run |
|---|---|---|---|
| IsJumping = true | Speed Less 0.05 | IsJumping = true | IsJumping = false |
| Speed Less 0.5 | IsJumping = false | | Speed Greater 0 |
| | IsOnWall = false | | |

| Run -> Slide | Slide -> Run | Slide -> Jump | Slide -> Idle |
|---|---|---|---|
| IsOnWall = true | IsOnWall = false | IsJumping = true | IsOnWall = false |
| Speed Greater 0 | IsOnWall = false | IsJumping = false | Speed Less 0.5 | |

最后，选择 **RunAnimation** 块，将动画的速度改为 **2.5**。

接下来，你将修改角色脚本以调整新的动画参数。这将允许动画根据玩家的状态发生变化。

在代码编辑器中打开 **SoyBoyController.cs**。

在 **Update()** 方法中，使用 **Input.GetAxis()** 方法（位于顶部附近），添加：

```csharp
animator.SetFloat("Speed", Mathf.Abs(input.x));
```

在同一个 Update() 方法中，更改检查 Y 轴输入的代码：

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

再次在 Update() 方法中，在显示 `isJumping = true;` 的代码大括号后添加：

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

接下来移动到 FixedUpdate() 方法并替换此代码：

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

首先创建一个锯片障碍。将其命名为 Hazard。从 Sprites 文件夹将锯片精灵拖到场景中。

选择锯片 GameObject，点击 Add Component（添加组件）并选择新的 C# Script。在代码编辑器中打开 Hazard 脚本。在类顶部添加以下字段：

```csharp
public GameObject playerDeathPrefab;
public AudioClip deathClip;
public Sprite hitSprite;
private SpriteRenderer spriteRenderer;
```

在 Start() 方法上方添加以下内容：

```csharp
void Awake()
{
    spriteRenderer = GetComponent<SpriteRenderer>();
}
```

这在脚本启动时缓存了 SpriteRenderer 的引用。现在你将实现玩家碰到锯片时发生的逻辑。使用 Unity 2D  方法：

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

开启粒子系统上的 Emission（发射）部分，并将 Rate over Time 设置为300。开启 Shape（形状）部分，并将 Shape 设置为 Cone（锥体），Angle 为35，Radius 为

在场景中创建一个 GameObject。将其命名为 DeathParticleSystem 并为其添加粒子系统组件。将 Transform 组件的 X 轴旋转改为 -90。

你需要的最后一个引用是 Hazard 脚本上的 Player Death Prefab。这是当玩家碰到障碍时实例化的粒子效果。

保存脚本，回到 Unity 查看锯片 GameObject 上的 Hazard 脚本。从 Sprites 文件夹将锯片-hit 精灵拖到锯片 GameObject Hazard 脚本中的 Hit Sprite 字段。同样地，将 Sound 文件夹中的 ssb_death 音剪辑拖到 Death Clip 字段。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_372_0.png)

# Unity Games by Tutorials 第 13 章：更多 Unity 2D

