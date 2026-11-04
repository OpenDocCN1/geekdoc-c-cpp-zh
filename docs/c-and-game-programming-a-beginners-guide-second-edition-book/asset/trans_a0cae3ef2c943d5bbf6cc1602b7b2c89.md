

// base
Point[] Vase = this.sharpTriangle();
g.FillPolygon(bFlowerColor, Vase);
}
```

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_316_0.png)

屏幕截图 4.8. 电视机。

```
public void TV(Graphics g, Brush bTVColor, Pen pTVColor) {
    Brush GrayBrush = new SolidBrush(Color.Gray);

    g.FillRectangle(GrayBrush, this.imagePosX, // console
        this.imagePosY, 25, 15);
    g.FillEllipse(bTVColor, this.imagePosX+1, // tube
        this.imagePosY+1, 15, 13);
    g.FillEllipse(bTVColor, this.imagePosX+18, // 1st dial
        this.imagePosY+2, 5, 5);
    g.FillEllipse(bTVColor, this.imagePosX+18, // 2nd dial
        this.imagePosY+7, 5, 5);
    g.DrawLine(pTVColor, this.imagePosX+12, this.imagePosY, // ant. left
        this.imagePosX+5, this.imagePosY-5);
    g.DrawLine(pTVColor, this.imagePosX+14, this.imagePosY, // ant. right
        this.imagePosX+19, this.imagePosY-5);
}
```

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_317_0.png)

屏幕截图 4.9. 台灯。

```
public void Lamp(Graphics g, Brush LampColor, Brush LampshadeColor) {
    Point[] DrawLamp = this.sharpTriangle();
    Point[] DrawLampshade = this.Trapezoid();
    g.FillPolygon(LampColor, DrawLamp);
    g.FillPolygon(LampshadeColor, DrawLampshade);
}
```

我们将在简单的 OnPaint 函数中把这些图像组合起来（参见示例 4.55）。

## 示例 4.55. Battle Tennis 对象的 OnPaint 函数。

```
protected override void OnPaint(PaintEventArgs e) {
    // Write start-up text if game is stopped
    if (gameState.currentState == GameState.Stopped) {
        ...
        if (!MouseInquire) {
            DialogResult result = MessageBox.Show(this,
                "Do you want to enable the mouse?",
                "Mouse Detect?", MessageBoxButtons.YesNo,
                MessageBoxIcon.Question, MessageBoxDefaultButton.Button1,
                MessageBoxOptions.RightAlign);
        }
        MouseInquire = true;
        if (result == DialogResult.Yes) {
            MouseOverride = true;
        }
    }
} else {
    // draw background color
    buffer.ColorFill(Color.Black);
    buffer.ForeColor = Color.Blue;
    // Draw the scores
    if (player.score < HighScore) {
        buffer.DrawText(4*SCALE, 2*SCALE, HighScore.ToString(),
            false);
    } else {
        buffer.DrawText(4*SCALE, 2*SCALE, player.score.ToString(),
            false);
    }

    buffer.DrawText(16 * SCALE, 2*SCALE, player.score.ToString(),
        false);

    // Draw the player
    try {
        destination = new Rectangle(player.imagePosX,
            player.imagePosY, player.imageWidth, player.imageHeight);
        buffer.Draw(destination, PlayerDraw, DrawFlags.Wait);
        ...
        // Draw the ball
        if (theBall.isActive) {
            try {
                destination = new Rectangle(theBall.imagePosX,
                    theBall.imagePosY,
                    theBall.imageWidth, theBall.imageHeight);
                buffer.Draw(destination, TheBallDraw, DrawFlags.Wait);
                ...
                // Draw the targets
                for (int i = 0; i < NUM_TARGETS; i++) {
                    if (targets[i].isActive) {
                        try {
                            destination = new Rectangle(targets[i].imagePosX,
                                targets[i].imagePosY, targets[i].imageWidth,
                                targets[i].imageHeight);
                            buffer.Draw(destination, TargetDraw[i],
                                DrawFlags.Wait);
                            primary.Flip(buffer, FlipFlags.DoNotWait);
                            buffer.Dispose();
                        }
                    }
                }
            }
        }
    }
}
```

## 输入设备：键盘、操纵杆和鼠标

我们再次希望让玩家能够移动。Keyboard 将包含标准的方向、动画和约束方法，Joystick 也是如此。这里再次使用 Mouse，因为 Battle Tennis 提供了类似的网球式移动，主要区别在于横向校准。

## 示例 4.56. Battle Tennis 的键盘控制。

```
private void Keyboard_Tick(object sender, System.EventArgs e) {
    Microsoft.DirectX.DirectXException.IgnoreExceptions();
    ...
    keyboard = new
        Microsoft.DirectX.DirectInput.Device(SystemGuid.Keyboard);
    keyboard.Properties.BufferSize = 8;
    keyboard.Acquire();

    KeyboardState state = keyboard.GetCurrentKeyboardState();

    for (Key k = Key.Escape; k <= Key.MediaSelect; k++) {
        if (state[k] && k == Key.Left) {
            player.direction = AnimatedImage.WEST;
            player.Animate();
            player.ConstrainToBox();
            if (theBall.IsActive == false)
                Invalidate();
            break;
        ...
    }
}
```

## 示例 4.57. Battle Tennis 的操纵杆控制。

```
private void Joystick_Tick(object sender, System.EventArgs e) {
    Microsoft.DirectX.DirectXException.IgnoreExceptions();
    if (gameState.currentState == GameState.State.Stopped)
        return;

    foreach (DeviceInstance instance in
        Manager.GetDevices(DeviceClass.GameControl,
        EnumDevicesFlags.AttachedOnly)) {
        joystick = new
            Microsoft.DirectX.DirectInput.Device(instance.InstanceGuid);
        break;
    }

    if (joystick == null) {return;}

    joystick.SetDataFormat(DeviceDataFormat.Joystick);

    foreach (DeviceObjectInstance d in joystick.Objects) {
        if ((0 != (d.ObjectId & (int)DeviceObjectTypeFlags.Axis))) {
            joystick.Properties.SetRange(ParameterHow.ById,
                d.ObjectId, new InputRange(-1000, 1000));
        }
    }
    joystick.SetCooperativeLevel(this,
        Microsoft.DirectX.DirectInput.CooperativeLevelFlags.Background |
        Microsoft.DirectX.DirectInput.CooperativeLevelFlags.NonExclusive);
    joystick.Properties.AxisModeAbsolute = true;
    joystick.Acquire();
    joystick.Poll();
    JState = joystick.CurrentJoystickState;

    player.direction = 0;

    if (-400 < JState.X) {
        player.direction = AnimatedImage.WEST;
    } else if (-500 > JState.X) {
        player.direction = AnimatedImage.EAST;
    }
    ...

    byte[] buttons = JState.GetButtons();
    if (theBall.isActive == false &&
        gameState.currentState != GameState.State.Stopped) {
        foreach (byte b in buttons) {
            if (0 != (b & 0x80)) {
                FireBall();
                ...
            }
        }
    }
}
```

## 示例 4.58. Battle Tennis 的鼠标控制。

```
private void Mouse_Tick(object sender, System.EventArgs e) {
    Microsoft.DirectX.DirectXException.IgnoreExceptions();
    mouse = new Microsoft.DirectX.DirectInput.Device(SystemGuid.Mouse);
    MouseState mouseData = new MouseState();

    mouse.SetDataFormat(DeviceDataFormat.Mouse);
    mouse.Acquire();
    mouse.Poll();

    // Get the current state of the mouse device.
    mouseData = mouse.CurrentMouseState;

    if (MouseOverride) {
        player.imagePosX = Cursor.Position.X;
        player.imagePosY = Cursor.Position.Y;
        player.ConstrainToBox();

        byte[] buttons = mouseData.GetMouseButtons();
        if (0 != buttons[0] && !theBall.isActive) {
            FireBall();
        }
    }
}
```

## 声音的属性

在第 3 章中，我们研究了 DirectSound 的基础知识。在那里，我们学习了创建声音设备并设置其协作级别的基础知识，以及执行的基础知识。在本节中，我们将研究用于修改声音的 BufferDescription 属性。BufferDescription 方法用于初始化对象的新实例（参见表 4.5）。

| 属性 | 描述 |
|---|---|
| BufferBytes | 一个读/写整数属性；当创建 PrimaryBuffer 设置为 true 的缓冲区时，BufferBytes 必须设置为零。 |
| CanGetCurrentPosition | 一个读/写布尔属性，用于模拟声音。 |
| Control3D | 一个读/写布尔属性，不要与 BufferCaps.Control3D 混淆，用于指示在 3D 空间中生成声音的类型兼容性。Control3D 不能与 ControlPan 一起使用。 |
| ControlEffects | 一个读/写布尔属性，用于确定缓冲区是否可以使用效果处理；条件包括 8/16 位 PCM 格式且不超过两个立体声声道。 |
| ControlFrequency | 一个读/写布尔属性，用于确定缓冲区的频率是否可以被更改。 |
| ControlPan | 一个读/写布尔属性，用于确定缓冲区是否支持声像平移；ControlPan 不能与 Control3D 一起使用。 |
| ControlPositionNotify | 一个读/写布尔属性，用于确定缓冲区是否支持位置通知。 |
| ControlVolume | 一个读/写布尔属性，用于确定缓冲区是否支持音量。 |
| DeferLocation | 一个读/写布尔属性，用于确定是否应在播放时将缓冲区分配给硬件或软件资源。对于使用语音管理的缓冲区，必须设置此标志。 |
| Flags | 一个读/写枚举属性，用于分配与其他 BufferDescriptions 相关的布尔引用。 |
| GlobalFocus | 一个读/写布尔属性，用于确定缓冲区是否为全局。 |
| Guid3DAlgorithm | 一个读/写 GUID 属性，指定用于 3D 虚拟化的算法。 |
| LocateInHardware | 一个读/写布尔属性，用于确定缓冲区是否需要硬件。 |
| LocateInSoftware | 一个读/写布尔属性，用于确定缓冲区是否需要软件（注意，此设置会忽略任何可用硬件）。 |

表 4.5

