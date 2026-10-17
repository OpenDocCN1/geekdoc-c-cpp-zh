
你不再使用 `Vector2` 来指示纹理的位置，而是使用 `Rectangle`，它是点（左上角）、宽度和高度的组合。如果 `Rectangle` 的高度与纹理的宽度和高度不匹配，纹理将被缩放到 `Rectangle` 的大小。原始宽高比将被忽略。

如果你只想显示纹理的矩形子集，可以使用 `Draw` 方法的两个稍微扩展的版本之一：

```
Draw(Texture2D texture, Vector2 position, Rectangle?, source, Color color)
Draw(Texture2D texture, Vector2 position, Rectangle destination, Rectangle?, source, Color color)
```

第三个参数是可空的 `Rectangle` 对象。如果你将此参数设置为 `null`，结果与前两个 `Draw` 版本相同。否则，你可以指定图像的像素子集。

接下来两个 `Draw` 版本有五个额外的参数，你在 `DrawStrings` 中见过过它们：

```
Draw(Texture2D texture, Vector2 position, Rectangle?, source, Color color,
    Float rotation, Vector2 origin, float scale, SpriteEffects effects, float depth)
```

```
Draw(Texture2D texture, Vector2 position, Rectangle?, source, Color color,
    Float rotation, Vector2 origin, Vector2 scale, SpriteEffects effects, float depth)
```

与 `DrawString` 一样，旋转角是弧度，按顺时针测量。`origin` 是纹理中的一个点，将与 `position` 参数对齐。你可以均匀缩放

# 第 8 章 纹理与精灵图 181

你会注意到以圈数衡量的速度，以及神秘的 `Polyline` 类的实例化。`LoadContent` 方法与上一个项目非常相似，不是添加一个名为 `turnPoints` 的数组，而是将它们添加到 `Polyline` 类的 `Vertices` 属性中：

XNA 项目: CarOnlineCourse File: Game1.cs (节选)

```
protected override void LoadContent(){
    spriteBatch = new SpriteBatch(GraphicsDevice);
    var car = this.Content.LoadTexture2D("Car");
    carCenter = new Vector2(car.Width / 2, car.Height / 2);
    float margin = car.Width;
    Viewport viewport = this.GraphicsDevice.Viewport;

    polylineInterpolator.Vertices.Add(
        new Vector2(car.Width, car.Width));
    polylineInterpolator.Vertices.Add(
        new Vector2(viewport.Width - car.Width, car.Width));
    polylineInterpolator.Vertices.Add(
        new Vector2(car.Width, viewport.Height - car.Width));
    polylineInterpolator.Vertices.Add(
        new Vector2(viewport.Width - car.Width, viewport.Height - car.Width));
    polylineInterpolator.Vertices.Add(
        new Vector2(car.Width, car.Width));
}
```

还要注意，此方法在最后再次添加了起点，而且这些点并没有精确描述上上项目相同的路线。上一个项目导致汽车从左上到右上，再到右下再到左下，最后回到左上。现在的顺序是从左上到右上，然后对角线向下到左下，再到右下，最后再次对角线回到起点。这正是上一个程序缺乏的灵活性。

与上一章使用参数方程的程序一样，`Update` 现在简单到让你流泪：

XNA 项目: CarOnlineCourse File: Game1.cs (节选)

```
protected override void Update(GameTime gameTime){
    if (GamePad.GetState(PlayerIndex.One).Buttons.Back == ButtonState.Pressed)
        this.Exit();

    float t = (SPEED * (float)gameTime.TotalGameTime.TotalSeconds) % 1;
    float angle;
```

## 第二部分 XNA

## polylineInterpolatorGetValue(t, false, out angle);

```csharp
position = polylineInterpolator.GetValue(t, false, out angle);
rotation = angle + MathHelper.PiOver2;

base.Update(gameTime);
```

与往常一样，t 的计算范围为 0 到 1，0 表示屏幕左上角的轨迹起点，当 t 趋于 1 时，表示它正回到初始位置。如果将 t 直接传递给 PolylineInterpolator 的 `GetValue` 方法，该方法将返回折线沿途某处的的 `Vector2` 值。

