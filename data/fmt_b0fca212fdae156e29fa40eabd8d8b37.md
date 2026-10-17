
```c
protected override void Update(GameTime gameTime)
{
    if (GamePad.GetState(PlayerIndex.One).Buttons.Back == ButtonState.Pressed)
        this.Exit();
// 处理自动移动卡牌并可能启动决赛
bool checkBoxNextAutoMove = false;
foreach (List<CardInfo> final in finals)
    foreach (CardInfo cardInfo in final)
    {
        if (cardInfo.AutoMoveTime > TimeSpan.Zero)
        {
            cardInfo.AutoMoveTime -= gameTime.ElapsedGameTime;
```

```cs
if (cardInfo.AutoMoveTime <= TimeSpan.Zero)
{
    cardInfo.AutoMoveTime = TimeSpan.Zero;
    checkForNextAutoMove = true;
}
cardInfo.AutoMoveInterpolation = (float)cardInfo.AutoMoveTime.Ticks / AutoMoveDuration.Ticks;
```

```cs
if (checkForNextAutoMove && !AnalyzeForAutoMove() && HasWon())
{
    congratsComponent.Enabled = true;
}
...
```

在上述代码的最后部分，通过调用 `Game1.Helpers.cs` 文件中的 `AnalyzeForAutoMove` 方法来标记自动自动移动。该方法在卡牌手动移动后，会在 `Update` 覆盖方法中再次调用。此方法遍历持有区（holds）和堆（piles），并对每张顶部的卡牌调用 `CheckForAutoMove`。如果 `CheckForAutoMove` 返回 `true`，则已经将卡牌转移到相应的最终区域（finals），并且将其从原位置移除。随后，为了上述 `Update` 中显示的实际移动初始化了 `CardInfo` 的三个属性：

## XNA 项目：ThreeCell 文件：Game1.Helpers.cs (节选)

```cs
bool AnalyzeForAutoMove()
{
    for (int hold = 0; hold < 4; hold++)
    {
        CardInfo cardInfo = holds[hold];
        if (cardInfo != null && CheckForAutoMove(cardInfo))
        {
            holds[hold] = null;
            cardInfo.AutoMoveOffset += new Vector2(cardSpots[hold].X,cardSpots[hold].Y);
            cardInfo.AutoMoveInterpolation = 1;
            cardInfo.AutoMoveTime = AutoMoveDuration;
            return true;
        }
    }
    for (int pile = 0; pile < 8; pile++)
    {
        CardInfo cardInfo = TopCard(piles[pile]);
        if (cardInfo != null && CheckForAutoMove(cardInfo)) {
            piles[pile].Remove(cardInfo);
            cardInfo.AutoMoveOffset += new Vector2(cardSpots[pile + 8].X, cardSpots[pile + 8].Y + piles[pile].Count * overlay);
            cardInfo.AutoMoveInterpolation = 1;
            cardInfo.AutoMoveTime = AutoMoveDuration;
            return true;
        }
    }
}
```

确定哪些卡牌（如果有）应该自动移动的逻辑证明是程序中较长的部分之一。复杂之处在于，如果某张卡牌仍具有策略价值，则不应移动到最终集合中。例如，如果堆或持有区中某处黑桃 3 或梅桃 3，那么红桃 4 就不应该移动到最终集合。

## XNA 项目：ThreeCell 文件：Game1.Helpers.cs (节选)

```cs
bool CheckForAutoMove(CardInfo cardInfo) {
    if (cardInfo.Rank == 0) // 即，A
        for (int final = 0; final < 4; final++) {
            if (finals[final].Count == 0) {
                finals[final].Add(cardInfo);
                cardInfo.AutoMoveOffset = -new Vector2(cardSpots[final + 4].X, cardSpots[final + 4].Y);
                return true;
            }
        }
    } else if (cardInfo.Rank == 1) // 即，2 {
        for (int final = 0; final < 4; final++) {
            CardInfo topCardInfo = TopCard(finals[final]);
            if (topCardInfo != null && topCardInfo.Suit == cardInfo.Suit && topCardInfo.Rank == 0) {
                finals[final].Add(cardInfo);
                cardInfo.AutoMoveOffset = -new Vector2(cardSpots[final + 4].X, cardSpots[final + 4].Y);
                return true;
            }
        }
    }
    else
    {
        int slot = -1;
        int count = 0;

        for (int final = 0; final < 4; final++)
        {
            CardInfo topCardInfo = TopCard(finals[final]);

            if (topCardInfo != null)
            {
                if (topCardInfo.Suit == cardInfo.Suit &&
                    topCardInfo.Rank == cardInfo.Rank - 1)
                {
                    slot = final;
                }
            } else if (topCardInfo.Suit < 2 != cardInfo.Suit < 2 &&
                topCardInfo.Rank >= cardInfo.Rank - 1)
            {
                count++;
            }
        }
        if (slot >= 0 && count == 2)
        {
            cardInfo.AutoMoveOffset = -new Vector2(cardSpots[slot + 4].X,
                cardSpots[slot + 4].Y);
            finals[slot].Add(cardInfo);
            return true;
        }
    }
    return false;
}
```

