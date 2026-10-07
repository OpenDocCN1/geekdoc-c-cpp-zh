
# 创建 ColorBlock 组件

```csharp
// 创建 ColorBlock 组件

Color[] colors = { Color.Red, Color.Red, Color.Green, Color.Blue,

                   Color.Cyan, Color.Magenta, Color.Yellow,

                   new Color(0.2f, 0.2f, 0.2f),

                   Color.Black, new Color(0.4f, 0.4f, 0.4f),

                   new Color(0.6f, 0.6f, 0.6f),

                   new Color(0.8f, 0.8f, 0.8f), Color.White };

foreach (Color cl in colors)
{
    ColorBlock colorBlock = new ColorBlock(this);
    colorBlock.color = cl;
    colorBlocks.Add(colorBlock);
    this.Components.Add(colorBlock);
}

base.Initialize();
}
```

组件的剩余初始化工作在 `LoadContent` 覆盖中进行，此时可以为 `Button` 组件加载字体。在构造函数中显式设置后缓冲区的大小，而在 `LoadContent` 方法中以更抽象的方式计算维度，似乎有点奇怪，但通常保持代码尽可能通用化和灵活是最好的。

## XNA Project: PhingerPaint File: Game1.cs (片段)

```csharp
protected override void LoadContent()
{
    spriteBatch = new SpriteBatch(this.GraphicsDevice);
    Rectangle bounds = this.GraphicsDevice.Viewport;
    SpriteFont font = Content.Load<SpriteFont>("font");

    // 设置按钮
    clearButton.font = font;
    saveButton.font = font;

    Vector2 textSize = font.MeasureString("Save");
    int buttonWidth = (int)textSize.X;
    int buttonHeight = (int)textSize.Y;

    clearButton.Rectangle = new Rectangle(0, 0, buttonWidth, buttonHeight);
    saveButton.Rectangle = new Rectangle(0, buttonHeight + 10, buttonWidth, buttonHeight);

    // 设置块
    for (int i = 0; i < colorBlocks.Count; i++)
    {
        ColorBlock block = colorBlocks[i];
        block.Destination = new Rectangle(0, buttonHeight + 20 + (i * 60), bounds.Width, 50);
    }
}
```

## 第二部分 XNA

它需要一些初始化信息和一个回调函数，因此该方法根据当前日期生成一个唯一文件名：

### XNA Project: PhingerPaint File:Game1.cs (excerpt e)

```c
void OnSaveButtonClick(object sender, EventArgs e)
{
    DateTime dt = DateTime.Now;
    filename = String.Format("PhingerPaint-{0:D2}-{1:D2}-{2:D2}-{3:D2}-{4:D2}-{5:D2}", dt.Year % 100, dt.Month, dt.Day, dt.Hour, dt.Minute, dt.Second);
    Guide.BeginKeyboardInput(PlayerIndex.One, "phinger paint save file",
"enter filename:", filename, KeyboardCallback, null);
}
```

`Guide.BeginKeyboardInput` 会调用程序接收对 `OnDeactivated` 的调用，之后会显示以下屏幕：

![](img/d9347c1f55fa6d523479d2cd9b4d5459_318_0.png)

此屏幕中你可以自定义的部分仅是标题中的文本字符串和输入框中的初始文本。该屏幕在竖屏模式下看起来比横屏模式好得多。在横屏模式下，所有标题、文本框和屏幕键盘都重新调整了方向，但两个按钮没有，这种组合看起来非常奇怪。看一眼你可能就会想在横屏模式下使用 `Guide.BeginKeyboardInput`！当点击“OK”或“Cancel”按钮之一时，程序会被去激活，并调用 PhingerPaint 中的回调函数：

### XNA Project: PhingerPaint File:Game1.cs (excerpt)

```csharp
void KeyboardCallback(AsyncResult result)
{
    filename = Guide.EndKeyboardInput(result);
}
```

你的程序应该假设该回调函数是异步调用的（正如参数所暗示的那样），因此你不应该在这里做太多，除了调用 `Guide.EndKeyboardInput` 并将返回值保存到字段中。如果用户点击了“OK”按钮，则返回值为输入到字段的最终文本。如果用户点击了“Cancel”或返回键，`Guide.EndKeyboardInput` 将返回 `null`。处理该返回值的好位置是在下一次调用程序的 `Update` 时：

### XNA Project: PhingerPaint File:Game1.cs (excerpt)

```csharp
protected override void Update(GameTime gameTime)
{
    if (GamePad.GetState(PlayerIndex.One).Buttons.Back == ButtonState.Pressed)
    {
        this.Exit();
    }
    // 如果保存对话框返回，保存图像
    if (!string.IsNullOrEmpty(filename))
    {
        canvas.SaveToLibrary(filename);
        filename = null;
    }
}
```

注意逻辑检查了 `filename` 字段是否非 `null` 且为空，但在结束时将其设回 `null` 以确保一次。`SaveToLibrary` 并不是 `Texture2D` 类的真实方法！它是 `Petzold.Phone.Xna` 中 `TextureExtensions` 类中的另一个扩展方法。

### XNA Project: Petzold.Phone.Xna File: TextureExtensions.class (excerpt)

