
CheckInput() 首先计算一个用于工作的比例。浮点数 scalerX 和 scalerY 分别保存屏幕宽度和高度的百分之一对应的值。

```
// calculate and use deltas
float mouseDeltaY = Input.mousePosition.y - prevMousePos.y;
float mouseDeltaX = Input.mousePosition.x - prevMousePos.x;
```

代码中通过获取当前鼠标位置，并减去鼠标在上一次更新结束时的位置，来计算鼠标移动的增量。

```
// scale based on screen size
vert += ( mouseDeltaY * speedY ) * scalerY;
horz += ( mouseDeltaX * speedX ) * scalerX;
// store this mouse position for the next time we're here
prevMousePos= Input.mousePosition;
```

当鼠标位置乘以缩放变量（scalerX 和 scalerY）时，我们得到一个百分比数值。我们表示鼠标在屏幕上的百分比位置，并将该百分比作为输入。

```
// set up some Boolean values for up, down, left and right
Up = ( vert>0 );
Down = ( vert<0 );
Left = ( horz<0 );
Right = ( horz>0 );
```

如果需要，基于鼠标的输入脚本还会填充上述用于方向移动的布尔变量。

```
// get fire / action buttons
Fire1= Input.GetButton( "Fire1" );
}
```

为了使开火按钮正常工作，必须在 Unity 编辑器的输入设置中，在 Fire1 条目下正确设置鼠标按钮输入。

```
public void LateUpdate()
{
    // check inputs each LateUpdate() ready for the next tick
    CheckInput();
}
```

脚本从 LateUpdate() 调用自己的更新函数，Unity 建议所有输入检查都在这里进行。

> 注意：要正确设置输入，请打开 Unity 的输入菜单：编辑 > 项目设置 > Input

## 5.6 关卡加载

本书中有两种加载系统。一种使用 Unity 的 SceneManager 直接加载场景。高级关卡加载在本书中有独立章节，你可以在第 13 章中找到。

## 5.7 ScriptableObjects

ScriptableObject 是管理需要在整个游戏中持久化的数据的好方法。框架中只有一个脚本，即 ProfileScriptableObject。

### 5.7.1 ProfileScriptableObject

保存和加载将在第 12 章完整介绍。对于存档，本框架使用一个 ScriptableObject 来存储我们想要在档案中保存的所有内容。这个脚本需要被序列化，因此要注意不要使用引擎可能难以序列化的任何变量类型。它构成了存档的基础。你可以在 Assets/GPC_Framework/Scripts/COMMON 文件夹中找到这个脚本。

ProfileScriptableObject.cs 脚本如下所示：

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using System;

namespace GPC
{
    [CreateAssetMenu(fileName = "ProfileData", menuName = "CSharpFramework/ProfileScriptableObject")]
    [Serializable]
    public class ProfileScriptableObject : ScriptableObject
    {
        public Profiles theProfileData;
    }

    [Serializable]
    public class Profiles
    {
        public ProfileData[] profiles;
    }

    [Serializable]
    public class ProfileData
    {
        [SerializeField]
        public int myID;
        [SerializeField]
        public bool inUse;
        [SerializeField]
        public string profileName = "EMPTY";
        [SerializeField]
        public string playerName = "Anonymous";
        [SerializeField]
        public int highScore;
        [SerializeField]
        public float sfxVolume;
        [SerializeField]
        public float musicVolume;
    }
}
```

## 5.8 生成

在许多情况下，使用 Unity 内置的 Instantiate 函数来为基于桌面电脑的游戏创建对象已经足够了，但在 Unity 中实例化 GameObject 可能是一个开销很大的过程，在移动设备上尤其明显。一种常见的绕过处理器开销的方法是使用对象池。对象池是指你拥有一组对象，可以重复使用而无需销毁它们。构建对象池管理系统超出了本书的范围，不过集中生成系统将使将来更容易切换为更好的解决方案。

在 Assets/GPC_Framework/Scripts/COMMON/SPAWNING 文件夹中可以找到这些脚本。

### 5.8.1 生成器组件

这个 Spawner 类可以在场景开始后经过一段时间后实例化预制体，或者当摄像机与生成点之间的距离达到一定值时实例化预制体，或者当另一个脚本调用它来生成时实例化预制体。在本书中，它用于示例游戏 Blaster，其中每一波敌人都存储在一个单独的场景中。敌方预制体在场景加载完成后自动生成，玩家就可以开始射击它们了。

```
using UnityEngine;