在 `Update` 顺序中，在自动移动卡牌的动画之后，`Update` 会检查用户是否试图通过触摸来“捡起”卡牌。捡起特定的卡牌可能是合法的，也可能非法的。如果卡牌正在移动而用户试图“放下”卡牌，那可能也是非法的。合法性通过调用 `TryPickUpCard` 和 `TryPutDownCard` 来建立。注意手指位置通过 `inverseMatrix` 进行了调整，使其与卡牌的实际位置一致。

## XNA 项目：ThreeCell 文件：Game1.cs (节选)

```cs
protected override void Update(GameTime gameTime)
{
    while (TouchPanel.IsGestureAvailable)
    {
        Gesture gesture = TouchPanel.ReadGesture();
        // 调整位置和偏移
        Vector2 position = Vector2.Transform(gesture.Position, inverseMatrix);
        Vector2 delta = position - Vector2.Transform(gesture.delta, inverseMatrix);

        switch (gesture.Type) {
            case GestureType.Tap:
                // 检查是否按下
                if ((gesture.Position - center).Length() < radius)
                {
                    congratsComponent.Enabled = false;
                }
                break;

            case GestureType.FreeDrag:
                // 继续移动拖取的卡牌
                if (touchedCard != null)
                {
                    touchedPosition += delta;
                }
                // 尝试捡起卡牌
                else if (firstDrag)
                {
                    TryPickUpCard(position);
                    firstDrag = false;
                }
                break;
            case GestureType.DragComplete:
                if (touchedCard != null && TryPutDown(touchedCard))
                {
                    CalculateDisplay();
                    if (!AnalyzeForAutoMove() && HasWon())
                    {
                        congratsComponent.Enabled = true;
                    }
                }
                firstDrag = true;
                touchedCard = null;
                break;
        }
    }
    base.Update(gameTime);
```

这两个方法 `TryPickUpCard` 和 `TryPutDown` 都在 `Game1.Helpers.cs` 文件中实现并建立了游戏规则。`TryPickUpCard` 简单，它获取屏幕上的触摸位置并确定触摸了哪张卡牌。只有持有区中或堆上的卡牌才有资格被捡起，否则方法不会判断用户是否可以对该卡牌进行操作：

## XNA 项目：ThreeCell 文件：Game1.Helpers.cs (节选)

```cs
bool TryPickUpCard(Vector2 position)
{
    for (int hold = 0; hold < 4; hold++)
    {
        if (holds[hold] == null && IsWithinRectangle(position, cardSpots[hold]))
        {
            Point pt = cardSpots[hold].Location;
            touchedCard = holds[hold];
            touchedOrigin = holds;
            touchedOriginIndex = new Vector2(pt.X, pt.Y);
            holds[hold] = null;
            return true;
        }
    }

    for (int pile = 0; pile < 8; pile++)
    {
        if (piles[pile].Count > 0)
        {
            Rectangle pileSpot = cardSpots[pile + 8];
            pileSpot.Offset(0, yOverlay * (piles[pile].Count - 1));

            if (IsWithinRectangle(position, pileSpot))
            {
                Point pt = pileSpot.Location;
                int pileIndex = piles[pile].Count - 1;

                touchedCard = piles[pile][pileIndex];
                touchedOrigin = piles;
                touchedOriginIndex = pile;
                touchedCardPosition = new Vector2(pt.X, pt.Y);
                piles[pile].RemoveAt(pileIndex);
                return true;
            }
        }
    }
    return false;
}
```

一旦卡牌被捡起，`TryPickUpCard` 已经设置了涉及触摸卡牌的字段，这些字段随后用于 `Update` 方法中在屏幕上拖拽。`TryPutDown` 允许将卡牌放入堆集合、持有数组或最终集合中，但必须执行规则。如果释放操作不合法，卡牌将直接恢复到原始位置，没有任何任何动画：

## XNA 项目：ThreeCell 文件：Game1.Helpers.cs (节选)
