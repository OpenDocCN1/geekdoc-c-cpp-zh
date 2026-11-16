

游戏会转瞬即刻结束！

为了解决这个问题，游戏使用**增量时间（delta time）**：自上一帧以来经过的游戏时间。要将前面的代码转换为使用增量时间，你不应将移动视为每帧多少像素，而应将其视为每秒多少像素。因此，如果理想的移动速度是每秒150像素，那么以下代码要灵活得多：

单击此处查看代码图像

```
// Update x position by 150 pixels/second

enemy.mPosition.x += 150 * deltaTime;
```

现在，无论帧率如何，代码都能正常工作。在30 FPS时，增量时间约为0.033，因此敌人每帧移动5像素，每秒总共移动150像素。在60 FPS时，敌人每帧仅移动2.5像素，但每秒总共仍移动150像素。60 FPS情况下的运动当然会更平滑，但每秒的总速度保持不变。

由于这在多种帧率下都有效，作为经验法则，游戏世界中的所有内容都应作为增量时间的函数进行更新。

为了帮助计算增量时间，SDL提供了一个`SDL_GetTicks`成员函数，用于返回自`SDL_Init`函数调用以来经过的毫秒数。通过将前一帧的`SDL_GetTicks`结果保存在成员变量中，你可以使用当前值来计算增量时间。

首先，你声明一个`mTicksCount`成员变量（在构造函数中将其初始化为零）：

```
Uint32 mTicksCount;
```

使用`SDL_GetTicks`，你可以创建`Game::UpdateGame`的第一个实现：

单击此处查看代码图像

```
void Game::UpdateGame()
{

    // Delta time is the difference in ticks from last
    // (converted to seconds)
    float deltaTime = (SDL_GetTicks() - mTicksCount) / 1000.0f;

    // Update tick counts (for next frame)
    mTicksCount = SDL_GetTicks();

    // TODO: Update objects in game world as function
    // ...
}
```

考虑首次调用`UpdateGame`时会发生什么。因为`mTicksCount`初始为零，你会得到一个正的`SDL_GetTicks`值（自初始化以来的毫秒数），并将其除以`1000.0f`以得到以秒为单位的增量时间。接下来，你将`SDL_GetTicks`的当前值保存在`mTicksCount`中。在下一帧中，`deltaTime`行根据`mTicksCount`的旧值和新值计算新的增量时间。因此，在每一帧中，你都会根据自上一帧以来经过的刻数来计算增量时间。

虽然允许游戏模拟以系统允许的任何帧率运行似乎是个好主意，但实际上这样做可能会出现多种问题。最显著的是，任何依赖物理效果的游戏（例如带有跳跃的平台游戏）都会根据帧率表现出行为差异。

尽管针对这个问题有更复杂的解决方案，但最简单的解决方案是实现**帧率限制**，它强制游戏循环等待直到目标增量时间过去。例如，假设目标帧率为60 FPS。如果一帧仅在15ms后完成，帧率限制会要求再等待约1.6ms以满足16.6ms的目标时间。

幸运的是，SDL还提供了一种帧率限制方法。例如，为了确保帧之间至少间隔16ms，你可以将以下代码添加到`UpdateGame`的开头：

单击此处查看代码图像

```
while (!SDL_TICKS_PASSED(SDL_GetTicks(), mTicksCount + 16))
{
}
```

你还必须注意增量时间过高的情况。最显著的是，这发生在调试器中逐行执行游戏代码时。例如，如果你在调试器的断点处暂停五秒钟，你会得到一个巨大的增量时间，模拟中的所有内容都会大幅向前跳转。要解决这个问题，你可以将增量时间限制在最大值（例如`0.05f`）。这样，游戏模拟在任何一帧都不会跳得太远。这得出了清单1.5中的`Game::UpdateGame`版本。虽然你还没有更新球拍或球的位置，但至少你正在计算增量时间值。

## 清单1.5 Game::UpdateGame实现

单击此处查看代码图像

```
void Game::UpdateGame()
{
    // Wait until 16ms has elapsed since last frame
    while (!SDL_TICKS_PASSED(SDL_GetTicks(), mTicksCount + 16))
    {
    }

    // Delta time is the difference in ticks from last
    // (converted to seconds)
    float deltaTime = (SDL_GetTicks() - mTicksCount) / 1000.0f;

    // Clamp maximum delta time value

    if (deltaTime > 0.05f)

    {

        deltaTime = 0.05f;

    }

    // TODO: Update objects in game world as function

}
```

