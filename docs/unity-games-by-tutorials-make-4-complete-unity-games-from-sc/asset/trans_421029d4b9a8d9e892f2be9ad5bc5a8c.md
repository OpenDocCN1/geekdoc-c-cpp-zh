

# Unity 游戏教程

```
jumpDuration += Time.deltaTime;
}else{
  isJumping = false;
  jumpDuration = 0f;
}
```

只要按住跳跃键，jumpDuration 就会根据上一帧完成所需的时间（`Time.deltaTime`）计数。如果释放跳跃键，jumpDuration 将重置为 0 以供下次计时使用，并且 `isJumping` 布尔标志将重置为 `false`。

保存代码并运行游戏尝试一下（点击或按住 Space 键测试不同的跳跃高度）。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_361_0.png)

# 处理空中控制

当 Super Soy Boy 处于空中时，你不希望他的移动速度像在地面上跑步时那么敏捷，因此你现在将根据玩家是否在空空中来改变加速度变量。

首先，由于你已经有了 `PlayerIsOnGround()` 布尔检查方法，在 `FixedUpdate()` 方法中，检查 `if (input.x == 0)` 这一行并修改为：

```
if (PlayerIsOnGround() && input.x == 0)
```

这是一个额外的检查，确保只有当玩家在地面且没有使用左或右控制时，`xVelocity` 才会被设置为 0。

在类顶部添加一个新变量，用于存储用于空中控制的值：

```
public float airAccel = 3f;
```

`airAccel` 的值 `3f` 是普通加速度 `accel` 值的一半。你已经为地面移动设置了加速度，现在你将使用 `airAccel` 进行空中控制。这意味着空中控制将不再像地面控制那样灵敏，因此跳跃对玩家来说就不会太困难或令人沮丧（避免跳跃过度补偿）。

Unity 游戏教程

第 13 章：更多 Unity 2D

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_362_0.png)

在 `FixedUpdate()` 方法的顶部，将行 `var acceleration = accel` 替换为：

```
var acceleration = 0f;
if (PlayerIsOnGround()) {
    acceleration = accel;
}
else {
    acceleration = airAccel;
}
```

这段代码首先将 `acceleration` 设置为 0（一个默认初始值）。然后检查玩家是否在地面上，并分别将 `acceleration` 设置为 `accel` 或 `airAccel`。

在方法的下方，使用 `acceleration` 的值作为因子为角色的 `rigidbody` 添加力，因此这现在会根据玩家是否在空中发生动态变化。

# 墙跳

列表中的下一个实现项是墙跳。

首先，你需要一种方法来确定墙是在玩家的左侧还是右侧。这样当玩家从墙上跳起时，你就知道要将他们推离所在的墙。

在 `BoyController.cs` 中，在 `PlayerIsOnGround()` 方法下方，添加以下方法：

```
public bool IsWallToLeftOrRight() {
    // 1
    bool wallOnLeft = Physics2D.Raycast(new Vector2(transform.position.x - width, transform.position.y), -Vector2.right, raycastLengthCheck);
    bool wallOnRight = Physics2D.Raycast(new Vector2(transform.position.x + width, transform.position.y), Vector2.right, raycastLengthCheck);
```

raywender.com

366

```
Vector2.right, raycastLengthCheck;
// 2
if (wallOnLeft || wallOnRight)
{
    return true;
}
else
{
    return false;
}
```

- 1. 你再次利用了 `Physics2D.Raycast` 的隐式布尔转换检查，来查看向角色左侧（`-Vector2.right`）和右侧（`Vector2.right`）发出的两个射线检测是否击中了任何物体。（注意 `raycastLengthCheck` 的值很小，所以射线只会向贴图侧面发射极短的距离来检查墙壁。）
- 2. 如果这两个射线中有一个击中了任何物体，该方法返回 `true`；否则返回 `false`。

现在你需要一种方法来区分玩家是在触碰地面还是墙。幸运的是，你已经有两个可以完成这两个任务的方法。

