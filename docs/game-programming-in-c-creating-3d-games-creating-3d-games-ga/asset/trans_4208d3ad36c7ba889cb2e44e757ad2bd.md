
这之所以有效，是因为如果 point.x < min.x，那么 min.x - point.x 是三个值中最大的，也是 x 轴上的差值。否则，如果 min.x < point.x < max.x，那么零是最大的。最后，如果 point.x > max.x，那么 point.x - max.x 是最大的。一旦你得到所有三个轴上的差值，你就使用距离公式来计算点与 AABB 之间的最终距离的平方：

单击此处查看代码图片

```cpp
float AABB::MinDistSq(const Vector3& point) const
{
    // Compute differences for each axis
    float dx = Math::Max(mMin.x - point.x, 0.0f);
    dx = Math::Max(dx, point.x - mMax.x);
    float dy = Math::Max(mMin.y - point.y, 0.0f);
    dy = Math::Max(dy, point.y - mMax.y);
    float dz = Math::Max(mMin.z - point.z, 0.0f);
    dz = Math::Max(dz, point.z - mMax.z);
    // Distance squared formula
    return dx * dx + dy * dy + dz * dz;
}
```

一旦你有了 `MinDistSq` 函数，你就可以实现球体与 AABB 的相交测试。你找出球体中心与 AABB 之间的最小距离的平方。如果它小于或等于半径的平方，那么球体和 AABB 相交：

单击此处查看代码图片

```cpp
bool Intersect(const Sphere& s, const AABB& box)
{
    float distSq = box.MinDistSq(s.mCenter);
    return distSq <= (s.mRadius * s.mRadius);
}
```

## 胶囊体与胶囊体测试

相交两个胶囊体在概念上很简单。因为两个胶囊体都是带有半径的线段，你首先找出这些线段之间的最小距离的平方。如果距离的平方小于或等于半径平方和，那么两个胶囊体相交：

单击此处查看代码图片

```cpp
bool Intersect(const Capsule& a, const Capsule& b)
{
    float distSq = LineSegment::MinDistSq(a.mSegment,
    b.mSegment);
    float sumRadii = a.mRadius + b.mRadius;

    return distSq <= (sumRadii * sumRadii);
}
```

不幸的是，由于存在多种边界情况，计算两条线段之间的最小距离比较复杂。本章不深入探讨这些细节，但其源代码提供了两条线段的 MinDistSq 实现。

## 线段测试

如前所述，线段在碰撞检测中用途广泛。本章的游戏项目使用线段测试来检测球体弹丸是否与物体碰撞。本节将探讨线段与其他对象之间的几个关键测试。对于这些测试，你不仅想知道线段是否相交，还想知道第一个这样的交点。

本节在很大程度上依赖之前定义的线段参数方程：

L(t) = Start + (End - Start)t where 0 ≤ t ≤ 1

大多数线段相交测试的方法是首先将线段视为一条无限直线——因为如果无限直线与对象不相交，那么线段也不可能相交。一旦你求出无限直线的交点，你就验证 t 是否在线段的 [0, 1] 范围内。

### 线段与平面测试

要找出线段与平面之间的交点，你想知道是否存在一个 t，使得 L(t) 是平面上的一个点：

L(t) · n̂ + d = 0

你可以通过一些代数变换来求解。首先代入 L(t)：

(Start + (End - Start)t) · n̂ + d = 0

因为点积对加法具有分配律，你可以将其改写为：

Start · n̂ + (End - Start) · n̂t + d = 0

最后，你求解 t：

Start · n̂ + (End - Start) · n̂t + d = 0
(End - Start) · n̂t = -Start · n̂ - d
t = (-Start · n̂ - d) / ((End - Start) · n̂)

请注意，如果分母中的点积计算结果为零，则存在除以零的潜在风险。这种情况只会发生在直线垂直于平面法线时，也就是说直线与平面平行。在这种情况下，直线和平面相交的前提是直线完全位于平面上。

计算出 t 的值后，你接着测试它是否在线段范围内，如清单 10.5 所示。这里的 Intersect 函数通过引用返回 t 值，调用者可以使用它来计算交点（如果需要）。

### 清单 10.5 线段与平面相交

单击此处查看代码图片

```cpp
bool Intersect(const LineSegment& l, const Plane& p, float& outT)
{
    // First test if there's a solution for t
    float denom = Vector3::Dot(l.mEnd - l.mStart,
                               p.mNormal);
    if (Math::NearZero(denom))
    {
        // The only way they intersect if start/end are
        // points on the plane (P dot N) == d
        if (Math::NearZero(Vector3::Dot(l.mStart, p.mNormal) - p.mD))
        {
            outT = 0.0f;
            return true;
        }
        else
        {
            return false;
        }
    }
    else
    {
        float numer = -Vector3::Dot(l.mStart, p.mNormal) - p.mD;
        outT = numer / denom;
        // Validate t is within bounds of the line segment
        if (outT >= 0.0f && outT <= 1.0f)
        {
            return true;
        }
        else
        {
            return false;
        }
    }
}
```

### 线段与球体测试

要找出线段与球体之间的交点，你要查找是否存在一个 t 值，使得直线与球体中心 C 之间的距离等于球体半径 r：

||L(t)-C||=r
||Start+(End-Start)t-C||=r
||Start-C+(End-Start)t||=r

为了简化这个方程，你引入代换：

X = Start - C
Y = End - Start
||X + Yt|| = r

为了求解 t，你需要一种方法将其从长度运算内部提取出来。为此，你对方程两边求平方，并将长度平方运算替换为点积：

||X + Yt||^2 = r^2
(X + Yt) · (X + Yt) = r^2

因为点积对向量加法具有分配律，你可以应用 FOIL（首、外、内、末）分配法则：

(X + Yt) · (X + Yt) = r^2
X · X + 2X · Yt + Y · Yt^2 = r^2

然后你将其改写为二次形式：

Y · Yt^2 + 2X · Yt + X · X - r^2 = 0
a = Y · Y
b = 2X · Y
c = X · X - r^2
at^2 + bt + c = 0

最后，你应用二次方程求解公式来求解 t：

t = (-b ± √(b² - 4ac)) / 2a

二次方程的 **判别式**（根号下的值）告诉你方程的解的数量和类型。负判别式意味着解是虚数。就游戏而言，你可以假设没有任何对象具有虚数位置。因此，你知道负判别式意味着直线与球体不相交。否则，二次方程可能有一个或两个解。判别式为零意味着只有一个解，因为直线与球体相切。判别式大于零意味着直线与球体有两个交点。图 10.10 说明了这三种可能性。

![](img/e9afcec1487716b0ef80d7e7c09869c8_681_0.png)

图 10.10 线段与球体相交的可能判别式值

一旦你得到 t 的解，你接着验证 t 是否在范围 [0, 1] 内。因为有两个可能的解，你优先选择较低的 t 值，它代表第一个交点。但是，如果线段起始于球体内部并从球体射出，较高的 t 值代表交点。清单 10.6 给出了线段与球体相交的代码。请注意，如果球体完全包含线段，此函数返回 false。

### 清单 10.6 线段与球体相交

单击此处查看代码图片

```cpp
bool Intersect(const LineSegment& l, const Sphere& s, float& outT)
{
// Compute X, Y, a, b, c as per equations
Vector3 X = l.mStart - s.mCenter;
Vector3 Y = l.mEnd - l.mStart;
float a = Vector3::Dot(Y, Y);
float b = 2.0f * Vector3::Dot(X, Y);
```