namespace GPC
{
    [AddComponentMenu("SharpBookCode/Common/Spawn Prefabs (no path following)")]

    public class Spawner : ExtendedCustomMonoBehaviour
    {
        // should we start spawning based on distance from the camera?
        // if distanceBased is false, we will need to call this class from elsewhere, to spawn
        public bool distanceBasedSpawnStart;

        // if we're using distance based spawning, at what distance should we start?
        public float distanceFromCameraToSpawnAt = 35f;
        public bool shouldAutoStartSpawningOnLoad;
        public float timeBetweenSpawns = 1;
        public bool startDelay;
        public int totalAmountToSpawn = 10;
        public bool shouldRepeatWaves;
        public bool shouldRandomizeSpawnTime;
        public float minimumSpawnTimeGap = 0.5f;
        public GameObject[] _spawnObjectPrefabs;
        private int totalSpawnObjects;
        private int spawnCounter = 0;
        private int currentObjectNum;
        private Transform _cameraTransform;
        public bool shouldSetSpeed;
        public float speedToSet;
        public bool shouldSetSmoothing;
        public float smoothingToSet;
        public bool shouldSetRotateSpeed;
        public float rotateToSet;
```

上面唯一需要注意的变量声明是生成对象存储在一个数组中。这意味着你可以添加多种类型的预制体来进行生成。

```
void Start()
{
    // cache ref to our Transform
    _TR = transform;
    if(_cameraTransform==null)
        _cameraTransform = Camera.main.transform;
}
```

上面，我们缓存了 Transform；如果尚未在 Inspector 中设置，我们会尝试使用 Unity 内置的 Camera.main 查找场景中主摄像机的 Transform。

```
if (shouldAutoStartSpawningOnLoad)
    StartSpawn();
```

我们查看生成列表数组中有多少个对象，并将结果存储在一个名为 totalSpawnObjects 的变量中。这样只是为了更方便。

```
public void OnDrawGizmos()
{
    if (distanceBasedSpawnStart)
    {
        Gizmos.color = new Color(0, 0, 1, 0.5f);
        Gizmos.DrawSphere(transform.position, distanceFromCameraToSpawnAt);
    }
    else
    {
        Gizmos.color = new Color(0, 1, 1f);
        Gizmos.DrawSphere(transform.position, 1f);
    }
}
```

Gizmo 是一种形状，可以用来为你的组件或游戏对象提供视觉辅助——比如立方体或球体——它会显示在编辑器的场景视图中。得益于这段代码，每当该组件附加到游戏对象上时，Unity 都会在其周围绘制一个 Gizmo，以显示我们的生成器将在多远的距离激活。绘制发生在上面的 OnDrawGizmos() 函数中，游戏引擎会在游戏运行时和空闲时自动调用该函数。

上面，我们检查名为 distanceBasedSpawnStart 的布尔变量，以确定是否使用基于距离的生成。如果为 true，我们根据生成距离绘制球体。如果 distanceBasedSpawnStart 为 false，我们仅使用固定半径绘制球体。这样，我们总是有一个 Gizmo，可以更轻松地看到生成将发生在哪里。

要设置即将绘制的 Gizmo 的颜色，你可以调用 Gizmos.color()，并传入红、绿、蓝参数，后跟一个 alpha 值。所有值都应在 0 到 1 之间。一旦你在函数中调用了 Gizmos.color()，之后绘制的任何内容都会使用该颜色，直到你再次调用 Gizmos.Color() 为止。

绘制球体 Gizmo 非常简单，只需调用 Gizmos.DrawSphere()，并传入要绘制的位置以及球体的半径。上面，我们取 Transform 的位置，在第一个实例中，我们传入
