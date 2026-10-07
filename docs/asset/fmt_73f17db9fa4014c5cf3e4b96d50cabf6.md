
```csharp
protected override void Update(GameTime gameTime)
{
    int yMin = int.MaxValue;
    int yMaxUpdate = 0;
    bool canvasNeedsUpdate = false;

    while (TouchPanel.GetGestures(GestureType.FreeDrag).Count > 0)
    {
        var gesture = TouchPanel.GetGestures(GestureType.FreeDrag)[0];
        RoundCappedLine line = new RoundCappedLine(gesture.StartPoint, gesture.EndPoint, gesture.LineThickness / 2f);

        for (int y = 0; y < canvas.Bounds.Height; y++)
        {
            xCollection.Clear();
            line.GetAllX(y, xCollection);

            if (xCollection.Count == 2)
            {
                int xMin = (int)xCollection[0];
                int xMax = (int)xCollection[1];
                if (xMin > xMax) { int temp = xMin; xMin = xMax; xMax = temp; }

                for (int x = xMin; x < xMax; x++)
                {
                    pixels[y * canvas.Width + x] = Color.Red;
                }
                yMin = Math.Min(yMin, y);
                yMaxUpdate = Math.Max(yMaxUpdate, y);
                canvasNeedsUpdate = true;
            }
        }
    }

    if (canvasNeedsUpdate)
    {
        this.GraphicsDevice.Textures[0] = null;

        int height = yMaxUpdate - yMin;
        Rectangle rect = new Rectangle(0, yMin, canvas.Width, height);
        canvas.SetData<Color>(0, rect, pixels, yMin * canvas.Width);
    }
    base.Update(gameTime);
}
```

# 第 9 章 动态纹理 227

类型为 `Rectangle` 的矩形参数将更新范围限制在 `Texture2D` 内的特定矩形区域。`startIndex` 指向 *pixels* 数组的索引，但 `count` 必须等于 *rectangle* 宽度和高度的乘积。该方法假设从 *startIndex* 开始的 *count* 个像素属于该矩形区域。

如果你正在处理一个对应于整个 `Texture2D` 的单个 *pixels* 数组，并且不想限制在某个矩形区域进行更新，那么你无法灵活地指定任何你想要的矩形，因为 *pixels* 数组中的像素行仍然是基于 *Texture2D* 的全宽排列的。这意味着矩形的宽度必须与 *Texture2D* 的宽度相同。简而言之，你只能将 *SetData* 调用限制为一个或多个整行。这就是为什么你的代码保留了 *yminUpdate* 和 *yMaxUpdate*，而没有保留 X 轴的等效值。

在上面显示的 *Update* 方法中，你还会在调用 *SetData* 之前看到此调用：

```
this.GraphicsDevice.Textures[] = null;
```

当在 *Update* 覆盖方法中调用 *SetData* 时，如果特定的 *Texture2D* 是 *Draw* 方法中最后一个显示的内容且它仍然设置在 *GraphicsDevice* 对象中，这有时是必要的。

*Draw* 覆盖方法非常简单：

| XNA 项目: BetterFingerPaint 文件: Game1.cs (节选) |

| :--- |

```c
protected override void Draw(GameTime gameTime)
{
    spriteBatch.Begin();
    spriteBatch.Draw(canvas, Vector2.Zero, Color.White);
    spriteBatch.End();

    base.Draw(gameTime);
}
```

真正的好消息是触发了显示：

![](img/d9347c1f55fa6d523479d2cd9b4d5459_241_0.png)

笔触是实心的，没有裂缝，而且看看那些精美的圆角。

BetterFingerPaint 程序不会允许你同时用两个手指画画。要使用手势来增强程序功能将变得有些杂乱。单手指的 FreeDrag 手势会产生双手指的 Pinch 手势（这包含有效的 Position2 和 Delta2 属性），那么程序在处理三个手指或同时多个手指时就会失败。

为了处理多个手指，必须回到低级触摸接口，如接下来的 MultiFingerPaint 项目所示。MultiFingerPaint 的大部分内容与 BetterFingerPaint 相同，但构造函数没有启用手势：

# XNA 项目: MultiFingerPaint 文件: Game1.cs (节选)

```c
public Game1()
{
    graphics = new GraphicsDeviceManager(this);
    Content.RootDirectory = "Content";

    // Windows Phone 默认帧率为 30 fps。
    TargetElapsedTime = TimeSpan.FromTicks(3333333);
}
```