作为一个额外奖励，`GetValue` 的最后一个参数允许获取角度值，该值是折线在该点处的切线角。该角度相对于正 X 轴顺时针方向测量。例如，当汽车从左上角行驶到右上时，角度为 0。当汽车从左上角行驶到左下角时，角度在某个位置……位图中的汽车朝上，因此它需要额外旋转 π/2 弧。

`Draw` 方法与之前相同：

## XNA 项目：CarOnPolylineCourse 文件：Game1.cs（节选）

```csharp
protected override void Draw(Game gameTime)
{
    GraphicsBatch.Begin();
    spriteDevice.Clear(Color.Blue);
    spriteBatch.Draw(car, position, null, Color.White, rotation, carCenter, 1, SpriteEffects.None, 0);
    spriteBatch.End();

    base.Draw(gameTime);
}
```

这里是朝向左下角的汽车：

![](img/d9347c1f55fa6d523479d2cd9b4d5459_196_0.png)

# 第 8 章 纹理与精灵 183

为了演示目的，`PolylineInterpolator` 类为了简单性牺牲了效率。

以下是整个类：

XNA 项目：CarOnPolylineCourse 文件：PolylineInterpolator.cs（完整）

```csharp
using System;
using System.Collections.Generic;
using Microsoft.Xna.Framework;

namespace CarOnPolylineCourse
{
    public class PolylineInterpolator
    {
        public PolylineInterpolator()
        {
            Vertices = new List<Vector2>();
        }

        public List<Vector2> Vertices { protected set; get; }

        public float totalLength()
        {
            float totalLength = 0;

            // 注意循环从索引 1 开始
            for (int i = 1; i < Vertices.Count; i++)
            {
                totalLength += (Vertices[i] - Vertices[i - 1]).Length();
            }
            return totalLength;
        }

        public Vector2 GetValue(float t, bool smooth, out float angle)
        {
            if (Vertices.Count == 0)
            {
                return GetValue(Vector2.Zero, Vector2.Zero, t, smooth, out angle);
            }

            else if (Vertices.Count == 1)
            {
                return GetValue(Vertices[0], Vertices[0], t, smooth, out angle);
            }

            if (Vertices.Count == 2)
            {
                return GetValue(Vertices[0], Vertices[1], t, smooth, out angle);
            }

            // 计算总长度
            float totalLength = TotalLength();
            float accumLength = 0;
        }
}
```

## 第二部分 XNA

```csharp
// 注意循环从索引 1 开始
for (int i = 1; i < Vertices.Count; i++)
{
    float prevLength = accumulateLength;
    accumulateLength += Vertices[i - 1].Length();

    if (t >= prevLength / totalLength && t < accumulateLength / totalLength)
    {
        float tPrev = prevLength / totalLength;
        float tThis = accumulateLength / totalLength;
        float tNew = (t - tPrev) / (tThis - tPrev);

        return GetValue(Vertices[i - 1], Vertices[i],
            tNew, smooth, out angle);
    }
}

    return GetValue(Vector2.Zero, Vector2.Zero, t, smooth, out angle);
}

Vector2 GetValue(Vector2 vertex1, Vector2 vertex2, float t,
    smooth, out angle)
{
    angle = (float)Math.Atan2(vertex2.Y - vertex1.Y, vertex2.X - vertex1.X);

    return smooth ? Vector2.SmoothStep(vertex1, vertex2, t) :
        Vector2.Lerp(vertex1, vertex2, t);
}
```

单一的 `Vertices` 属性允许你定义一个 `Vector2` 对象的集合来定义折线。如果你希望折线终回到起点，则需要显式地复制该点。所有的工作都发生在 `GetValue` 方法中。此时，该方法确定折线的总长度。然后它遍历顶点并累加它们的长度，找到累加长度跨越 t 值的顶点对。这些顶点被传递给 `GetValue` 方法，以使用 `Vector2.Lerp` 执行线性插值，并使用程序员的第二个方法 `Math.Atan2` 计算切线角。

