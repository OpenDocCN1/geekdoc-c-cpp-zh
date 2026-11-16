

我们将完成 50%：(175–100)/150。使用该百分比，我们可以通过样条线和四元数来确定其位置和方向。

## 3D 点的移动

把物理事件想象成玩连线游戏。在这个版本的游戏中，点已经按顺序编号，并且你已经知道我们要描摹的形状是一张人脸。由于大多数脸不是方形的，当你在点之间描摹时，你决定加入艺术元素，让点之间的线条呈现柔和的曲线，而不是生硬的直线。最终结果是，这些曲线让面孔看起来自然得多，也比直接用尺子画出来更悦目。

就像玩连线游戏一样，你在点（或航点）之间绘制线条的方式决定了客户将看到的整体图像。大多数预设物理引擎可以轻松支持多种连线移动算法，包括基本线性方法和多种样条线实现。在本章中，我们将专注于仅使用 Catmull-Rom 样条线 [Dunlop00] 来在点与点之间移动我们的对象。

速度是这种新物理多么颠倒的一个绝佳示例。速度是根据我们放置航点的位置以及允许对象在一对航点之间旅行的时间来确定的。这是程序员在使用这种物理方法时面临的许多逆向思维混乱之一。我们太习惯于给对象加速度和速度，然后将其发送到世界中，以至于当我们意识到一个以 T 时间行驶 X 距离的对象完美契合旧速度公式时，可能会感到困惑。

清单 4.6.1 是一个基本函数，它使用完成百分比、百分比的平方、百分比的立方、我们在 n-2、n-1 和 n+1 间隔处的 X、Y 或 Z 位置作为样条点，以及给定的 X、Y 或 Z 位置来生成当前位置。

## 清单 4.6.1 给定 X、Y 或 Z 的 Catmull-Rom 计算

```
inline float GetSpline(float inOurPoint, float inPercent,
    float inTSquared, float inTCubed,
    float inBack2, float inBack1, float inNext)
{
    return (0.5f * ((2.0f * inBack1 +
        ((-inBack2 + inOurPoint) * inPercent) +
        ((2.0f * inBack2 - 5.0f * inBack1 + 4.0f *
        inOurPoint - inNext) * inTSquared) +
        ((-inBack2 + 3.0f * inBack1 - 3.0f * inOurPoint)
        + inNext)*inTCubed)));
}
```

清单 4.6.2 是一个简化函数，它根据给定的百分比将对象推进到下一个航点。它使用 GetSpline 方法和该航点的结束世界位置来确定当前的 3D 位置。例如，如果 inPercent 为 0.5，对象的当前位置将位于上一个航点和当前航点之间的中点。

## 清单 4.6.2 沿样条路径推进点

```
void AdvanceSpline(float inPercent, GE3DPoint& ioPoint, const
GE3DPoint& inBack2, const GE3DPoint& inBack1,
const GE3DPoint& inNext)
{
inPercent = min(1.0f, inPercent);
float theTSquared = inPercent * inPercent;
float theTCubed = theTSquared * inPercent;
/* Spline for X */
ioPoint.mX = ::GetSpline(ioPoint.mX,
inPercent, theTSquared, theTCubed,
inBack2.mX, inBack1.mX, inNext.mX);
/* Spline for Y */
ioPoint.mY = ::GetSpline(ioPoint.mY,
inPercent, theTSquared, theTCubed,
inBack2.mY, inBack1.mY, inNext.mY);
/* Spline for Z */
ioPoint.mZ = ::GetSpline(ioPoint.mZ,
inPercent, theTSquared, theTCubed,
inBack2.mZ, inBack1.mZ, inNext.mZ);
}
```

清单 4.6.3 展示了使用大部分预计算样条的 AdvanceSpline。如果你想使用更快的样条计算，请像所示那样将大部分数学计算预计算到查找表中。（注意，你将在本章的后续部分看到，可以在运行时影响对象的物理路径。在这种情况下，请使用正常的、较慢的样条计算，因为每次物理路径更改时你都会重新计算样条。）

## 清单 4.6.3 缓存的样条计算

