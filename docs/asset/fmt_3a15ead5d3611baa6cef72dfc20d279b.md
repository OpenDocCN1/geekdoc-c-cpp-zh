
# XNA Project: ThreeCell File: Game1.Helper.cs (excerpt)

```c
static Texture2D CreateSurface(GraphicsDevice graphicsDevice, Rectangle[] cardSpots)
{
    uint backgroundColor = new Color(0, 0, 0x60).PackedValue;
    uint outlineColor = Color.White.PackedValue;
    uint replayColor = Color.Red.PackedValue;
    Texture2D surface = new Texture2D(graphicsDevice, wSurface, hSurface);
    uint[] pixels = new uint[wSurface * hSurface];

    for (int i = 0; i < pixels.Length; i++) {
        if ((new Vector2(i % wSurface, i / wSurface) - centerReplay).LengthSquared() < radiusReplay * radiusReplay)
            pixels[i] = replayColor;
        else
            pixels[i] = backgroundColor;
    }

    foreach (Rectangle rect in cardSpots)
    {
        // 矩形的顶部
        for (int x = 0; x < wCard; x++) {
            pixels[(rect.Top - 1) * wSurface + rect.Left + x] = outlineColor;
        }
        // ... (逻辑在 OCR 文本中继续)
    }
    // 注意：此处 OCR 文本在此是碎片化/不完整的，
    // 根据上下文重构逻辑流。
    surface.SetData(pixels);
    return surface;
}
```

`Game1` 中的其他方法非常浅易懂：

# XNA Project: PhreeCell File: Game1.Helper.cs (excerpt)

```c
static void ShuffleDeck(CardInfo[] deck)
{
    Random rand = new Random();
    for (int i = 0; i < 52; i++)
    {
        int random = rand.Next(52);
        // ... 交换逻辑
    }
}

static bool IsWithinRectangle(Vector2 point, Rectangle rect)
{
    return point.X >= rect.Left && point.X < rect.Right && point.Y >= rect.Top && point.Y < rect.Bottom;
}

static Rectangle GetTextureSource(CardInfo cardInfo)
{
    return new Rectangle(0, 0, wCard, hCard); // 占位符
}

static CardInfo TopCard(List<CardInfo> cardInfos)
{
    return cardInfos[cardInfos.Count - 1]; // 占位符
}
```

`GetTextureSource` 与大位图配合使用。它返回一个对应最上方卡片的 `Rectangle`。在 `LoadContent` 结束时，游戏几乎准备好调用 `Replay` 方法，该方法会将牌组洗入牌堆中。然而，还有墓碑机制（tombstoning）需要处理。该程序最初是围绕以下构建的：

# XNA Project: ThreeCell File: Game1.cs (excerpt)

```c
protected override void Deactivated(object sender, EventArgs args)
{
    PhoneApplicationService appService = PhoneApplicationService.Current;

    // 保存牌堆
    List<int>[] piles = new List<int>[4];
    for (int i = 0; i < piles.Length; i++)
    {
        piles[i] = new List<int>();
        // ... 保存牌堆的逻辑
    }
    appService.State("piles") = piles;

    // 保存终局
    List<int>[] finals = new List<int>[4];
    for (int i = 0; i < finals.Length; i++)
    {
        finals[i] = new List<int>();
        // ... 保存终局的逻辑
    }
    appService.State("finals") = finals;

    // 保存持有
    int[] holds = new int[4];
    for (int i = 0; i < holds.Length; i++)
    {
        if (this.holds[i] == null)
            holds[i] = -1;
        else
            holds[i] = 13 * this.holds[i].Suit + this.holds[i].Rank;
    }
    appService.State("holds") = holds;

    base.OnDeactivated(sender, args);
}

protected override void OnActivated(object sender, EventArgs args)
{
    PhoneApplicationService appService = PhoneApplicationService.Current;
    // ... 激活逻辑
}
```

```c
if (appService.State.ContainsKey("piles"))
{
    // 获取牌堆整数
    List<int> piles = appService.State["piles"] as List<int>();

    for (int i = 0; i < piles.Length; i++)
    {
        foreach (int cardindex in piles[i])
            this.piles[i].Add(deck[cardindex]);
    }

    // 重放决赛牌整数
    List<int> finals = appService.State["finals"] as List<int>();

    for (int i = 0; i < finals.Length; i++)
    {
        foreach (int cardindex in finals[i])
            this.finals[i].Add(deck[cardindex]);
    }

    // 重放手牌整数
    int[] holds = appService.State["holds"] as int[];

    for (int i = 0; i < holds.Length; i++)
    {
        if (holds[i] != -1)
            this.holds[i] = deck[holds[i]];
    }

    CalculateddisplayMatrix();
}
else
{
    Replay();
}
base.OnActivated(sender, args);
```

好消息是，在 `OnActivated` 覆盖方法的最后，调用了 `Replay` 方法来真正开始游戏。

## 游戏与重放

`Replay` 位于 `Game1.Helper.cs` 类中：

```
XNA Project: PhreeCell File: Game1.Helper.cs (excerpt)

void Replay()
{
    for (int i = 0; i < 4; i++)
```

```c
holds[i] = null;

foreach (List<CardInfo> pile in finals)
    pile.Clear();

foreach (List<CardInfo> pile in piles)
    pile.Clear();

ShuffleDeck(deck);

// 将卡牌分配到牌堆
for (int card = 0; card < 52; card++)
{
    piles[card % 8].Add(deck[card]);
}
CalculateDisplayMatrix();
```

