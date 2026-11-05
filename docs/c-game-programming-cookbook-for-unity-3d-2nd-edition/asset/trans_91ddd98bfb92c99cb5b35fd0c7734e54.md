
4. 提供一个接口，允许其他脚本查询航点总数：由于我们的车辆各自保存自己的航点计数器编号，它们需要某种方式来确保计数器保持在实际存在的航点数量范围内。

In the racing game example in this book, we use waypoints for the AI and for the main player;

1. 检查主玩家是否朝向正确方向：车辆控制器代码将追踪玩家在赛道上的位置（基于已通过的航点）并检查其前向向量，以确保它面向赛道上的下一个航点。如果玩家的前向向量不在一定的容差角度范围内，游戏将显示错误方向消息并最终将车辆重新生成，使其面向正确方向。
2. 重新生成系统使用航点在赛道上找到一个“安全”的位置来重新生成玩家，同时使用其旋转使重新生成的车辆沿赛道面向正确方向。
3. 了解车辆在赛道上行驶了多远，这用于与其他玩家的进度进行比较以计算比赛位置

航点控制器脚本：

```
using UnityEngine;
using System.Collections.Generic;
namespace GPC
{
    [AddComponentMenu("CSharpBookCode/Utility/Waypoints Controller")]
    [ExecuteInEditMode]
    public class WaypointsController : MonoBehaviour
    {
        private List<Transform> _transforms;
        private Vector3 firstPoint; // store our first waypoint so we can loop the path
        private float distance;
        private int totalTransforms;
        private Vector3 diff;
        private float curDistance;
        private Transform closest;
        private Vector3 currentPos;
        private Vector3 lastPos;
        private Transform _pointT;

        public bool closed = true;
        public bool shouldReverse;

        void Start()
        {
            GetTransforms();
        }
    }
```

在上面的变量和类声明之后，Start() 函数调用了一个名为 GetTransforms() 的函数。我们将在函数后面详细查看它。

接下来是 OnDrawGizmos() 函数。如果你从未使用过 Gizmos，它们是用于使编辑和/或可视化更轻松的辅助对象。Unity 在编辑器中以及你如何与之交互方面非常依赖 Gizmos，同时也为你构建自己的自定义类型提供了一个良好的接口。

所有 Gizmo 绘制需要在以下两种函数之一中完成（由引擎自动调用）：

|  |  |
|---|---|
| OnDrawGizmos | 每一帧都被调用。所有 Gizmos 都可以被拾取。 |
| OnDrawGizmosSelected | 仅当附加了脚本的对象被选中时才调用。 |

OnDrawGizmos() 函数是一个运行时类（由游戏引擎自动调用），我们可以在其中绘制自己的 Gizmos 并进行一些基于编辑器的操作。在这种情况下，WaypointsController 的 OnDrawGizmos 函数将渲染航点位置并在每个航点之间绘制线条，以便我们对路径有一个简单的视觉表示。

```
void OnDrawGizmos()
{
    GetTransforms();
    if (totalTransforms < 2)
    {
        return;
    }
```

在函数的开始，我们调用 GetTransforms() 以确保关于构成我们路径的所有 Transforms 的存储信息是最新的（以防它们已被移动或添加了新对象）。

当你第一次构建路径时，显然它将从单个航点开始。只有一个点时，没有用于渲染线的终点，因此此函数检查是否有足够的航点来绘制线条，如果 totalTransforms 计数小于 2 则退出。

```
Transform _tempTR = (Transform) _transforms[0];
lastPos = _tempTR.position;
```

上面，我们从 _transforms List 中索引 0 处获取第一个航点 transform 并将其存储在 _tempTR 中。我们这样做是为了在编辑器中绘制表示路径的线条时有一个起点。

lastPos 将充当下一条线的起点，因此在此阶段我们只需要它有一个值：

```
firstPoint = _tempTR.position;
lastPos = firstPoint;
_pointT = (Transform)_transforms[0];

for (int i = 1; i < totalTransforms; i++)
{
    _tempTR = (Transform)_transforms[i];
    if (_tempTR == null)
    {
        GetTransforms();
        return;
    }

    // grab the current waypoint position
    currentPos = _tempTR.position;
```

如果所有 Gizmos、线条和编辑器辅助图形颜色相同，生活会更困难。出于这个原因，Unity 提供了 Gizmos.color 函数来设置它们的颜色。它只需要一次对 Gizmos.color 的调用（传入一个 Color 对象），之后的所有内容都将使用它进行渲染。

```
Gizmos.color = Color.green;
```

Gizmos.DrawSphere 在指定位置和半径处绘制一个球体，如下所示：