我只会向你展示 *Update* 覆盖方法的一部分，因为其余部分与之前相同。该方法本质上是枚举了从 `TouchPanel.GetState` 调用获取的 `TouchCollection`。该集合包含了多个手指触摸屏幕、移动和抬起屏幕的 `TouchLocation` 对象，程序只对移动感兴趣。它不需要跟踪多个手指。它所做的就是获取一个特定的触摸点，通过 `GetPreviousLocation` 获取该手指的上一个触摸点，并在这些点之间画一条线：

# XNA 项目: MultiFingerPaint 文件: Game1.cs (节选)

```c
protected void Update(GameTime gameTime)
{
    // 允许游戏退出
    if (GamePad.GetState(PlayerIndex.One).Buttons == ButtonState.Pressed)
        this.Exit();

    bool canvasNeedsUpdate = false;
    int yMinUpdate = Int32.MaxValue, yMaxUpdate = 0;

    TouchCollection touches = TouchPanel.GetState();

    foreach (TouchLocation touch in touches)
```

if (touch.State == TouchLocation.Moved)

{

    TouchLocation previousTouch;

    touch.GetPreviousLocation(out previousTouch);

    Vector2 point1 = previousTouch.Position;

    Vector2 point2 = touch.Position;

    float radius = 12;

    RoundCappedLine line = new RoundCappedLine(point1, point2, radius);

}

```

这里是同时四个手指的情况：

![](img/d9347c1f55fa6d523479d2cd9b4d5459_243.png)

## 修改现有图像

你可以通过对“源”`Texture2D` 调用 `GetData` 来修改图像，然后通过算法修改像素并使用 `SetData` 将其传输到“目标”`Texture2D`。这在 RippleEffect 项目中所示。源 `Texture2D` 是从网站复制的位图。程序修改像素，使得图像具有横向移动的波浪：

![](img/d9347c1f55fa6d523479d2cd9b4d5459_243_1.png)

程序的字段存储了源（src）和目标（dst）`Texture2D` 对象以及对应的像素数组：

# XNA 项目: RippleEffect 文件: Game1.cs (字段节选)

```c

public class Game : Microsoft.Xna.Framework.Game

{

    GraphicsDevice graphics;

    SpriteBatch spriteBatch;

    const int RIPPLE = 10;

    Texture2d srcTexture;

    Texture2d dstTexture;

    uint[] srcPixels;

    uint[] dstPixels;

    Vector2 position;

    ..

}

```

该常量表示源位图中的像素将上下移动 10 像素。这既用于从源像素计算目标像素的算法，也用于确定目标图像必须比源图像大多少。

`LoadContent` 从程序内容加载 `srcTexture`，并将像素复制到 `srcPixels` 数组中。`dstTexture` 比 `srcTexture` 高 20 像素；为目标像素分配了数组，但尚未对其进行任何操作：

# XNA 项目: RippleEffect 文件: Game1.cs (节选)

```c

protected override void LoadContent()

{

    // 创建一个新的 SpriteBatch，可用于绘制纹理。

    spriteBatch = new SpriteBatch(GraphicsDevice);

    srcTexture = this.Content.Load<Texture2D>("PetoldTattoo");

    srcPixels = new uint[srcTexture.Width * srcTexture.Height];

    srcTexture.GetData(srcPixels);

    dstTexture = new Texture2D(GraphicsDevice, srcTexture.Width, srcTexture.Height + 20);

    dstPixels = new uint[dstTexture.Width * dstTexture.Height];

    Viewport viewport = GraphicsDevice.Viewport;

    position = new Vector2((viewport.Width - dstTexture.Width) / 2, (viewport.Height - dstTexture.Height) / 2);

}

```


```cs

dstPixels[dstIndex] = srcPixels[srcIndex];

}

  this.GraphicsDevice.Textures[0] = null;

  dstTexture.SetData((uint*)dstPixels);

  base.Update(gameTime);

}

```

在这个 `Update` 重写中，`srcTexture` 仅用于判断 `yDst` 是否超出了位图的底一行；显然，我本保存行数并丢弃实际的 `srcTexture` 图像。

`Update` 重写以从数组中的像素更新 `dstTexture` 结束，而 `Draw` 重写只是简单地显示该图像：

## XNA 项目：RippleEffect 文件：Game1.cs (节选)

```cs

protected override void Draw(GameTime gameTime)