## 更新球拍位置

在乒乓球游戏中，玩家根据输入控制球拍的位置。假设你希望W键将球拍向上移动，S键将球拍向下移动。既不按任何键，又或两个键同时按下，都应意味着球拍完全不移动。

你可以使用一个mPaddleDir整数成员变量来具体实现这一点：如果球拍不移动，则设为0；如果球拍向上移动（负y方向），则设为-1；如果球拍向下移动（正y方向），则设为1。

因为玩家通过键盘输入控制球拍的位置，你需要在`ProcessInput`中添加代码，根据输入更新`mPaddleDir`：

```
mPaddleDir = 0;

if (state[SDL_SCANCODE_W])
{
    mPaddleDir -= 1;
}

if (state[SDL_SCANCODE_S])
{
    mPaddleDir += 1;
}
```

注意你如何对`mPaddleDir`进行加减操作，这确保了如果玩家同时按下两个键，`mPaddleDir`将为零。

接下来，在`UpdateGame`中，你可以添加基于增量时间更新球拍的代码：

单击此处查看代码图像

```
if (mPaddleDir != 0)
{
    mPaddlePos.y += mPaddleDir * 300.0f * deltaTime;
}
```

在这里，你根据球拍方向、每秒300.0f像素的速度以及增量时间来更新球拍的y位置。如果mPaddleDir为-1，球拍将向上移动；如果为1，则会向下移动。

一个问题是，这段代码允许球拍移出屏幕。要解决这个问题，你可以为球拍的y位置添加边界条件。如果位置过高或过低，将其移回有效位置：

单击此处查看代码图像

```
if (mPaddleDir != 0)
{
    mPaddlePos.y += mPaddleDir * 300.0f * deltaTime;
    // Make sure paddle doesn't move off screen!
    if (mPaddlePos.y < (paddleH/2.0f + thickness))
    {
        mPaddlePos.y = paddleH/2.0f + thickness;
    }
    else if (mPaddlePos.y > (768.0f - paddleH/2.0f - thickness))
    {
        mPaddlePos.y = 768.0f - paddleH/2.0f - thickness;
    }
}
```

在这里，`paddleH`变量是一个描述球拍高度的常量。有了这段代码，玩家现在可以上下移动球拍，且球拍不会移出屏幕。

## 更新球的位置

更新球的位置比更新球拍的位置要复杂一些。首先，球在x和y两个方向上移动，而不仅仅是一个方向。其次，球需要从墙壁和球拍上弹回，这会改变其运动方向。因此，你既需要表示球的**速度**（速度和方向），又需要执行**碰撞检测**以确定球是否与墙壁发生碰撞。

为了表示球的速度，添加另一个名为`mBallVel`的`Vector2`成员变量。将`mBallVel`初始化为`(-200.0f, 235.0f)`，这意味着球开始时在x方向上以每秒-200像素、在y方向上以每秒235像素的速度移动。（换句话说，球沿着向下且向左的对角线移动。）

为了根据速度更新球的位置，请将以下两行代码添加到`UpdateGame`中：

单击此处查看代码图像

```
mBallPos.x += mBallVel.x * deltaTime;
mBallPos.y += mBallVel.y * deltaTime;
```

这与更新球拍的位置类似，只不过现在你正在 *同时* 更新球在 x *和* y 两个方向上的位置。

接下来，你需要让球从墙壁上弹回的代码。判断球是否与墙壁碰撞的代码，类似于检查球拍是否移出屏幕的代码。例如，如果球的y位置小于或等于球的高度，则球与顶部墙壁发生碰撞。

关键问题是：当球与墙壁碰撞时该怎么办？例如，假设球在碰到顶部墙壁之前正向上且向右移动。在这种情况下，你希望球现在开始向下且向右移动。同样，如果球碰到底部墙壁，你希望球开始向上移动。关键点在于，从顶部或底部墙壁弹回会取消速度的y分量，如图1.7(a)所示。同样，与左侧球拍或右侧墙壁碰撞应取消速度的x分量。

