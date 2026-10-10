
`Gizmos.color=Color.red;`

`Gizmos.DrawLine(currentPos, firstPoint);`

}

在讨论完 `GetTransforms()` 函数之后，该类的其余部分由公开的实用程序函数组成，供其他脚本访问：

| 方法 | 说明 |
| :--- | :--- |
| SetReverseMode | 设置名为 `shouldReverse` 的布尔变量的值，决定了路径是否应该反转。 |
| FindNearestWaypoint | 在给定距离内距离给定位置最近的路点，并以整数形式返回其索引。`FindNearestWaypoint` 函数有两种实现方式，其中一种增加了一个额外的参数 `exceptThis`。此函数将像常一样找到最近的路点，但 `exceptThis` 将忽略指定的 transform。 |
| GetWaypoint | 返回传入的索引号（作为整数）对应的路点的 transform。 |
| GetTotal | 返回一个整数值，代表该类控制的路点总数。 |

```csharp
public void SetReverseMode(bool rev)
{
    shouldReverse=rev;
}
public int FindNearestWaypoint(Vector3 fromPos, float maxRange)
{
    // make sure that we have populated the transforms
    // list, if not, populate it
    if (transforms==null)
        GetTransforms();
    // make sure that we have populated the transforms
    // list, if not, populate it
    if (transforms==null)
        GetTransforms();
}
```

```csharp
// the distance variable is just used to hold the
// 'current' distance when we are comparing, so that
// we can find the closest
distance = Mathf.Infinity;
```

为了找到距离 3D 向量 `fromPos` 最近的路点，变量 `distance` 初始为一个非常大的数字——`Mathf.Infinity`。我们在下面的迭代循环中使用它来比较距离：

```csharp
// Iterate through them and find the closest one
for(int i = 0; i < transforms.Count; i++)
{
    // grab a reference to a transform
    TEMPtrans = (Transform)transforms[i];
    // calculate the distance between the current
    // transform and the passed in transform's
    // position vector
    diff = (TEMPtrans.position - fromPos);
    curDistance = diff.sqrMagnitude;
    // now compare distances - making sure that
    // we are not
    if (curDistance < distance)
}
```

由于 `Mathf.Infinity` 也就是无穷大，因此这个条件至少会被满足一次。应该会有比无穷大更近的东西，这意味着只要有 transform 可以进行比较，无论它们在 3D 世界中有多远，我们都应该能获得某种返回结果。

```csharp
if( Mathf.Abs( TEMPtrans.position.y - fromPos.y ) < maxRange )
{
```

在某些情况下，返回很远的 transform 并不总是理想的结果，因此提供了 `maxRange` 来至少对所需的距离设置一个上限。

```csharp
// set our current 'winner'
// (closest transform) to the
// transform we just found
closest = TEMPtrans;
```

```csharp
// store the index of this
// waypoint
TEMPtransIndex=i;
```

```csharp
// set our 'winning' distance
// to the distance we just
// found
distance = curDistance;
```

![](img/041dca164b58875f4f1a64abb3328f5c_174_0.png)

### 7.1 路点系统 (Waypoint System)

加上 `maxRange` 之后，我们无法 100% 确定返回结果，因此在返回结果之前进行快速检查，确保 `closest` 中包含非零值：

```csharp
// now we make sure that we did actually find
// something, then return it
if (closest) {
    // return the waypoint we found in this test
    return currentIndex;
} else {
    // no waypoint was found, return -1 (this
    // should be accounted for at the other end!)
    return -1;
}
// this function has the addition of a check to avoid finding the
// same transform as the one passed in. We use this to make sure
// that we are looking for the nearest waypoint we don't find
// the same one as we just passed
```

同一个函数可能有两种不同的实现，每个实现都有自己的一组所需参数。在这里，`FindNearestWaypoint()` 的第二个版本与第一个版本几乎相同，不同之处是通过本节讨论讨论的 `exceptThis` 参数传入了一个新的 transform。

```csharp
public int FindNearestWaypoint(Vector3 fromPos , Transform exceptThis, float maxRange) {
    // make sure that we have populated the transforms
    // list, if not, populate it
    if (transforms==null)
        GetTransforms();
    // the distance variable is just used to hold the
    // 'current' distance when we are comparing, so that
    // we can find the closest
    distance = Mathf.Infinity;
    // Iterate through and find the closest closest one
    for(int i = 0; i < transforms.Count; i++) {
        // grab a reference to a transform
        TEMPTrans = (transforms[i]);
        // calculate the distance between the current
        // transform and the passed in transform's
        // position vector
        diff = (TEMPTrans.position - fromPos);
        curDistance = diff.magnitude;
        // now compare distances - making sure that
        // we are not
        if (curDistance < distance && TEMPTrans != exceptThis)
    }
}
```

```csharp
{
if(Mathf.Abs(TEMPTrans.position.y - fromPos.y) < maxRange) {
    // set our current 'winner'
    // (closest transform) to the
    // transform we just found
    closest = TEMPTrans;
    // store the index of this
    // waypoint
    TEMPIndex=i;
    // set our 'winning' distance
    // to the distance we just
    // found
    distance = curDistance;
    }
}
// now we make sure that we did actually find
// something, then return it
if(closest) {
    // return the waypoint we found in this test
    return currentIndex;
} else {
    // no waypoint was found, return -1 (this
    // should be accounted for at the other end!)
    return -1;
}
}
```

