
// 每一帧渲染时调用一次

```csharp
void Update ()
{
    if (launched)
    {
        float dist = Vector2.Distance(transform.position, lastPointPosition);
        if (dist >= pointDistance)
        {
            // 是时候添加新点了
            AddPathPoint();
        }
    }
}
```

```csharp
void ProjectileLaunched ()
{
    // 弹药刚刚发射，所以删除之前的轨迹
    for (int i = 0; i < pathParent.childCount; i++)
    {
        Destroy(pathParent.GetChild(i).gameObject);
    }
}
```

```csharp
AddPathPoint();
// 因为弹药已发射，更新变量值
launched = true;
}
```

```csharp
// 在路径上添加一个新点
void AddPathPoint ()
{
```

```csharp
// 使用模板创建一个新点
GameObject newPoint = (GameObject) Instantiate(pathPointPrefab);
// 将点放置在当前弹药位置
newPoint.transform.position = transform.position;
// 将父对象设置为该点
newPoint.transform.parent = pathParent;
// 存储添加点的位置
lastPointPosition = transform.position;
```

该小程序使用我们刚刚创建的模板来沿路径绘制点，因此我们需要通过 `pathPointPrefab` 变量来定义此模板。然后，通过 `pointDistance` 变量，我们可以调整连续点之间的所需距离。接下来，我们需要对 Path 进行一个引用，这是一个我们必须作为根对象添加到场景层级（hierarchy）中的空对象。该对象将是所有轨迹点的父对象，并帮助我们一次性访问它们，以便在绘制新路径时删除它们（正如我们很快将看到的）。由于我们在弹药移动以绘制路径时计算每两个连续点之间的距离，因此我们始终必须保留上一个绘制点的位置。该位置存储在 `lastPointPosition` 变量中。最后，我们知道路径应该在弹药发射后才绘制，因此我们使用 `launched` 变量来判断是否已发射。

记住，当弹药发射时，Project 程序会发送 `ProjectileLaunched` 消息，PathDrawer 通过同名函数接收该消息。一旦之前绘制的路径（如果有）通过删除空对象的所有子对象被删除（我们通过 `pathParent` 变量保留该对象的引用），删除完成后，我们通过调用 `AddPathPoint()` 函数在发射位置绘制一个点，然后将 `launched` 值改为 `true`。

`AddPathPoint()` 函数的作用是创建一个新点。

```csharp
public void DoSpecialAttack ()
{
    // 获取原始弹体的当前速度
    Rigidbody2D myRB = GetComponent<Rigidbody2D>();
    float originalVelocity = myRB.velocity.magnitude;
    // 将所有碎片的碰撞组件存储在此数组中
    Collider2D [] colliders = new Collider2D[clusterCount];
    Collider2D myCollider = GetComponent<Collider2D>();
    for (int i = 0; i < clusterCount; i ++)
    {
        // 创建一个新碎片
        GameObject cluster = (GameObject) Instantiate(clusterPrefab);
        // 设置碎片对象的位置、名称和父级
        cluster.transform.parent = transform.parent;
        cluster.name = name + "_cluster_" + i;
        cluster.transform.position = transform.position;
        // 将当前位置的碎片碰撞组件存储在数组中
        colliders [i] = cluster.GetComponent<Collider2D>();
        // 忽略此碎片与之前创建的碎片之间可能发生的碰撞
        // 忽略碎片与原始物体之间可能发生的碰撞
        Physics2D.IgnoreCollision(colliders [i], myCollider);
        for (int a = 0; a < i; a ++)
        {
            Physics2D.IgnoreCollision(colliders [i], colliders [a]);
        }
    }
    Vector2 clusterVelocity;
    // 随着每个新碎片的产生，减少水平方向的速度
    // 并增加垂直方向的速度，以确保碎片化
    clusterVelocity.x = (originalVelocity / clusterCount) * (clusterCount - i);
    clusterVelocity.y = (originalVelocity / clusterCount) * -i;
    // 为新碎片添加刚体
    Rigidbody2D clusterRB = cluster.GetComponent<Rigidbody2D>();
    clusterRB.velocity = clusterVelocity;
    // 选择碎片块使其等于原始物体的质量
    clusterRB.mass = myRB.mass;
    // 在碎片寿命结束后销毁碎片
    Destroy(cluster, clusterLife);
    }
    // 最后销毁原始弹体对象
    Destroy (gameObject);
}
```

执行这种攻击的想法是接收 `DoSpecialAttack` 消息，然后使用指定的模板创建指定数量的碎片。为了防止碎片之间相互碰撞，以及碎片与原始弹体之间的碰撞（在它们从场景中删除的前一刻可能会发生碰撞），我们使用了 `Physics2D.IgnoreCollision()` 函数，并为其提供了我们想要忽略之间碰撞的两个碰撞组件。注意，我们维护了一个碰撞组件矩阵来存储所有碎片的组件，当创建新碎片时，我们将之前碎片的碰撞组件传递过去，并在旧组件和新组件之间调用上述函数以消除碰撞。下一步是碎片的运动速度，我们获取了原始弹体的速度值，并每次乘以一个不同的值，以获得新速度的水平分量和垂直分量。这两个分量随碎片的改变而变化：第一个碎片从高水平速度和低垂直速度开始，然后随着垂直值向下逐渐增加而水平值减少，这些值开始变化，导致弹体以类似于图中所示的方式散开（我在图中增加了碎片数量以阐明这一概念）：

![](img/e263e4c2a46d978fb73216c778f3ec48_284_0.png)