等一下：`GetValue` 有一个布尔参数，导致该方法使用 `Vector2.SmoothStep` 而不是 `Vector2.Lerp`。

## XNA 项目: CarOnOvalCourse 文件: Game1.cs (片段)

请注意下面的 `Update` 方法计算了两个角度。第一个称为 `ellipseAngle`，基于 `t` 并决定了在椭圆上的位置。这是传递给椭圆参数方程的角度，用于获取作为 x 和 y 组合的位置：

```csharp
protected override void Update(GameTime gameTime)
{
    if (Gamepad.GetState(PlayerIndex.One).Back == ButtonState.Pressed)
    {
        this.Exit();
    }

    float t = (SPEED / (float)gameTime.TotalGame.Seconds) % 1;
    float ellipseAngle = MathHelper.Pi * t;
    float x = ellipseCenter.X + ellipseRadiusX * (float)Math.Cos(ellipseAngle);
    float y = ellipseCenter.Y + ellipseRadiusY * (float)Math.Sin(ellipseAngle);
    float position = new Vector2(x, y);

    float dxdt = -ellipseRadiusX * (float)Math.Sin(ellipseAngle);
    float dydt = ellipseRadiusY * (float)Math.Cos(ellipseAngle);
    rotation = MathHelper.PiOver2 + Math.Atan2(dydt, dxdt);

    base.Update(gameTime);
}
```

第二个 `Update` 中的角度是 `rotation`。这是控制汽车朝向的角度。`dxdt` 和 `dydt` 变量是我之前展示的参数方程的导数。`Math.Atan2` 方法提供了相对于正 X 轴的旋转角度，这必须旋转 90 度以符合位图的原始方向。

到此时，你可能已经能背诵 `Draw` 方法了：

```csharp
protected override void Draw(GameTime gameTime)
{
    GraphicsDevice.Clear(Color.Blue);

    spriteBatch.Begin();
    spriteBatch.Draw(car, position, null, Color.White, rotation, carCenter, 1, SpriteEffects.None, 0);
    spriteBatch.End();

    base.Draw(gameTime);
}
```

## 通用曲线解决方案

对于不太用参数方程表示的曲线移动，XNA 本身提供了一个基于 `Microsoft.Xna.Framework` 命名空间中 `Curve` 和 `CurveKey` 类的通用解决方案。

`Curve` 类包含一个名为 `Keys` 的属性，类型为 `CurveKeyCollection`，这是一个 `CurveKey` 对象的集合。每个 `CurveKey` 对象允许你指定一个形式为 `(Position, Value)` 的数值对。`Position` 和 `Value` 属性都是 `float` 类型。当你将一个位置传递给 `Curve` 的 `Evaluate` 方法时，它会返回一个插值。

但这一切相当令人困惑，因为正如文档所指出的——`CurveKey` 的 `Position` 属性几乎总是时间，而 `Value` 属性通常是位置，或者更准确地说，是位置的一个坐标。如果你想使用 `Curve` 对二维空间中的点进行插值，你需要两个 `Curve` 实例——一个用于 X 坐标，另一个用于 Y。这些 `Curve` 实例的对待方式非常类似于参数方程。

假设你想让汽车环绕一个看起来像无穷符号的路径，并且假设我们将用两个相邻的圆来近似无穷符号。（我将向你展示的技术将允许你以后在需要时将这两个圆分开。）

![](img/d9347c1f55fa6d523479d2cd9b4d5459_202_0.png)

## 第 8 章：纹理与精灵

在这两个圆上画出 45 度的点：

![](img/d9347c1f55fa6d523479d2cd9b4d5459_203_0.png)

如果每个圆的半径为 1 个单位，整个图形宽 4 个单位，高 2 个单位。这些点的 X 坐标（从左到右）值是 0, 0.293, 1, 0.707, 2, 2.293, 3, 3.707 和 4，Y 坐标（从上到下）的值为 0, 0.293, 1, 1.707 和 2。值 0.707 只是 45 度的正弦和余弦，而 0.293 是 1 减去该值。