```
/* uses a precomputed array to compute a fast spline */
inline float GetFastSpline(float* inArray, float inSquared,
float inCubed, float inPercent)
{
return (0.5f * (inArray[0] + (inArray[1] * inPercent) +
(inArray[2] * inSquared) + (inArray[3] * inCubed)));
}
```

/* simplified Advance spline method */
void AdvanceSpline(float inPercent, GE3DPoint& ioPoint)
{
ioPoint.mX = GetFastSpline(mOptimizedSplines,
 theSqd, theCube, thePercent);
ioPoint.mY = GetFastSpline(mOptimizedSplines + 4,
 theSqd, theCube, thePercent);
ioPoint.mZ = GetFastSpline(mOptimizedSplines + 8,
 theSqd, theCube, thePercent);
}

## 方向和四元数

方向描述了对象的偏航、俯仰和滚转。简而言之，方向不是对象的位置，而是对象在该位置所面向的方向。如果对象是倒置的、侧倾的或翻滚的，这指的是它的方向。幸运的是，四元数非常适合方向。四元数不仅能出色地平滑修改对象的方向，还能完美契合我们与 3D 移动和样条线一起使用的时间-百分比范式。如果这还不够，使用四元数来推进方向简单到应该是一种犯罪。四元数通过使用球形线性插值，称为“slerping”，在对象的方向上施展魔法，它沿着曲线平滑地缩放方向（参见 [Svarovsky00]）。

## 启动引擎！

是时候将所有部件组装成一台轰鸣的引擎，让我们的游戏玩家兴奋不已。基本引擎的核心很简单。它的工作是处理所有物理节点，使用样条线推进对象位置，然后使用四元数推进方向。最后，应用正确的方向并设置对象的位置。

浏览清单 4.6.4，我们可以看到预设物理引擎的更新代码长什么样。更新中的第一个操作是弹出我们的节点，直到进入正确的时间范围。例如，如果世界时间是 200，而节点 3 从 195 到 220，我们将弹出节点 1 和 2，以确保在节点 3 处准备好进行处理。一旦获得当前节点，我们先推进方向（使用时间和四元数），然后推进 3D 位置（使用时间和样条线）。最后，在完成更新之前，我们确保围绕对象上的正确点（脚、头、中间，随处）进行旋转。它很简单，很快，几乎太容易了。

## 清单 4.6.4 预设物理引擎的更新方法

```
float thePercent;
bool theResult = true;
bool thePointMatches;

/* Ensure our next point is the right one (time-wise) */
AdjustToCorrectPointUsingTime(inWorldTime);

/* any physics nodes? */
if(mPhysicsNodes.empty() == false)
{
    GE3DPoint thePoint;

    /* get our point */
    inCurrentLocation.GetPosition(thePoint);

    /* get the first item */
    FPNode& theNode = mPhysicsNodes.front();

    /* compute the percent(it will be 0-1.0F because
    of the "AdjustToCorrectPoint method" */
    thePercent = ((float)(inWorldTime -
    theNode.mStartTime)) * theNode.mInverseTotalTime;

    /* advance Orientation */
    theNode.mAdvanceOrientation(thePercent,
    mQuatOrientation);
    outResultOrientation = mQuatOrientation;

    /* Advance our location */
    theNode.mAdvanceSpline(thePercent, thePoint,
    theNode.mSplines[0], theNode.mSplines[1],
    theNode.mSplines[2]);

    /* Rotate it at the correct spot. (head/middle/etc) */
    ApplyRotation(theNode, outTransform, thePoint);
}
else
{
    theResult = false;
}
```

## 把它打磨得光鲜亮丽！

与游戏行业的几乎所有事情一样，细节是你能够脱颖而出或与大众落后的地方。一些对物理在客户眼中表现如何产生重大影响的打磨项目来自于为航点添加加速斜坡、动画和效果。其他项目包括将点映射到对象或地形上、围绕对象上的任意点旋转、倒带物理，或引起反应发生。

## 斜坡和倒带

几乎每一步，预设物理似乎都在与传统的物理观念作斗争。我们如何才能不使用加速度，自然地将对象移动过一系列点？幸运的是，四元数需要一个百分比

