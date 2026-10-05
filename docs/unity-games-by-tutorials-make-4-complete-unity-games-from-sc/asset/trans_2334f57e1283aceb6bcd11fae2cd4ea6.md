

`speed` 和 `accel` 浮点变量存储了预定义的值，用于计算施加到 Super Boy `Rigidbody` 的力。你将它们设为公共（public），以便在编辑器中轻松地调整它们；例如，你可以使用它们来改变控制手感。

`Vector2` 输入字段存储了控制器在任何时间点的 x 和 y 的当前输入值。负值表示控制向左 (-x) 或向下 (-y)，正值表示控制向右 (x) 或向上 (y)。

最后三个私有字段分别引用 `SpriteRenderer`、`Rigidbody2D` 和 `Animator` 组件。这可以避免让你在 `Update()` 循环中反复查找这些引用。这种方法可以防止不必要的变量赋值迭代对性能产生负面影响。

现在你将创建一个新方法 `Awake()`。在现有的 `Start()` 方法上方添加以下代码。

```cs
void Awake()
{
    sr = GetComponent<SpriteRenderer>();
    animator = GetComponent<Animator>();
    rb = GetComponent<Rigidbody2D>();
}
```

在此方法中，确保你的组件引用在游戏开始时被缓存。

更具体地说，它会在存放 `SoyBoyController.cs` 的 GameObject 上定位组件类型，并将它们分配给这三个字段。通过这种方式，你获得了使用 `GetComponent` 类属性的益处。

为了完善逻辑，请考虑：如果你没有强制要求组件类型，而 GameObject 缺少其中一个或多个组件，那么 `Awake()` 在尝试定位缺失的组件时将会失败！

现在确保 Super Boy 知道朝向哪个方向。你将使用 Unity 的 `Input` 类来解释用户输入，从而改变 Super Boy 精灵的方向。

在 `Update()` 中添加以下代码：

```cs
void Update()
{
    // 1
    input.x = Input.GetAxis("Horizontal");
    input.y = Input.GetAxis("Jump");
    // 2
    if (input.x > 0f)
    {
      sr.flipX = false;
    } else if (input.x < 0f) {
      sr.flipX = true;
    }
}
```

- 1. `Input.GetAxis()` 从名为 `Horizontal` 和 `Jump` 的 Unity 内置控制器获取 X 和 Y 值。这些值将是 -1、0 或 1，取决于控制是左、右、上、下还是中立。该值存储在变量 `input`（这是一个 `Vector2`）的 x 和 y 属性中。
- 2. 如果 `input.x` 大于 0，则玩家面向右，精灵在 X 轴上翻转。否则，玩家必须面向左，因此精灵被设置为“不翻转”。

保存脚本并运行 Unity。

将新创建的 `SoyBoyController` 脚本添加到场景中的 SoyBoy GameObject 上，并点击 Inspector 面中的 `Apply` 按钮以更新 SoyBoy 预制体。运行游戏并按下键盘上的左或右键（或 A 和 D键），查看 Super Soy Boy 切换方向。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_351_0.png)

现在让 Super Soy Boy 跑起来。

打开脚本 `SoyBoyController.cs` 并添加以下代码：

```cs
void FixedUpdate()
{
  // 1
  var acceleration = accel;
  var xVelocity = 0f;
  // 2
  if (input.x == 0) {
    xVelocity = 0f;
  } else {
    xVelocity = rb.velocity.x;
  }
  // 3
  rb.AddForce(new Vector2((input.x * speed) - rb.velocity.x) * acceleration, 0));
  // 4
  rb.velocity = new Vector2(xVelocity, rb.velocity.y);
}
```

- 1. 将 `accel` —— 即公共浮点字段的值赋值给命名为 `acceleration` 的私有变量。这现在看起来似乎是多余的，但稍后你会看到 `acceleration` 用于存储地面力和加速度值，现在定义它是有重要的。
- 2. 如果水平轴控制处于中立状态，则 `xVelocity` 被设置为 0，否则 `xVelocity` 被设置为 `rb`（即 `Rigidbody2D`）组件的当前 x 速度。
- 3. 通过计算水平轴控制的当前值乘以加速度，向 `rb` 添加一个力。
- 4. 将速度重置为新的 `xVelocity`，同时保持当前的 y 速度。

