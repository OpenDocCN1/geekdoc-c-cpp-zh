
```
// Adjust range of radar and radius
float mRadarRange;
float mRadarRadius;
```

mBlips 向量跟踪相对于雷达中心的目标点的 2D 偏移量。更新雷达时，你需要更新 mBlips。这样一来，绘制雷达只需先绘制背景，然后在所需偏移量处绘制目标点贴图。

最后，mRadarRange 和 mRadarRadius 变量是雷达的参数。范围是指雷达在世界中能看到的距离。例如，范围为 2000 表示雷达在世界空间中的范围为 2000 单位。因此，对于每个在玩家 mRadarRange 范围内的目标，你会在雷达上创建一个目标点。半径变量是屏幕上绘制的 2D 雷达的半径。

假设一个游戏的雷达范围为 50 单位。现在想象玩家正前方 25 单位处有一个物体。由于物体位置是 3D 的，你需要将玩家和物体的位置都转换为屏幕雷达的 2D 坐标。在 z-up 世界中，这意味着雷达相当于将玩家和游戏对象投影到 x-y 平面上。这意味着你的雷达会忽略玩家及其追踪对象的 z 分量。

因为雷达上的“上”通常对应世界空间中的前方，而你的世界是 +x 方向向前，仅忽略 z 分量是不够的。对于雷达上的玩家和任何角色，你需要将它们的 (x, y, z) 坐标转换为雷达偏移量的 2D 向量 (y, x)。

一旦玩家和物体的位置都转换为 2D 雷达坐标，你就可以构建一个从玩家指向物体的向量，为清晰起见，该向量记为 \(\vec{a}\)。\(\vec{a}\) 的长度决定了物体是否在雷达范围内。对于之前范围为 50 单位且物体在前方 25 单位处的示例，\(\vec{a}\) 的长度小于最大范围。这意味着物体应出现在雷达中心和边缘之间的中点处。你可以先将 \(\vec{a}\) 除以雷达的最大范围，再乘以雷达的缩放比例，将 \(\vec{a}\) 转换为相对于雷达半径的缩放，并将结果保存在新向量 \(\vec{a}\) 中：

\(\vec{r} = RadarRadius (\vec{a} / RadarRange)\)

然而，大多数雷达会随玩家旋转，使得雷达上的“上”始终对应游戏世界中的前方。这意味着你不能直接将 \(\vec{r}\) 用作雷达目标点的偏移量。相反，你需要计算玩家朝向向量的 x-y 投影与世界前方（单位 x）之间的角度。由于你需要 x-y 平面上的角度，可以使用 atan2 函数计算该角度 \(\theta\)，并根据 \(\theta\) 构建一个 2D 旋转矩阵。回顾一下，对于行向量，2D 旋转矩阵如下：

Rotation(\theta) = \begin{bmatrix} \cos\theta & \sin\theta \\ -\sin\theta & \cos\theta \end{bmatrix}

有了旋转矩阵后，最终的目标点偏移量就是 \(\vec{r}\) 经过该矩阵旋转的结果：

BlipOffset = \(\vec{r} Rotation2D(\theta)\)

清单 11.8 展示了计算所有目标点位置的代码。你需要遍历所有目标组件，并测试拥有者角色是否在雷达范围内。如果是，则使用前面的公式计算目标点偏移量。

### 清单 11.8 HUD::UpdateRadar 实现

点击此处查看代码图像

```
void HUD::UpdateRadar(float deltaTime)
{
    // Clear blip positions from last frame
    mBlips.clear();

    // Convert player position to radar coordinates
    Vector3 playerPos = mGame->GetPlayer()->GetPosition();
    Vector2 playerPos2D(playerPos.y, playerPos.x);

    // Ditto for player forward
    Vector3 playerForward = mGame->GetPlayer()->GetForward();
    Vector2 playerForward2D(playerForward.x, playerForward.y);

    // Use atan2 to get rotation of radar
    float angle = Math::Atan2(playerForward2D.y, playerForward2D.x);
    // Make a 2D rotation matrix
    Matrix3 rotMat = Matrix3::CreateRotation(angle);

    // Get positions of blips
    for (auto tc : mTargetComps)
    {
        Vector3 targetPos = tc->GetOwner()->GetPosition();
        Vector2 actorPos2D(targetPos.y, targetPos.x);

        // Calculate vector between player and target
        Vector2 playerToTarget = actorPos2D - playerPos2D;

        // See if within range
        if (playerToTarget.LengthSq() <= (mRadarRange * mRadarRange))
        {
            // Convert playerToTarget into an offset from
            // the center of the on-screen radar
            Vector2 blipPos = playerToTarget;
            blipPos *= mRadarRadius/mRadarRange;

            // Rotate blipPos
            blipPos = Vector2::Transform(blipPos, rotMat);
            mBlips.emplace_back(blipPos);
        }
    }
}
```