```
Gizmos.DrawSphere(currentPos, 2);
```

以及这个

```
// draw the line between the last waypoint and the current one
Gizmos.color = Color.red;
Gizmos.DrawLine(lastPos, currentPos);
```

Gizmos.DrawLine 是 Unity 提供的另一个实用工具，用于在两个 3d 向量之间绘制一条简单的线。Gizmo 绘制系统还有一些其他选项可用于使编辑更容易。

根据 Unity 文档，Gizmo 接口提供：

|  |  |
|---|---|
| DrawCube | 绘制一个以中心和大小为参数的实心盒子。 |
| DrawFrustum | 使用当前设置的 Gizmos.matrix 绘制摄像机视锥体以确定其位置和旋转。 |
| DrawGUITexture | 在场景中绘制纹理。 |
| DrawIcon | 在场景视图中的位置绘制图标。 |
| DrawLine | 绘制一条从 from 开始朝向 to 的线。 |
| DrawRay | 绘制一条从 from + direction 开始的光线。 |
| DrawSphere | 绘制一个以中心和半径为参数的实心球体。 |
| DrawWireCube | 绘制一个以中心和大小为参数的线框盒子。 |
| DrawWireSphere | 绘制一个以中心和半径为参数的线框球体。 |

如本章前面所述，航点在某个阶段用作可能卡住或离轨的车辆的重新生成点。它们的旋转也用于确保重新定位的车辆面向正确方向；出于这个原因，我们需要航点面向“前方”。为了确保我们的航点旋转正确，我们遍历并将每个航点向前指向下一个航点：

```
_pointT.LookAt(currentPos);
```

你可以通过使用 transform.LookAt() 函数轻松旋转 transform，使其前方向向另一个 transform。它接受一个或两个参数，第一个是要指向的 transform，第二个是可选的上向量。

请注意，在 OnDrawGizmos() 期间一直进行此功能会使拖放编辑变得困难，因为当你拖动航点时，对象枢轴会自动旋转。如果发现自动旋转点有问题，请注释掉上面的行。

随着函数的继续，我们继续遍历航点，然后如果布尔变量 closed 设置为 true，则关闭路径（你可以在编辑器中当 GameObject 附加此脚本时被选中时，在 Inspector 窗口中设置它）：

```
// update our 'last' waypoint to become this
// move on to find the next...
lastPos = currentPos;
// update the pointing transform
_pointT = (Transform)_transforms[i];
}
// close the path
if (closed)
{
    Gizmos.color = Color.red;
    Gizmos.DrawLine(currentPos, firstPoint);
}
}
public void GetTransforms()
{
    _transforms = new List<Transform>();
}
```

为了使航点控制脚本易于使用，我们需要在场景中以一种方式设置航点，以便我们想要使用它们。这种格式是一个空的 GameObject，附加了 WaypointsController.cs 组件，所有航点作为 Hierarchy 中的子对象。GetTransforms() 函数中找到的所有 Transforms 都像这样添加到名为 _transforms 的 List 中：

```
foreach(Transform t in transform)
{
    // add this transform to our arraylist
    _transforms.Add(t);
}

totalTransforms = (int)_transforms.Count;
```

在 GetTransforms() 的末尾，我们将 transforms 的总数存储在一个整数中以便以后轻松访问（这样我们就不必每次需要知道 List 中包含多少个 Transforms 时都去计数 List）。

类的其余部分由其他脚本可访问的公共实用函数组成：

|  |  |
|---|---|
| SetReverseMode | SetReverseMode 设置一个名为 shouldReverse 的布尔变量的值，该变量决定路径是否应被反转。 |
| FindNearestWaypoint | 找到给定位置在给定距离内的最近航点，并以整数形式返回其索引号。FindNearestWaypoint 有两种实现，其中一种添加了 exceptThis 的额外参数。该函数将像正常情况一样找到最近的航点，但当使用 exceptThis 时，它将忽略指定的 transform。 |
| GetWaypoint | 返回以整数形式传入的索引号处的航点的 transform。 |
| GetTotal | 返回一个整数值，表示该类控制的航点总数。 |

```
public void SetReverseMode(bool rev)
{
    shouldReverse = rev;
}

public int FindNearestWaypoint(Vector3 fromPos, float maxRange)
{
    if(_transforms == null)
        GetTransforms();
    distance = Mathf.Infinity;
    int tempIndex = 0;
```

为了找到 3D 向量 fromPos 的最近航点，变量 distance 最初设置为 Mathf.Infinity（计算机等价于无限大数字！）。我们使用