`GetWaypoint()` 返回传入索引号（作为整数）对应的路点的 transform。

```csharp
public Transform GetWaypoint(int index) {
    if(shouldReverse) {
```

这是类中唯一使用 `shouldReverse` 的地方。当 `shouldReverse` 为 true 时，`GetWaypoint` 将反转路点的索引（例如，使用 GetWaypoint 获取索引为零的路点将返回最后一个路点，而不是第一个）。为了反转传入此函数的索引，通过 transforms 的数量修改变量索引。

```csharp
// send back the reverse index'd waypoint
index=totalTransforms-index;
if(index<0)
    index=0;
}
```

显然，在尝试确保 transforms 已设置好之前，它不是为空。如果 transforms 为空，我们需要调用 `GetTransforms()` 来准备好一切：

```csharp
// make sure we populated the transforms list,
// not, populate it
if(transforms==null)
    GetTransforms();
```

如果请求的索引过高，它不会返回错误的路点，而是返回一个空值。调用端的代码可以检查空返回值并采取相应的措施：

```csharp
// first let's check to see if this index is higher than
// our waypoint count
// if so, we return null which needs to be handled on the
// other side
if(index>totalTransforms-1)
    return null;
```

现在一切都设置正确（transforms 列表包含路点，且索引在范围内），剩下的就是返回数组中的 transform：

```csharp
return (Transform) transforms[index];
```

路点控制器脚本的最后一部分是 `GetTotal()`，它被其他脚本用于发现有多少路点：

```csharp
public int GetTotal()
{
    return totalTransforms;
}
```

## 第 8 章：音频管理器

音频可以决定一个视频游戏的成败。良好的音频可以通过强化游戏世界的主题并将环境填充为生动且有噪音的地方，提供更深层次的沉浸感。相反，糟糕的音频会让玩家感到烦躁，并将良好的游戏体验变得重复且空虚。

大多数商业游戏有多个不同层的音频同时播放，并根据上下文进行切换或改变。为了达到商业级的音频效果，Unity 的音频系统需要大量的帮助。默认情况下，完成一些简单任务（如淡入淡出或控制音量水平）并不容易。为了实现即使基本的功能，都需要额外的音频管理。

本书中的音频代码为我们的框架提供了以下功能：

- 1. 为多个音频片段提供单一音频源
- 2. 能够从单个源管理音频片段
- 3. 能够播放、暂停或停止音频片段
- 4. 能够播放、暂停或停止从磁盘流的音乐
- 5. 提供音量控制功能以设置音量并使音乐淡入淡出
- 6. 通过静态单例实例提供可访问性，以便所有音频的调用都具有相同的格式

书中有两个脚本与音频的播放和管理有关。一个是用于音效的音频控制器 `BaseSoundController.cs`。另一个用于音乐控制的脚本 `MusicSoundController.cs`。

### 8.1 音频控制器

在本书的示例框架中，假设每个场景都有音频控制器，这是一个挂载了 `BaseSoundController.cs` 脚本的空游戏 GameObject。该组件有一个在 Unity 编辑器 Inspector 中填充的数组，包含了游戏所需的音频（它们的 AudioClips）。当另一个脚本需要某个声音时，它会调用音频管理器来播放，并传递 AudioClip 在数组中对应的索引：

```
BaseSoundController.Instance.PlaySoundByIndex( the index number from the array of sounds );
```

将音频播放集中化可以避免在多个地方处理属性，例如当用户在选项菜单中更改音量时，无需在每个 AudioSource 上设置音量水平。当音频在这里集中化时，一个音量设置和一个音量就可以轻松处理所有的游戏音频。

以下是完整的音频控制器脚本：

```cs
public class BaseSoundController : MonoBehaviour
{
    public static BaseSoundController Instance;
    public AudioClip[] GameSounds;
    private int totalSounds;
    private ArrayList soundObjectList;
    private SoundObject tempSoundObj;
    public float volume= 1;
    public string gamePrefsName = "DefaultGame"; // 在编辑器中忘记设置
                                                // 这个项！！
    public void Awake()
    {
        Instance = this;
    }
    public void Start()
    {
        // 当此脚本首次启动时，
        // 我们从 PlayerPrefs 中获取音量
        volume = PlayerPrefs.GetFloat(gamePrefsName+"_SFXVol");
        Debug.Log("BaseSoundController gets volume from prefs "+gamePrefsName+"_SFXVol at "+volume+"");
        soundObjectList=new ArrayList();
        // 为 GameSounds 数组中所有的声音创建声音对象
        foreach(AudioClip theSound in GameSounds)
        {
            tempSoundObj = new SoundObject(theSound,
                theSound.name, volume);
            soundObjectList.Add(tempSoundObj);
            totalSounds++;
        }
    }
    public void playSoundByIndex(int anIndexNumber, Vector3 aPosition)
    {
```