该方法清空了 `holds` 数组以及 `finals` 和 `piles` 集合，随机洗牌，并将其分配到 `piles` 中的八个集合中。方法通过调用 `CalculateDisplayMatrix` 结束。这并不是该方法唯一被调用次数。它在 `OnActivated` 中也会被调用，当程序从挂起（tombstoning）状态恢复时。此后，每当卡牌从一个 `piles` 集合移动或添加到其中时，为了防万一，都会重新计算显示矩阵。

此矩阵负责游戏区域的高度，如果需要更多空间来查看牌堆区域的所有卡牌。程序处理这个问题的方式并不十分优雅。它只是简单地让整个游戏区域变短了一些，包括所有卡牌甚至重放按钮：

![](img/d9347c1f55fa6d523479d2cd9b4d5459_346_0.png)

我对这个解决方案并不完全满意，但这是执行该操作的 `CalculateDisplayMatrix` 方法：

## XNA Project: ThreeCell File: Game1.Helper.cs (excerpt)

```c
void CalculateDisplayMatrix()
{
    // 根据首选的后缓冲区设置，这将为 40
    int viewport = this.GraphicsDevice.Viewport.Height;

    // 计算所需的总高度并垂直缩放
    int maxCardsInPiles = 0;

    foreach (List<CardInfo> pile in piles)
        maxCardsInPiles = Math.Max(maxCardsInPiles, pile.Count);

    int requiredHeight = 2 * yMargin + yCap + 2 * hCard +
        yOverlay * (maxCardsInPiles - 1);

    // 如果需要显示所有卡牌，设置压缩 Y 的矩阵
    if (requiredHeight > viewportHeight)
        displayMatrix = Matrix.Scale(1, (float)viewportHeight / requiredHeight);
    else
        displayMatrix = Matrix.Identity();

    // 寻找命中测试的逆矩阵
    inverseMatrix = Matrix.Invert(displayMatrix);
}
```

`displayMatrix` 用于 `SpriteBatch` 的 `Begin` 调用中，因此它会一次性应用到所有内容上。虽然稍微偏离了我习惯的顺序，但你现在准备好查看 `Game1` 类中的 `Draw` 方法了。

## XNA Project: ThreeCell File: Game1.cs (excerpt)

```c
protected override void Draw(GameTime gameTime)
{
    spriteBatch.Begin(SpriteSortMode.Immediate, null, null, null, null,
        displayMatrix);
    spriteBatch.Draw(surface, Vector2.Zero, Color.White);

    // 绘制手牌
    for (int hold = 0; hold < 4; hold++)
    {
        CardInfo cardInfo = holds[hold];
        if (cardInfo != null)
        {
            Rectangle source = GetCardTextureSource(cardInfo);
            Vector2 destination = new Vector2(cardSpots[hold].X, cardSpots[hold].Y);
        }
    }
```

```c
spriteBatch.Draw(cards, destination, source, Color.White);

// 绘制牌堆
for (int pile = 0; pile < 8; pile++)
{
    Rectangle cardSpot = cardSpots[pile + 8].Count;

    for (int card = 0; card < piles[pile].Count; card++)
    {
        CardInfo cardInfo = piles[pile][card];
        Rectangle source = GetCardTextureSource(cardInfo);
        Vector2 destination = new Vector2(cardSpots[pile + 8].X, cardSpots[pile + 8].Y);
        spriteBatch.Draw(cards, destination, source, Color.White);
    }
}

// 绘制决赛，包含自动移动
for (int pass = 0; pass < 2; pass++)
{
    for (int final = 0; final < 4; final++)
    {
        for (int card = 0; card < finals[final].Count; card++)
        {
            CardInfo cardInfo = finals[final][card];

            if ((pass == 0 && cardInfo.AutoMoveOffset == 0) ||
                (pass == 1 && cardInfo.AutoMoveOffset != 0))
            {
                Rectangle source = GetCardTextureSource(cardInfo);
                Vector2 destination = new Vector2(cardSpots[final + 4].X, cardSpots[final + 4].Y + yOverlay * cardInfo.AutoMoveOffset);
                spriteBatch.Draw(cards, destination, source, Color.White);
            }
        }
    }
}

// 绘制触碰卡牌
if (touchedCard != null)
{
    Rectangle source = GetCardTextureSource(touchedCard);
    spriteBatch.Draw(cards, touchedPosition, Color.White);
}

spriteBatch.End();

base.Draw(gameTime);
```

## 第11章 触摸游戏

在 `SpriteBatch` 对象中调用 `Begin` 并显示表面后，该方法用于绘制卡牌。从最简单的部分开始——`holds` 数组中的四个可能的卡牌。`GetTextureSource` 方法返回卡牌在位图中的矩形，`cardSpot` 数组提供了每个卡牌出现的位置。

下一部分稍微复杂。在显示牌堆区域的卡牌时，`cardSpot` 位置需要偏移以适应重叠的卡牌。真正有问题的地方是决赛，因为它是因为自动移动功能。正如你所看到的，卡牌符合自动移动条件时，会从手牌或牌堆移除并放入决赛集合。然而，卡牌的位置需要从其旧位置到新位置进行动画处理。这就是 `CardInfo` 中 `AutoMoveOffset` 和 `AutoMoveation` 属性的用途。

`Update` 方法几乎完全关注自动移动功能的动画实现和触摸处理。带有嵌套 `foreach` 循环的大部分移动了已标记为自动移动并已进入决赛集合的卡牌。

XNA Project: ThreeCell File: Game1.cs (excerpt)
