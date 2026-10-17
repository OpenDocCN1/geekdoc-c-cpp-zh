
# 第二部分 XNA

但请等一下，它变成了这样：

![](img/d9347c1f55fa6d523479d2cd9b4d5459_288_0.png)

Pinch 代码看起来很熟悉，不同在于它决定了水平还是垂直增量占主。此信息被传递给 `ComputeScaleMatrix` 方法：

## XNA 项目: MandelbrotSet 文件: Game1.cs (节选)

```csharp
protected override void Update(GameTime gameTime)
{
    ...
    // 读取触摸手势
    while (TouchPanel.IsGestureAvailable)
    {
        GestureSample gesture = TouchPanel.ReadGesture();
        switch (gesture.GestureType)
        {
            case GestureType.Pinch:
                bool xDominates = Math.Abs(gesture.Delta.X) + Math.Abs(gesture.Delta2.X) >
                    Math.Abs(gesture.Delta.Y) + Math.Abs(gesture.Delta2.Y);
                Vector2 oldPoint1 = gesture.Position - gesture.Delta;
                Vector2 newPoint1 = gesture.Position;
                Vector2 oldPoint2 = gesture.Position2 - gesture.Delta2;
                Vector2 newPoint2 = gesture.Position2;
                drawMatrix *= ComputeScaleMatrix(oldPoint1, oldPoint2, newPoint2, xDominates);
                drawMatrix *= ComputeScaleMatrix(newPoint2, oldPoint1, newPoint1, xDominates);
                break;
        case GestureType.PinchComplete:
            // 从缩放像素设置纹理
            pixels = ZoomPixels(pixels, drawMatrix);
            texture.SetData<uint>(pixels);
```
```csharp
// 设置新的 PixelInfo 参数
PixelInfo.xPixelCoordAtComplexOrigin *= drawMatrix.M11;
PixelInfo.xPixelCoordAtComplexOrigin += drawMatrix.M41;
PixelInfo.yPixelCoordAtComplexOrigin *= drawMatrix.M22;
PixelInfo.yPixelCoordAtComplexOrigin += drawMatrix.M42;
PixelInfo.unitsPerPixel /= drawMatrix.M11;

// 重新初始化 PixelInfos
lock(pixelInfoLock)
{
    InitializePixelInfo(pixels);
}
drawMatrix = Matrix.Identity;
globalIteration = 0;
break;
UpdateCoordinateText();
}
base.Update(gameTime);
}
```

`ComputeScaleMatrix` 方法与 DragAndPinch 中的该方法非常相似，只是它在方法的布尔参数后面进行均匀缩放：

## XNA 项目: MandelbrotSet 文件: Game.cs (节选)

```csharp
Matrix ComputeScaleMatrix(Vector2 refPoint, Vector2 oldPoint, Vector2 newPoint, bool xDominates)
{
    float scale = 1;
    if (xDominates)
        scale = (newPoint.X - refPoint.X) / (oldPoint.X - refPoint.X);
    else
        scale = (newPoint.Y - refPoint.Y) / (oldPoint.Y - refPoint.Y);
    if (float.IsNaN(scale) || float.IsInfinity(scale) || scale < 0)
    {
        return Matrix.Identity;
    }
    scale = Math.Min(1.1f, Math.Max(0.9f, scale));
    Matrix matrix = Matrix.CreateTranslation(-refPoint.X, -refPoint.Y, 0);
    matrix *= Matrix.CreateScale(scale, 1);
    matrix *= Matrix.CreateTranslation(refPoint.X, refPoint.Y, 0);
    return matrix;
}
```

# 第二部分 XNA

用于 PinchComplete 手势的 `ZoomPixels` 方法在从目标像素坐标计算源像素坐标时获取矩阵的逆。坦率地说，反转矩阵只是调用 `Matrix.Invert` 方法的问题。程序的早期版本调用 `Matrix.CreateScale`（上上）并将零作为第三个参数。这创建了一个可逆矩阵，而调用 `Invert` 则创建了一个所有字段都为 NaN（“非数字”）的矩阵。这并不可行。

## XNA 项目: MandelbrotSet 文件: Game1.cs (节选)

```csharp
uint[] ZoomPixels(uint[] srcPixels, Matrix matrix)
{
    Matrix invMatrix = Matrix.Invert(matrix);
    uint[] dstPixels = new uint[srcPixels.Length];
    for (int dstY = 0; dstY < PixelInfo.pixelHeight; dstY++)
    {
        int dstRow;
        for (int dstX = 0; dstX < PixelInfo.pixelWidth; dstX++)
        {
            int dstIndex = dstRow + dstX;
            Vector2 dst = new Vector2(dstX, dstY);
            Vector2 src = Vector2.Transform(dst, invMatrix);
            int srcX = (int)(src.X + 0.5f);
            int srcY = (int)(src.Y + 0.5f);
            if (srcX >= 0 && srcX < PixelInfo.pixelWidth &&
                srcY >= 0 && srcY < PixelInfo.pixelHeight)
            {
                int srcIndex = srcY * PixelInfo.pixelWidth + srcX;
                dstPixels[dstIndex] = srcPixels[srcIndex];
            }
            else
            {
                dstPixels[dstIndex] = Color.Black.PackedValue;
            }
        }
    }
    return dstPixels;
}
```

`UpdateCoordinateText` 方法负责计算左上和右下角的坐标、在 `StringBuilder` 中格式化它们并决定它们显示的位置：

## 第 10 章 从手势到变换

为了解决这个问题，我决定由 `Game` 派类专门负责调用 `TouchPanel.GetState`，但游戏将赋予组件处理这些触摸输入的机会。为了适应这一概念，我为 `GameComponent` 和 `DrawableGameComponent` 的派类创建了这个接口：

```
XNA Project: Petzold.Phone.Xna File: IProcessTouch.cs
```
