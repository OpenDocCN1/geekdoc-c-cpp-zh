

\|P(t) - Q(t)\| = r_p + r_q

您现在以与测试线段与球体相交类似的方式进行。对两边平方，并将长度的平方替换为点积：

\|P(t) - Q(t)\|^2 = (r_p + r_q)^2
(P(t) - Q(t)) \cdot (P(t) - Q(t)) = (r_p + r_q)^2
(P_0 + (P_1 - P_0)t - Q_0 - (Q_1 - Q_0)t)
\cdot (P_0 + (P_1 - P_0)t - Q_0 - (Q_1 - Q_0)t)
= (r_p + r_q)^2

然后，您提取公因式并进行代换：

(P_0 - Q_0 + ((P_1 - P_0) - (Q_1 - Q_0))t)^2
\cdot (P_0 - Q_0 + ((P_1 - P_0) - (Q_1 - Q_0))t)
= (r_p + r_q)

X = P_0 - Q_0
Y = (P_1 - P_0) - (Q_1 - Q_0)
(X + Yt) \cdot (X + Yt) = (r_p + r_q)^2

最后，您将点积分配到加法上，改写为二次形式，并求解二次方程：

(X + Yt) · (X + Yt) = (rp + rq)²
a = Y · Y
b = 2X · Y
c = X · X - (rp + rq)²
at² + bt + c = 0
t = (-b±√(b²-4ac)) / 2a

与线段与球体相交一样，您使用判别式来确定是否存在实数解。然而，对于扫掠球体相交，您只关心第一个交点，即两个 t 值中较小的那个。与之前一样，您必须验证 t 在范围 [0, 1] 内。清单 10.9 给出了扫掠球体相交的代码。该函数通过引用返回 t，因此调用者可以使用它来确定相交时刻球体的位置。

## Listing 10.9 Swept-Sphere Intersection

Click here to view code image

