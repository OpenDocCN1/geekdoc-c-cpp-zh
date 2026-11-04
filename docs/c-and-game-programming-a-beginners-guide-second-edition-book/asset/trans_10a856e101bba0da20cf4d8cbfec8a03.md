
### 示例 3.72. 添加小行星。

```
private void UseAsteroids_Click(object sender, System.EventArgs e) {
    this.menuItem5.Checked = !this.menuItem5.Checked;
    useAsteroids = this.menuItem5.Checked;

    for (int i = 0; i < MAX_ASTEROIDS; i++) {
        asteroids[i].isActive = useAsteroids;
        timer.getEvent("asteroid" + i).isActive = useAsteroids;
    }
}
```

### 示例 3.73. 设置与初始化

```
// (re) Sets positional data, scores, and other game data
public void Setup() {
    gameState.currentState = GameState.GameState.Started;
    gameState.currentSpeed = DEFAULT_SPEED;

    player1.imagePosX = SCALE;
    player1.imagePosY = this.ClientSize.Height/2;
    player1.score = 0;
    player1.isActive = true;
    player1.direction = AnimatedImage.EAST;

    player2.imagePosX = this.ClientSize.Width - 2*SCALE;
    player2.imagePosY = this.ClientSize.Height/2;
    player2.score = 0;
    player2.isActive = true;
    player2.direction = AnimatedImage.WEST;

    for (int i = 0; i < MAX_MISSILES; i++) {
        player1Missiles[i].isActive = false;
        player2Missiles[i].isActive = false;
    }

    for (int i = 0; i < MAX_ASTEROIDS; i++) {
        asteroids[i].RescaleImage(2 * SCALE, 2 * SCALE);
    }

    timer.Start();
}
```

## 太空战机：整合全部

再次，需要一个管理子程序将这些组件编织到游戏中。
这里，我已将最终产品移植到本书的 CD-ROM 上。（注意，第 3 章包含该游戏的四个版本，例如 Forms、GDI+、GDI+ with DirectX、和纯 DirectX。有关详细信息，请参阅 CD-ROM 上的 Example 3.74/SpaceFighter。）

## 游戏 3—小行星矿工

我们还可以构建一个主要依赖于我们已开发内容的第三个游戏。
Asteroid Miner 的目标是摧毁小行星而不是敌方舰船。
在这里，我们还想回顾用于创建游戏渲染版本的技巧（参见示例 3.75）。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_228_0.png)

### 示例 3.75. 头脑风暴小行星矿工。

- 1. 游戏应有一个玩家（一艘宇宙飞船），它从屏幕中央开始。
- 2. 游戏在加载的瞬间开始。
- 3. 玩家的移动应相对于屏幕是二维的，但应包括斜向移动。
- 4. 飞船应具有推力，但没有刹车或倒车，让动量将其向前携带。
- 5. 飞船将配备武器，至少一种武器，即可以发射到小行星上的导弹。为了保持简单，导弹不会对其他玩家造成伤害。
- 6. 我们将使用黑色背景，并在其上随机放置星星。
- 7. 飞船应发出声音，包括推力、武器的发射以及被击中时的爆炸声。小行星在被击中时也应发出声音。
- 8. 飞船在死亡时不应能够发射，而小行星可以穿过爆炸的船体而不造成伤害。
- 9. 玩家摧毁小行星时会获得分数，坠毁时会失去分数。
- 10. 玩家应拥有标准的三个生命，并自动结束游戏。
- 11. 我们将包含一个允许玩家复活受损飞船的命令；此控制还将兼作超空间模式。游戏将跟踪玩家的分数，允许保存最高分。（注意：保存分数所使用的技术将在第 4 章中解释。）

## GDI+ 绘图

对于我们的第三个游戏，我们希望用一些渲染示例替换手绘图像。屏幕截图 3.17 中表示的飞船可以用简单的 GDI+ DrawPie 命令替换。这里，变化的角度 player.startAngle() 调整我们的飞船，因此只需要一个引用（参见示例 3.76 和 3.77）。

### 示例 3.76. DrawPie 显示。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_229_0.png)

### 示例 3.77. DrawPie 编码。

```csharp
if (player.isActive == true) {
    g.DrawPie(Pens.Blue, player.imagePosX, player.imagePosY,
        SCALE, SCALE, player.startAngle(), 50);
    if (p1Event.isActive) {
        player.Exhaust(g, Brushes.Aqua);
    }
}
```

The Vortex 是太阳的替代版本，例如：

x1 = ImagePosX, y1 = ImagePosY+10
x2 = X+10, y2 = Y+10
x3 = X-10, y3 = Y-10
x4 = X+10, y4 = Y-10
x5 = X-10, y5 = Y+10

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_230_0.png)

图 3.5. 漩涡/太阳。

我们的飞船排气也基于玩家的位置，但在这里我们将大部分数学运算转移到作为子程序 Shapes.cs 列表的一部分的 Exhaust 方法中（参见示例 3.78）。

### 示例 3.78. Exhaust (Shapes.cs)。

```csharp
// game specific - draws an ellipse as connected to a FillPie ship
public int Exhaust(Graphics g, Brush bExhaustColor) {
    switch (this.direction) {
        case 1:
            g.FillEllipse (bExhaustColor, this.imagePosX+21,
                this.imagePosY-1, 5, 5);
            break;
        ...
    }
}
```

