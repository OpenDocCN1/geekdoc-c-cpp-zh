

![](img/e9afcec1487716b0ef80d7e7c09869c8_217_0.png)

### 图 3.14 测试两个圆之间的交点

你可以先在两个圆心之间创建一个向量并计算该向量的模长，从而执行此交点测试。然后，将此距离与两个圆的半径之和进行比较：

```
\|A.center - B.center\| \le A.radius + B.radius
```

回顾本章前面关于长度与长度平方的讨论。在圆的交点情况下，你只需要比较距离和半径之和。因为你知道距离和半径都不能为负数，所以可以对等式两边求平方，同时保持不等式不变：

```
\|A.center - B.center\|^2 <= (A.radius + B.radius)^2
```

> 注意
> 本节介绍的方法也适用于球体，因为同样的原理也适用。

## 创建 CircleComponent 子类

为了支持角色的碰撞检测，你可以创建一个 CircleComponent 以及一个用于测试两个圆组件之间交点的方法。然后，你可以将 CircleComponent 添加到任何需要碰撞的角色中。

首先，将 CircleComponent 声明为 Component 的子类，如清单 3.6 所示。CircleComponent 只需要半径这一个成员数据，因为圆心就是拥有者角色的位置。

### 清单 3.6 CircleComponent 声明

单击此处查看代码图片

```
class CircleComponent : public Component
{
public:
CircleComponent(class Actor* owner);
void SetRadius(float radius) { mRadius = radius; }
float GetRadius() const;
const Vector2& GetCenter() const;
private:
float mRadius;
};
```

接下来，声明一个全局 `Intersect` 函数，它以引用方式接收两个圆组件，如果两个圆相互相交则返回 `true`，如清单 3.7 所示。请注意，实现直接镜像了前一节的方程。你首先计算两个圆心之间的距离平方，然后将其与半径平方之和进行比较。

### 清单 3.7 CircleComponent 交点

单击此处查看代码图片

```
bool Intersect(const CircleComponent& a, const CircleComponent& b)
{

    // Calculate distance squared
    Vector2 diff = a.GetCenter() - b.GetCenter();

    float distSq = diff.LengthSq();

    // Calculate sum of radii squared
    float radiiSq = a.GetRadius() + b.GetRadius();

    radiiSq *= radiiSq;

    return distSq <= radiiSq;
}
```

然后，你可以像创建其他组件一样创建一个 `CircleComponent`。例如，以下两行代码将一个 `CircleComponent` 添加到 `Asteroid` 对象（其中 `mCircle` 是指向 `CircleComponent` 的成员变量指针）：

单击此处查看代码图片

```
mCircle = new CircleComponent(this);
mCircle->SetRadius(40.0f);
```

因为飞船发射的每个激光都需要检查与所有小行星的碰撞，你可以向 `Game` 添加一个 `Asteroid` 指针的 `std::vector`。然后，在 `Laser::UpdateActor` 中，你可以轻松地测试与这些小行星中每一个的交点：

单击此处查看代码图片

```
void Laser::UpdateActor(float deltaTime)
{
    // Do you intersect with an asteroid?
    for (auto ast : GetGame()->GetAsteroids())
    {
        if (Intersect(*mCircle, *(ast->GetCircle())))
        {
            // If this laser intersects with an asteroid
            // set ourselves and the asteroid to dead
            SetState(EDead);
            ast->SetState(EDead);
            break;
        }
    }
}
```

对每个小行星调用的 `GetCircle` 函数只是一个公共函数，返回指向小行星的 `CircleComponent` 的指针。同样，`mCircle` 变量是激光的 `CircleComponent`。

`CircleComponent` 在 `Asteroids` 的情况下效果很好，因为你可以用圆来近似游戏中所有对象的碰撞。但是，圆不适用于所有类型的对象，当然也不适用于 3D。第 10 章“碰撞检测”将更详细地深入探讨碰撞检测主题。

## 游戏项目

本章的游戏项目实现了经典游戏 Asteroids 的基本版本。本章前面的部分涵盖了游戏项目中使用的大部分新代码。该项目使用 MoveComponent 和 InputComponent 实现移动。CircleComponent 代码测试飞船的激光是否与小行星碰撞。游戏项目中缺少的一个显著功能是小行星不会与飞船碰撞（不过你将在练习 3.2 中添加该功能）。游戏项目也没有实现牛顿物理（不过你将在练习 3.3 中添加该功能）。代码可在本书的 GitHub 仓库中找到，位于 Chapter03 目录。在 Windows 上打开 Chapter03-windows.sln，在 Mac 上打开 Chapter03-mac.xcodeproj。

本章前面未涵盖的一个游戏功能是当玩家按下空格键时如何创建激光。因为检测空格键输入是 Ship 特有的，所以你应该重写 ActorInput 函数。但是，如果玩家按住空格键（或快速按下），你不希望创建太多激光以至于使游戏变得太简单。相反，你希望有一个冷却时间，飞船每半秒只能发射一次激光。要实现这一点，首先在 Ship 中创建一个 float 类型的 mLaserCooldown 成员变量并将其初始化为 0.0f。接下来，在 ActorInput 中，检查玩家是否按下空格键且 mLaserCooldown 小于或等于零。如果两个条件都满足，你就创建激光，将其位置和旋转设置为飞船的位置和旋转（这样它从飞船出发并朝向飞船面向的方向），并将 mLaserCooldown 设置为 0.5f：

单击此处查看代码图片

```
void Ship::ActorInput(const uint8_t* keyState)
{
    if (keyState[SDL_SCANCODE_SPACE] && mLaserCooldown <= 0.0f)
    {
        // Create a laser and set its position/rotation
        Laser* laser = new Laser(GetGame());
        laser->SetPosition(GetPosition());
        laser->SetRotation(GetRotation());

        // Reset laser cooldown (half second)
        mLaserCooldown = 0.5f;
    }
}
```

然后，重写 UpdateActor 以按 delta time 递减 mLaserCooldown：

单击此处查看代码图片

```
void Ship::UpdateActor(float deltaTime)
{
    mLaserCooldown -= deltaTime;
}
```

这样一来，mLaserCooldown 会跟踪玩家再次发射前剩余的时间。并且因为 ActorInput 在计时器未结束时不会创建激光，你确保玩家不能比期望更频繁地发射。有了激光发射，你就可以使用之前介绍的碰撞代码来射击并摧毁小行星了（参见图 3.15）。

![](img/e9afcec1487716b0ef80d7e7c09869c8_224_0.png)

### 图 3.15 向小行星发射激光

你可以在 `Laser` 中使用类似的 float 变量，强制激光在一秒后死亡（并从游戏世界中删除），即使激光没有与小行星碰撞。

## 总结

向量表示大小和方向。你可以使用向量进行许多不同的计算，包括在两点之间创建向量（使用减法）、计算两点之间的距离（使用减法和长度）、求两个向量之间的夹角（使用点积）以及计算表面的法线（使用叉积）。

对于基本移动，本章展示了如何创建一个 `MoveComponent`，允许角色向前移动并旋转。对于前向移动，你将角色的前向向量乘以移动速度和 delta time。将此结果加到角色的当前位置，即可得到时间步长后角色的新位置。在本章中，你还学习了如何在角色和组件中添加可重写的输入行为支持，以及如何利用此功能创建一个继承自 `MoveComponent` 的 `InputComponent`。

在牛顿物理中，物体的加速度等于作用于物体上的力除以物体的质量。你可以使用欧拉积分来计算变化量