```
bool SweptSphere(const Sphere& P0, const Sphere& P1,
                 const Sphere& Q0, const Sphere& Q1, float& outT)
{
    // Compute X, Y, a, b, and c
    Vector3 X = P0.mCenter - Q0.mCenter;
    Vector3 Y = P1.mCenter - P0.mCenter -
    (Q1.mCenter - Q0.mCenter);

    float a = Vector3::Dot(Y, Y);

    float b = 2.0f * Vector3::Dot(X, Y);

    float sumRadii = P0.mRadius + Q0.mRadius;

    float c = Vector3::Dot(X, X) - sumRadii * sumRadii;

    // Solve discriminant
    float disc = b * b - 4.0f * a * c;

    if (disc < 0.0f)
    {
        return false;
    }
    else
    {
        disc = Math::Sqrt(disc);

        // We only care about the smaller solution
        outT = (-b - disc) / (2.0f * a);

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

## ADDING COLLISIONS TO GAME CODE

前面的章节讨论了用于碰撞的几何对象以及如何检测这些对象之间的相交。本节探讨如何将这些技术融入游戏代码。新的 BoxComponent 类为角色添加 AABB，PhysWorld 类跟踪盒子并按需检测相交。然后，角色移动和新的投射物发射代码利用这一新的碰撞功能。

### The BoxComponent Class

BoxComponent 类的声明与其他组件的声明非常相似。不过，它不是重写 Update 函数，而是重写 OnUpdateWorldTransform 函数。

请记住，拥有该组件的角色在每次重新计算世界变换时都会调用 OnUpdateWorldTransform。

BoxComponent 的成员数据包含两个 AABB 结构体实例：一个用于对象空间边界，一个用于世界空间边界。对象空间边界在 BoxComponent 初始化后不应改变，但世界空间边界会在拥有该组件的角色的世界变换改变时随之改变。最后，BoxComponent 有一个布尔值，用于指定是否希望 BoxComponent 根据世界旋转进行旋转。这样，您可以选择角色旋转时其 BoxComponent 是否随之旋转。清单 10.10 显示了 BoxComponent 的声明。

### Listing 10.10 BoxComponent Declaration

Click here to view code image

```
class BoxComponent : public Component
{
public:
    BoxComponent(class Actor* owner);
    ~BoxComponent();
    void OnUpdateWorldTransform() override;
    void SetObjectBox(const AABB& model) { mObjectBox = model; }
    const AABB& GetWorldBox() const { return mWorldBox; }
    void SetShouldRotate(bool value) { mShouldRotate = value; }

private:
    AABB mObjectBox;
    AABB mWorldBox;
    bool mShouldRotate;
};
```

要获取网格文件的对象空间边界，Mesh 类在其成员数据中也添加了一个 AABB。然后，在加载 gpmesh 文件时，Mesh 对每个顶点调用 AABB::UpdateMinMax，最终得到一个对象空间 AABB。然后，使用网格的角色可以获取网格的对象空间边界，并将这些边界传递给角色的 BoxComponent：

Click here to view code image

```
Mesh* mesh = GetGame()->GetRenderer()->GetMesh("Assets

// Add collision box

BoxComponent* bc = new BoxComponent(this);

bc->SetObjectBox(mesh->GetBox());
```

要将对象边界转换为世界边界，您需要对边界应用缩放、旋转和平移。与构建世界变换矩阵时一样，顺序很重要，因为旋转是围绕原点进行的。清单 10.11 给出了 OnUpdateWorldTransform 的代码。要缩放盒子，您将 min 和 max 乘以拥有该组件的角色的缩放。要旋转盒子，您使用之前讨论过的 AABB::Rotate 函数，传入拥有该组件的角色的四元数。只有在 mShouldRotate 为 true 时（默认情况下为 true）才执行此旋转。要平移盒子，您将拥有该组件的角色的位置添加到 min 和 max 中。

### Listing 10.11 BoxComponent::OnUpdateWorldTransform Implementation

Click here to view code image

```
void BoxComponent::OnUpdateWorldTransform()
{

    // Reset to object space box

    mWorldBox = mObjectBox;

    // Scale

    mWorldBox.mMin *= mOwner->GetScale();

    mWorldBox.mMax *= mOwner->GetScale();

    // Rotate

    if (mShouldRotate)
    {
        mWorldBox.Rotate(mOwner->GetRotation());
    }

    // Translate
    mWorldBox.mMin += mOwner->GetPosition();
    mWorldBox.mMax += mOwner->GetPosition();
}
```

### The PhysWorld Class

就像您有独立的 Renderer 和 AudioSystem 类一样，为物理世界创建一个 PhysWorld 类是合理的。您将 PhysWorld 指针添加到 Game 中，并在 Game::Initialize 中对其进行初始化。

PhysWorld 包含一个 BoxComponent 指针向量以及相应的公共 AddBox 和 RemoveBox 函数，如清单 10.12 中的骨架声明所示。然后，BoxComponent 的构造函数和析构函数可以分别调用 AddBox 和 RemoveBox。这样，PhysWorld 将拥有一个包含所有盒子组件的向量，就像 Renderer 拥有一个包含所有精灵组件的向量一样。

### Listing 10.12 Skeleton PhysWorld Declaration

Click here to view code image

```
class PhysWorld
{
public:
    PhysWorld(class Game* game);
    // Add/remove box components from world
    void AddBox(class BoxComponent* box);
    void RemoveBox(class BoxComponent* box);
    // Other functions as needed
    // ...
private:
    class Game* mGame;
    std::vector<class BoxComponent*> mBoxes;
};
```

既然 PhysWorld 跟踪世界中的所有盒子组件，下一步就是添加对这些盒子进行碰撞测试的支持。您定义了一个名为 SegmentCast 的函数，它接受一个线段，如果线段与盒子相交则返回 true。此外，它通过引用返回关于第一次此类碰撞的信息：

Click here to view code image

```
bool PhysWorld::SegmentCast(const LineSegment& l, CollisionInfo& col)
{
    bool collided = false;

    // Initialize closestT to infinity, so first
    // intersection will always update closestT
    float closestT = Math::Infinity;
    Vector3 norm;

    // Test against all boxes
    for (auto box : mBoxes)
    {
        float t;
```

The `CollisionInfo` struct contains the position of intersection, the normal at the intersection, and pointers to both the `BoxComponent` and `Actor` of the collision:

`CollisionInfo` 结构体包含交点位置、交点处的法线，以及碰撞涉及的 `BoxComponent` 和 `Actor` 的指针：

Click here to view code image

```
struct CollisionInfo
{
    // Point of collision
    Vector3 mPoint;
    // Normal at collision
    Vector3 mNormal;
    // Component collided with
    class BoxComponent* mBox;
    // Owning actor of component
    class Actor* mActor;
};
```

由于线段可能与多个盒子相交，`SegmentCast` 假设最近的交点是最重要的。由于盒子组件向量没有顺序，SegmentCast 不能在第一次相交后直接返回。相反，函数需要针对所有盒子进行测试，并返回 t 值最低的交点结果，如清单 10.13 所示。之所以有效，是因为 t 值最低的交点是距离线段起点最近的交点。SegmentCast 使用之前讨论过的线段与 AABB 相交函数，但现在已修改为同时返回线段相交的那一侧的法线。

### Listing 10.13 PhysWorld::SegmentCast Implementation

Click here to view code image

```
bool PhysWorld::SegmentCast(const LineSegment& l, CollisionInfo& col)
{
    bool collided = false;

    // Initialize closestT to infinity, so first
    // intersection will always update closestT
    float closestT = Math::Infinity;
    Vector3 norm;

    // Test against all boxes
    for (auto box : mBoxes)
    {
        float t;
```