为了在一个简单的方法中同时知道这两者，你只需通过创建一个方便方法来同时调用这两个方法，并返回 `true` 或 `false`。

在类顶部添加以下变量 `float jump`：

```
public float jump = 14f;
```

现在，在 `IsWallToLeftOrRight()` 方法下方，添加以下新方法：

```
public bool PlayerTouchingGroundOrWall()
{
    if (PlayerIsOnGround() || IsWallToLeftOrRight())
    {
        return true;
    }else
    {
        return false;
    }
}
```

如果角色要么在地面上，或者在左侧或右侧有墙，则该方法将返回 `true`。如果他们贴着墙或在地面上，你就知道要把跳跃值应用到角色的 `rigidbody` 的 `Y` 速度上。否则，你将保持当前的 `Y` 速度不变。

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_363_0.png)

# Unity 游戏教程

在 `FixedUpdate()` 方法中，在 `rb.AddForce(...)` 行的上方编写以下内容：

```
var yVelocity = 0f;
if (PlayerIsTouchingOrWall() && input.y == 1)
{
    yVelocity = jump;
}
else
{
    yVelocity = rb.velocity.y;
}
```

这确保了当角色从地面或墙上跳跃时，`yVelocity` 值被设置为 14 的跳跃值。否则，它被设置为 `rigidbody` 的当前速度。

仍在 `FixedUpdate()` 方法中，修改这一行：

```
rb.velocity = new Vector2(xVelocity, rb.velocity.y);
```

将其修改为：

```
rb.velocity = new Vector2(xVelocity, yVelocity);
```

`yVelocity` 现在被用来修改角色 `Rigidbody` 的速度。在此时阶段，你的角色可以向上跳跃，但他只会直直向上移动。更正确的方法是将他推离墙壁。

在 `PlayerTouchingOrWall()` 方法下方，添加另一个方法：

```
public int GetWallDirection()
{
    bool wallOnLeft = Physics2D.Raycast(new Vector2(transform.position.x - width, transform.position.y), -Vector2.right, raycastLengthCheck);
    bool wallOnRight = Physics2D.Raycast(new Vector2(transform.position.x + width, transform.position.y), Vector2.right, raycastLengthCheck);
    if (wallOnLeft)
    {
        return -1;
    }
    else if (wallOnRight)
    {
        return 1;
    }
    else
    {
        return 0;
    }
}
```

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_364_0.png)

365

# Unity 游戏教程

这根据墙是在左侧（1）、右侧（1）还是都不是（0）返回一个整数。你将使用返回的值乘以角色的 x 速度，根据墙所在的侧向左或右移动（墙跳时）。

在 `FixedUpdate()` 方法中，就在这一行：

```
rb.velocity = new Vector2(xVelocity, yVelocity);
```

添加以下语句：

```
if (IsWallToLeftRight() && !PlayerIsOnGround() && input.y == -1) {
  rb.velocity = new Vector2(-GetWallDirection() * speed * 0.75f, rb.velocity.y);
}
```

这检查玩家左侧或右侧是否有墙、是否不在地面上，以及他们是否正在跳跃。如果是这样，角色的 `Rigidbody` 速度将被设置为一个新的速度，使用当前的 `Y` 速度，但对 `X`（水平）速度进行更改。

墙的反向方向通过调用新的 `GetWallDirection()` 方法并取反其返回的值计算出来（-1 变成 1，1 变成 -1）。

保存你的更改并返回 Unity。在场景编辑器中复制一些单块预制体，并将副本向上堆叠以建造一些墙壁。在场景编辑器中移动它们时，记住按住 `CTRL` 键以保持它们对齐到 1 个单位的大小。

运行游戏，并对着墙跳跃（Space 键）。当你落在墙上时，再次跳跃，向另一个方向移动。有了这种技术，你现在可以扩展规模了！

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_365_0.png)