注意，碎片会从原始弹体的分裂点散开。然后，我们调整每个碎片的质量，使其等于原始弹体的质量。虽然通过碎片数量除以质量来均匀分布是逻辑性的，但将所有碎片都拷贝原始质量将赋予它们更大的破坏力，从而赋予特殊攻击其优选的优势。

## 发射器行业

现在让我们转向发射器，这是一个会将这些弹体射向目标的弹弓。遗憾的是，我们的图形包不包含弹弓图像，因此我们将尝试使用一些木制和金属形状创建一个看起来像它的简单形状。在这里，我将使用三个木制矩形和一个石头三角形组成在图中看到的形状。这些物体必须放置在一个包含它们所有内容的空物体中，并且三角形 `Sprite Renderer` 组件中的 `Order in Layer` 值也必须调整并设置为 1，这样它就能像图片所示显示在碎片前面：

![](img/e263e4c2a46d978fb73216c778f3ec48_285_0.png)

除了我们已经缩放和旋转形成弹弓的四张图像外，还有 3 个指示其位置彩色线的空对象。这些空对象具有我们很快将看到的软件实用程序。`LaunchPos` 对象代表弹体在发射前放置的位置，而 `RightEnd` 和 `LeftEnd` 对象代表橡皮筋末端的位置，橡皮筋将在发射时推动弹体。目前形式的弹弓已准备好制作模组的初始版本，我们将为其添加一些插件和其他组件。

其中第一个是向目标发射弹体的主插件。让我们在接下来的叙述中了解这个名为 `Launcher` 的插件，然后讨论其功能的细节：

```csharp
using UnityEngine;
using System.Collections;

public class Launcher : MonoBehaviour
{
    // 发射器的发射力度系数
    public float launchForce = 1.0f;
    // 橡皮筋可以延伸的最大长度
    public float maxStretch = 1.0f;
    // 弹体在发射前放置的位置
    public Transform launchPosition;
    // 发射器上的碎片
    public Projectile currentProjectile;
    // 碎片是否都已消耗？
    private bool projectilesConsumed = false;
    // 启动时调用
    void Start ()
    {
    }
    // 每帧调用
    void Update ()
    {
        if (projectilesConsumed)
        {
            // 无事可做
            return;
        }
        if (currentProjectile != null)
        {
            // 如果碎片没有被发射也没有被玩家捕捉
            if (! currentProjectile.IsHeld () && currentProjectile.IsLaunched ())
            {
                // 将碎片带到发射位置
                BringCurrentProjectile();
            }
        }
    }
}
```

```csharp
BringCurrentProjectile();
}
else
{
  // 发射器上没有碎片
  // 找到最近的碎片并带到发射位置
  currentProjectile = GetNearestProjectile();
  if (currentProjectile == null)
  {
    // 所有碎片已消耗，向上发送消息
    projectilesConsumed = true;
    SendMessageUpwards("ProjectilesConsumed");
  }
}
```

```csharp
// 寻找最近的碎片并返回
Projectile GetNearestProjectile()
{
  Projectile [] allProjectiles = FindObjectsOfType<Projectile>();
  if (allProjectiles.Length == 0)
  {
    // 不再有碎片
    return null;
  }
  // 寻找最近的碎片并返回
  Projectile nearest = allProjectiles[0];
  float minDist = Vector2.Distance(nearest.transform.position, transform.position);
  for (int i = 1; i < allProjectiles.Length; i ++)
  {
    float dist = Vector2.Distance(allProjectiles [i].transform.position, transform.position);
    if (dist < minDist)
    {
        minDist = dist;
        nearest = allProjectiles [i];
    }
  }
  return nearest;
}

// 平滑地将当前碎片移动到发射位置
void BringCurrentProjectile ()
{
  // 弹体将在它们之间移动的位置
  Vector2 projectilePos = currentProjectile.transform.position;
  Vector2 launcherPos = launchPosition.transform.position;
  if (projectilePos == launcherPos)
  {
    // 实际上已经在发射处了，不需要移动它
    return;
  }
  // 使用帧之间经过时间的线性插值来实现平滑移动
  projectilePos = Vector2.Lerp (projectilePos, launcherPos, Time.deltaTime * 5.0f);
  // 将碎片放在它的新位置
  currentProjectile.transform.position = projectilePos;
  if (Vector2.Distance(launcherPos, projectilePos) < 0.1f)
  {
    // 弹物变得非常近，将其直接放在发射点
    currentProjectile.transform.position = launcherPos;
    currentProjectile.AllowControl();
  }
}
```

```csharp
// 持有当前弹物
public void HoldProjectile()
{
    if (currentProjectile != null)
    {
        currentProjectile.Hold();
    }
}
```

```csharp
// 将当前弹物拖到新位置
public void DragProjectile (Vector2 newPosition)
{
    if (currentProjectile != null)
    {
        // 确保不会超过最大弹性绳的张力
        float currentDist = Vector2.Distance(newPosition, launchPosition.position);
        if (currentDist > maxStretch)
        {
            // 将提供的位置更改允许的最远点
            float lerpAmount = maxStretch / currentDist;
            newPosition = Vector2.Lerp(launchPosition.position, newPosition, lerpAmount);
        }
    }
    // 将弹物放置在新位置
    currentProjectile.Drag(newPosition);
}

// 如果玩家正持有弹物，则释放并发射它
public void ReleaseProjectile()
{
    if (currentProjectile != null)
    {
        currentProjectile.Launch(launchForce);
    }
}
```