鉴于小行星同时被 Space Fighter 和 Asteroid Miner 共享，将其多边形构造函数放在类（Shapes.cs）中而不是实际程序（SpaceFighter.cs 和 AsteroidMiner.cs）中似乎是唯一合乎逻辑的做法。（参见示例 3.79–3.81。）

### 示例 3.79. 小行星。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_231_0.png)

### 示例 3.80. Do Paint。

```csharp
public void DoPaint(Graphics g) {
    // Draw asteroids
    asteroids[0].Asteroid(g, Brushes.Red);
    asteroids[1].Asteroid(g, Brushes.Blue);
    asteroids[2].Asteroid(g, Brushes.Orange);
    asteroids[3].Asteroid(g, Brushes.Yellow);
}
```

### 示例 3.81. 小行星 (Shapes.cs)。

```csharp
// complex shape - reusable as a single item
public void Asteroid(Graphics g, Brush bAsteroidColor) {
    Point[] PolyRoi = {
        new Point(this.imagePosX-this.imageWidth/5,
            this.imagePosY-2*this.imageHeight/5),
        new Point(this.imagePosX+this.imageWidth/5,
            this.imagePosY-2*this.imageHeight/5),
        new Point(this.imagePosX+this.imageWidth/5,
            this.imagePosY-this.imageHeight/5),
        new Point(this.imagePosX+2*this.imageWidth/5,
            this.imagePosY-this.imageHeight/5),
        new Point(this.imagePosX+2*this.imageWidth/5,
            this.imagePosY+this.imageHeight/5),
        new Point(this.imagePosX+this.imageWidth/5,
            this.imagePosY+this.imageHeight/5),
        new Point(this.imagePosX+this.imageWidth/5,
            this.imagePosY+2*this.imageHeight/5),
        new Point(this.imagePosX-this.imageWidth/5,
            this.imagePosY+2*this.imageHeight/5),
        new Point(this.imagePosX-this.imageWidth/5,
            this.imagePosY+this.imageHeight/5),
        new Point(this.imagePosX-2*this.imageWidth/5,
            this.imagePosY+this.imageHeight/5),
        new Point(this.imagePosX-2*this.imageWidth/5,
            this.imagePosY-this.imageHeight/5),
        new Point(this.imagePosX-this.imageWidth/5,
            this.imagePosY-this.imageHeight/5),};

    g.FillPolygon (bAsteroidColor, PolyRoi);
}
```

相比之下，导弹是该组中最简单的，只需一次 FillEllipse 调用，再配合一个简单的 for 循环即可实现多图像（参见示例 3.81 和 3.82）。

### 示例 3.81. 导弹。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_232_0.png)

### 示例 3.82. 导弹编码。

```csharp
// Draw missiles
for (int i = 0; i < MAX_MISSILES; i++) {
    if (playerMissiles [i].isActive)
        g.FillEllipse (Brushes.Black, playerMissiles [i].imagePosX,
            playerMissiles [i].imagePosY, 5, 5);
}
```

## 小行星矿工：整合全部

第 3 章包含该游戏的四个版本（Forms、GDI+、GDI+ with DirectX、和纯 DirectX；有关详细信息，请参阅 CD-ROM 上的 AsteroidMiner.cs。）

## 故障排除

我们又回到了故障排除。这里，不过，我们更像是经验丰富的老手，正在处理几周前对我们来说似乎陌生的游戏的细节。我们已经构建了标准游戏，我们修改过一次、两次，也许第三次，现在我们只是试图弄清楚最后的碎片。当然，显然有些东西出了问题，但试着换个角度看——看看我们走得多远。而且，如果需要再花几天时间达到下一个水平，那么这就是需要的时间。

> > 然而，如果你碰巧是一个浏览者，一个对 C# 还不熟悉的人，那么我建议你停下来，回去做达到这里所需的工作。真的没有必要在 DirectX 问题上挣扎，如果你还没有掌握 GDI+ 下呈现的更安全、但同样丰富的编码。记住，很多游戏结构是相同的，所以你不妨在更简单的格式下学习它们。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_233_0.png)

本节中发现的问题和解决方案专门针对 DirectX 9.0，列在 Installing、DirectDraw、DirectInput 和 DirectSound 类别下。如果你有其他编译或故障排除问题，请参阅最后两章中的故障排除部分。

安装 DirectX 时，重要的是要记住在安装新编译器或新 SDK 之前先卸载之前的或甚至同一版本的 DirectX。如果不先删除旧版本就安装 SDK，将导致安装失败。

DirectDraw 的错误似乎集中在位图上。首先，如果你尝试加载除位图之外的任何文件类型，你会遇到错误。其次，如果程序找不到指定的位图，你会遇到错误。第三，如果程序尝试在指定区域之外显示位图，你会遇到错误。第四，如果你的程序尝试在上一个位图绘制之前显示位图，你会遇到错误。当然，前两个错误在物理上是固有的（文件被移动、格式输入错误）；实际上只有后两个可以通过代码操作来补救。在这里，我们有两个选择：1）包含 try-catch 块以绕过异常或 2）使用忽略异常（参见示例 3.83 和 3.84）。