```csharp
public static void SaveToLibrary(this Texture2D texture, string filename)
{
    MemoryStream memoryStream = new MemoryStream();
    texture.SaveAsJpeg(memoryStream, texture.Width, texture.Height);
    memoryStream.Position = 0;
    MediaLibrary mediaLibrary = new MediaLibrary();
    mediaLibrary.SavePicture(filename, memoryStream);
    memoryStream.Close();
}
```

这是将 `Texture2D` 保存到手机相库的标准代码。尽管 FingerPaint 在保存图像时使用 PNG 格式，但相库中的图片是 JPEG。`SaveAsJpeg` 方法将图像保存到 `MemoryStream`，然后重置 `MemoryStream` 位置，并带有文件名传递给 `MediaLibrary` 的 `SavePicture` 方法。如果你正在部署到实际手机，并且运行的如 Visual Studio 之类的桌面软件可以与手机通信，这将抛出异常。当以独占模式访问手机媒体库运行时，你可能根据运行的是 32 位还是 64 位 Windows 来终止程序并重启。当然，重写了 `Update` 方法以避免处理触摸输入。我选择使用低级触摸，以便可以在画布上用多个手指绘图。`Button` 基本上根据 `IProcessTouch` 接口处理自己的触摸输入，但 `ColorBlock` 的处理方式不同。类 `get` 本身的 `Update` 方法也处理 `ColorBlock` 组件以及 `Texture2D` 画布。`ColorBlock` 组件的句方式比 `Button` 简单得多。只需触摸 `ColorBlock` 即可选择该项目并将程序切换到该颜色。触摸 ID 被保留且不允许用于其他任何地方。

### XNA Project: FingerPaint File: Game1.cs (excerpt)

```csharp
protected override void Update(GameTime gameTime)
{
    TouchCollection touches = TouchPanel.GetState();
    foreach (TouchLocation touch in touches)
    {
        // 忽略 ColorBlock 的进一步活动
        if (touchIdIgnore && touch.Id == touchIdIgnore)
            continue;
        // 让 Button 组件优先处理触摸
        bool touchHandled = false;
        foreach (GameComponent component in this.Components)
        {
            if (component is IProcessTouch &&
                (component as IProcessTouch).ProcessTouch(touch))
            {
                touchHandled = true;
                break;
            }
        }
        if (touchHandled)
            continue;
        // 检查对 ColorBlock 的点击
        if (touch.State == TouchLocationState.Pressed)
        {
            Vector2 position = touch.Position;
            ColorBlock newSelectedColorBlock = null;
            foreach (ColorBlock colorBlock in colorBlocks)
            {
                Rectangle rect = colorBlock.Bounds;
                if (position.X >= rect.Left && position.X < rect.Right &&
                    position.Y >= rect.Top && position.Y < rect.Bottom)
                {
                    drawingColor = colorBlock.color;
                    newSelectedColorBlock = colorBlock;
                }
            }
            if (newSelectedColorBlock != null)
            {
                foreach (ColorBlock colorBlock in colorBlocks)
                    colorBlock.IsSelected = colorBlock == newSelectedColorBlock;
            }
            touchIdIgnore = touch.Id;
        }
        else
        {
            touchIdIgnore = null;
        }
    }
}
```

剩余的触摸处理用于实际绘图，它只对 `TouchLocationState.Moved` 的值感兴趣。该状态允许调用 `TryPreviousLocation` 方法，然后将两个点传递给 `Petzold.Phone.Xna` 中 `RoundedCapLine` 类的构造函数，为每个笔触提供像素范围：

### XNA Project: PhingerPaint File: Game1.cs (excerpt)

```csharp
protected override void Update(GameTime gameTime)
{
    // 处理触摸输入
    bool canvasNeedsUpdate = false;
    TouchCollection touches = TouchPanel.GetState();
    foreach (TouchLocation touch in touches)
    {
        // 检查触摸移动
        else if (touch.State == TouchState.Moved)
        {
            TouchLocation prevLocation;
            touch.GetPreviousLocation(out prevLocation);
            Vector2 point1 = prevLocation.Position - canvasPosition;
            Vector2 point2 = touch.Position - canvasPosition;
            // 确信触摸位置回来了！
            float radius = 12;
            RoundedCapLine line = new RoundedCapLine(point1, point2, radius);
            int yMin = (int)(Math.Min(point1.Y, point2.Y) - radius);
            int yMax = (int)(Math.Max(point1.Y, point2.Y) + radius);
            yMin = Math.Max(0, Math.Min(canvas.Height, yMin));
            yMax = Math.Max(0, Math.Min(canvas.Height, yMax));
            for (int y = yMin; y < yMax; y++)
            {
                xCollection.Clear();
                line.GetAll(y, xCollection);
                if (xCollection.Count == 2)
                {
                    int xMin = (int)(Math.Min(xCollection[0], xCollection[1]) - 0.5f);
                    int xMax = (int)(Math.Max(xCollection[0], xCollection[1]) + 0.5f);
                    xMin = Math.Max(0, Math.Min(canvas.Width, xMin));
                    xMax = Math.Max(0, Math.Min(canvas.Width, xMax));
                    for (int x = xMin; x < xMax; x++)
                    {
                        pixels[y * canvas.Width + x] = drawingColor.PackedValue;
                    }
                }
            }
        }
    }
}
```