{

  GraphicsDevice.Clear(Color.Navy);

  spriteBatch.Begin();

  spriteBatch.Draw(dstTexture, position, Color.White);

  spriteBatch.End();

  base.Draw(gameTime);

}

```

虽然这个程序只修改了坐标，但类似的程序可以修改像素的实际颜色值。还可以基于多个源像素生成目标像素以实现过滤效果。

但如果你在每次 `Update` 调用期间计算像素并传输数据，请注意性能问题。每像素处理和 `SetData` 都需要不短的时间。该程序的第一个版本可以在手机模拟器上运行，但在手机本身上运行缓慢到每秒只有两次更新。我将位图缩小到原始尺寸的 50%（像素数量的 1/4），这显著提升了性能。

在下一章中，我将向你展示如何在第二个执行线程中通过算法计算像素。

# 第 10 章

## 从手势到变换 (From Gestures to Transforms)

Windows Phone 7 应用程序用户输入的主要手段是触摸。Windows Phone 7 设备拥有支持至少四个触摸点的屏幕，应用程序可以编写成一种让用户感到自然直观的方式来适应触摸。

正如你所见到的，XNA 程序员具有获取触摸输入的两种基本方法。通过底层的 `TouchPanel.GetState` 方法，程序可以跟踪单个手指——每个手指由一个 ID 数字识别——在它们触摸屏幕、移动和抬起的过程。`TouchPanel.ReadGesture` 方法提供了一个稍高级的接口，允许对惯性以及以“捏合”（pinch）和“拉伸”（stretch）手势形式的双指操作进行粗略处理。

### 手势与属性 (Gestures and Properties)

`TouchPanel` 类支持的各种手势对应于 `GestureType` 枚举的成员：

- `Tap`（轻点）：快速触摸并抬起
- `DoubleTap`（双击）：两次连续点击中的第二次
- `Hold`（长按）：按住一秒
- `FreeDrag`（自由拖动）：在屏幕上移动手指
- `HorizontalDrag`（水平拖动）：`FreeDrag` 的水平分
- `VerticalDrag`（垂直拖动）：`FreeDrag` 的垂直分
- `DragComplete`（拖动完成）：手指抬离屏幕
- `Flick`（快速滑动）：单指滑动运动
- `Pinch`（捏合）：两个手指相互靠近或分开
- `PinchComplete`（捏合完成）：手指抬离屏幕

要接收特定手势的信息，必须通过设置 `TouchPanel.EnabledGestures` 属性来启用手势。程序随后在 `Game` 类的 `Update` 重写期间以 `GestureSample` 结构的形式获取手势，该结构包含一个用于识别手势的 `GestureType` 属性。

`GestureSample` 还定义了四个 `Vector2` 类型的属性。这些属性对于 `DragComplete` 和 `PinchComplete` 类型无效。其他情况下：

- `Position` 除 `Flick` 之外对所有手势均有效。
- `Delta` 对所有 `Drag` 手势、`Pinch` 和 `Flick` 都有效。
- `Position2` 和 `Delta2` 仅对 `Pinch` 有效。

`Position` 属性指示手指相对于屏幕的当前位置。`Delta` 属性指示手指自上一次位置以来的移动。对于名为 `gestureSample` 的 `GestureSample` 类型对象，

`Vector2 previousPosition = gestureSample.Position - gestureSample.Delta;`

当第一个手指触摸屏幕或手指静止时，`Delta` 向量等于为零。

假设你只对拖动操作感兴趣，并且启用了 `FreeDrag` 和 `DragComplete` 手势。如果你需要跟踪手指从触摸屏幕到抬起期间移动的完整距离，可以使用两种策略之一：要么在 `DragComplete` 之后保存来自 `FreeDrag` 的值并将其与随后的 `Position` 值进行比较，要么将 `Delta` 值累加到一个运行总和中。

让我们来看简单的程序，它允许用户在屏幕上拖动一个小位图。在 `OneFingerDrag` 中，`Game1` 类有字段用于存储 `Texture2D` 并维护其位置：

> XNA 项目：OneFingerDrag 文件: Game1.cs (显示字段的节选)

```cs

public class Game1 : Microsoft.Xna.Framework.Game

{

    GraphicsDevice graphics;

    SpriteBatch spriteBatch;

    Texture2D texture;

    Vector2 texturePosition = Vector2.Zero;

    public Game1()

    {

        graphics = new GraphicsDevice(this);

        Content.RootDirectory = "Content";