绘制雷达只需先绘制背景，然后遍历每个目标点，将其作为雷达中心的偏移量绘制即可：

**点击此处查看代码图像**

```
const Vector2 cRadarPos(-390.0f, 275.0f);

DrawTexture(shader, mRadar, cRadarPos, 1.0f);

// Blips
for (const Vector2& blip : mBlips)
{

    DrawTexture(shader, mBlipTex, cRadarPos + blip, 1.0f);
}
```

图 11.5 展示了游戏中的雷达。雷达上的每个点都对应游戏世界中的一个目标角色。雷达中间的箭头只是一个额外的贴图，用于显示玩家位置，但它始终绘制在雷达中心。

![](img/e9afcec1487716b0ef80d7e7c09869c8_767_0.png)

### 图 11.5 游戏中的雷达

雷达的其他扩展可能包括根据敌人位于玩家上方还是下方而使用不同的目标点样式。在这样的样式之间切换需要考虑玩家和物体的 z 分量。

## 本地化

**本地化**是将游戏从一个地区或**区域设置**转换到另一个地区或区域设置的过程。最常见的本地化项目包括任何旁白对话以及屏幕上显示的任何文本。例如，使用英语开发的游戏如果要在中国发布，开发者可能希望将其本地化为中文。本地化最大的开支在于内容：有人必须翻译所有文本和对话，而在对话方面，不同的演员必须用不同的语言说出台词。

然而，本地化部分责任在于程序员。就 UI 而言，游戏需要一种系统来轻松显示来自不同区域设置的屏幕文本。这意味着你不能在代码中到处硬编码字符串，例如“Do you want to quit？”。相反，你至少需要一个映射，将类似 "QuitText" 的键与屏幕上显示的实际文本进行转换。

### 使用 Unicode

本地化文本的一个问题是，每个 ASCII 字符只有 7 位信息（尽管内部存储为 1 字节）。仅 7 位信息意味着总共有 128 个字符。在这些字符中，52 个是字母（大写和小写英文），其余字符是数字和其他符号。ASCII 不包含其他语言的任何字形。

为解决这个问题，许多不同公司组成的联盟在 1980 年代引入了 **Unicode** 标准。截至撰写本文时，当前版本的 Unicode 支持超过 100,000 个不同的字形，包括多种语言的字形以及表情符号。

由于单个字节无法表示超过 256 个不同的值，Unicode 必须使用不同的字节编码。存在多种不同的字节编码，包括每个字符为 2 字节或 4 字节的编码。然而，可以说最流行的编码是 **UTF-8**，其中字符串中每个字符的长度在 1 到 4 字节之间可变。在字符串中，有些字符可能只有 1 字节，有些可能是 2 字节，有些可能是 3 字节，有些可能是 4 字节。

虽然这看起来比为每个字符使用固定字节数更复杂，但 UTF-8 的优点在于它与 ASCII 完全向后兼容。这意味着 ASCII 字节序列直接对应相同的 UTF-8 字节序列。可以将 ASCII 视为 UTF-8 的一种特例，其中 UTF-8 字符串中的每个字符都是 1 字节。向后兼容性很可能是 UTF-8 成为万维网以及 JSON 等文件格式默认编码的原因。

不幸的是，C++ 对 Unicode 的内置支持并不完善。例如，`std::string` 类仅用于 ASCII 字符。但是，你可以使用 `std::string` 类来存储 UTF-8 字符串。问题是，如果字符串是 UTF-8 编码的，`length`
