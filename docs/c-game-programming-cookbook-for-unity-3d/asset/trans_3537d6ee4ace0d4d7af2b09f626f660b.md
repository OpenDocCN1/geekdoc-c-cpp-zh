

```cs
// 现在我们确保是否真的找到了
// 某个东西，如果是，就返回它
if (closest) {
    // 返回我们在本次测试中找到的路点
    return TEMpIndex;
} else {
    // 没有找到路点，所以返回 -1（这
    // 应该在另一端进行处理！）
    return -1;
}

// 此函数增加了一个检查，以避免找到与传入
// 相同的变换（transform）。我们使用它来确保
// 当我们寻找最近的路点时，不会找到
// 我们刚刚经过的那个路点

public int FindNearestWaypoint(Vector3 fromPos, Transform
exceptThis, float maxRange)
{
    // 确保我们已经已经填充了 transforms 
    // 列表，如果没有，则进行填充
    if(transforms==null) {
        GetTransforms();
    }
    // distance 变量仅用于在比较时
    // 存储“当前”距离，这样我们 
    // 就能找到最近的距离
    distance = Mathf.Infinity;

    // 遍历它们并找到最近的一个
    for(int i = 0; i < transforms.Count; i++) {
        // 获取一个 transform 的引用
        TEMptrans = (Transform)transforms[i];

        // 计算当前
        // transform 与传入的 transform 的
        // 位置向量之间的距离
        diff = (TEMptrans.position - fromPos);
        curDistance = diff.sqrMagnitude;

        // 现在比较距离 - 确保
        // 我们不是
        if (curDistance < distance && TEMptrans !=
        exceptThis) {
            if (Math.Abs(TEMptrans.position.y -
            fromPos.y) < maxRange) {
                // 将我们当前的“获胜者”设置为
                // 我们刚刚找到的 transform
                closest = TEMpIndex;
            }
            // 存储此路点的
            // 索引
            TEMpIndex=i;
        }
    }
    // 将我们的“获胜”距离
    // 设置为刚刚
    // 找到的距离
    distance = curDistance;
}
}

// 现在我们确保是否真的找到了
// 某个东西，如果是，就返回它
if(closest) {
    // 返回我们在本次测试中找到的路点
    return TEMP;
} else {
    // 没有找到路点，所以返回 -1（这
    // 应该在另一端进行处理！）
    return -1;
}
}

public Transform GetWaypoint(int index) {
    if(shouldReverse) {
        // 返回反向索引的路点
        index=(transforms.Count-1)-index;
        if(index<0) {
            index=0;
        }
    }
    // 确保我们已经已经填充了 transforms 列表，
    // 如果没有，则进行填充
    if(transforms==null) {
        GetTransforms();
    }
    // 首先，检查此索引是否大于
    // 我们的路点计数
    // 如果是，则返回 null，这需要在另一
    // 端进行处理
    if(index>transforms.Count-1) {
        return null;
    }
    return (Transform)transforms[index];
}
public int getTotal() {
    return totalTransforms;
}
```

在变量声明后，`Start()` 函数调用了函数 `GetTransforms()`。

```cs
void Start()
{
    // 确保当此脚本启动时
    // 我们已经获取了每个路点的 transforms
    GetTransforms();
}
```

跳到脚本的后续部分，现在来看看 `GetTransforms()` 函数，以便清楚当类启动时会发生什么：

```cs
public void GetTransforms()
{
    // 我们将所有路点的 transforms 存储在一个数组中
    // 该数组在这里初始化（在我们可以使用 ArrayList 之前
    // 我们总是需要这样做）
transforms=new ArrayList();
```

为了让路点控制器脚本易于使用，我们需要确保在想要使用它们的场景中，路点是按照特定的方式设置的。这种格式是一个带有一个 `WaypointsController.cs` 组件的空 GameObject，路点作为子对象。控制器脚本期望在它下方找到所有路点。

```cs
foreach (Transform t in transforms)
{
    // 将此添加到 arraylist
    transforms.Add(t);
}

totalTransforms=(int)transforms.Count;
```

在 `GetTransforms()` 结束处，我们将路点的总数存储在一个整数中，以便于访问。

如果你从未处理过 gizmos，它们非常简单：

```cs
void DrawGizmos()
{
    // 确保当此脚本启动时
    // 我们已经获取了每个路点的 transforms
    GetTransforms();
}
```

```cs
void DrawGizmos()
{
    // 确保当此脚本启动时
    // 我们已经获取了每个路点的 transforms
    GetTransforms();
}
```

```cs
void OnDrawGizmosSelected()
{
    // 确保当此脚本启动时
    // 我们已经获取了每个路点的 transforms
    GetTransforms();
}
```

```cs
void OnDrawGizmosSelected()
{
    // 确保当此脚本启动时
    // 我们已经获取了每个路点的 transforms
    GetTransforms();
}
```

```cs
void OnDrawGizmos()
{
    // 确保当此脚本启动时
    // 我们已经获取了每个路点的 transforms
    GetTransforms();
}
```

```cs
void OnDrawGizmos()
{
    // 确保当此脚本启动时
    // 我们已经获取了每个路点的 transforms
    GetTransforms();
}
```

```cs
void OnDrawGizmos()
{
    // 确保当此脚本启动时
    // 我们已经获取了每个路点的 transforms
    GetTransforms();
}
```

```cs
void OnDrawGizmos()
{
    // 确保当此脚本启动时
    // 我们已经获取了每个路点的 transforms
    GetTransforms();
}
```

```cs
void OnDrawGizmos()
{
    // 确保当此脚本启动时
    // 我们已经获取了每个路点的 transforms
    GetTransforms();
}
```

```cs
void OnDrawGizmos()
{
    // 确保当此脚本启动时
    // 我们已经获取了每个路点的 transforms
    GetTransforms();
}
```

```cs
void OnDrawGizmos()
{
    // 确保当此脚本启动时
    // 我们已经获取了每个路点的 transforms
    GetTransforms();
    
```

```

void OnDrawGizmos()
{
    // 
当
脚本启动时
    // 我们已经获取了每个路点的


    Transforms





```
