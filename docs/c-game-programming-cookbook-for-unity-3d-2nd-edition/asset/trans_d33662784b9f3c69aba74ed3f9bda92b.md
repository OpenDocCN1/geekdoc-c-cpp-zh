

```csharp
}
}
```

在这个基类中，只有一个 `Jump()` 函数的虚版本。如果你需要在跳跃发生时做其他事情，应该由你自己的派生脚本重写它。例如，本书第 2 章中的 RunMan 无限跑酷游戏使用重写后的 `Jump()` 函数来告诉玩家精灵播放其跳跃动画。

## 7 武器系统

为了尽可能灵活，在本章中我们构建一个武器管理系统，用来控制各个武器控制器。这些武器控制器反过来将负责生成投射物，最后投射物将独立地自行处理。我们的武器管理系统应能只使用单把武器运行，或者我们应能够添加许多不同的武器并在它们之间切换。

武器控制器处理武器并向它们传递消息。它包含一个包含所有武器的数组，以及一个按需激活和停用它们的方法。

每把武器都是一个预制体，附加的脚本派生自 BaseWeaponScript.cs。除了在收到 `Fire()` 调用时应执行其应做的事情之外，武器应是自包含的。BaseWeaponScript 包含武器的基础内容（弹药、装填时间，以及可被禁用或启用的能力）。

### 7.1 构建脚本

对于武器系统，有两个主要的脚本组件，以及一个用于输入的组件：

- 1. BaseWeaponController
  这是我们的武器控制系统的框架。它提供系统所需的一切，并且旨在被重写以实现自定义。
- 2. BaseWeaponScript
  它负责处理各种单独的武器类型。如果你把 BaseWeaponController 看作玩家的手臂，那么 BaseWeaponScript 就是它所持武器的设计。
- 3. StandardSlotWeaponController
  该类提供一种接收玩家输入并更改当前所选武器的方法。

所有与武器相关的脚本都可以在文件夹 Assets\GPC_Framework\Scripts\BASE\WEAPON 中找到。

#### 7.1.1 BaseWeaponController 类

BaseWeaponController 类派生自 MonoBehaviour，以便使用 Unity 常用的内置调用：

```csharp
using UnityEngine;
using System.Collections.Generic;

namespace GPC
{
    [AddComponentMenu("CSharpBookCode/Base/Base Weapon Controller")]
    public class BaseWeaponController : MonoBehaviour
    {
        public GameObject[] _weapons;
        public int selectedWeaponSlot;
        public int lastSelectedWeaponSlot;
        public Transform _weaponMountPoint;
        private List<GameObject> _weaponSlots;
        private List<BaseWeaponScript> _weaponScripts;
        private BaseWeaponScript _tempWeapon;
        private int ownerNum;
        public bool useForceVectorDirection;
        public Vector3 forceVector;
        private Vector3 theDir;

        public void Start()
        {
            // default to the first weapon slot
            selectedWeaponSlot = 0;
            lastSelectedWeaponSlot = -1;
        }
    }
}
```

当前所选武器槽位和最后所选武器都设置了默认值。当 lastSelectedWeaponSlot 变量设置为 -1 时，它只是让武器系统知道需要设置武器（为了避免后续重复调用，每当设置武器槽位时，它都会检查以确保尝试设置的新武器与当前已设置的武器不同——因此在初始化时用 -1 使 selectedWeaponSlot 与 lastSelectedWeaponSlot 的值不同）。

```csharp
// initialize weapon list List
_weaponSlots = new List<GameObject>();
// initialize weapon scripts List
_weaponScripts = new List<BaseWeaponScript>();
_TR = transform;
if (_weaponMountPoint == null)
    _weaponMountPoint = _TR;
```

该脚本使用名为 _weaponSlots 的 List 来保存稍后在函数中生成的不同武器——这是一个包含所有可用武器的 List，即使未提供弹药也是如此——上面我们创建了一个新的空 List，准备填充。除了存储武器的 GameObject 之外，我们还将存储附加到每个武器上的 BaseWeaponScript 组件。我们的 Transform 存储在 _TR 中，如果未在 Unity 编辑器 Inspector 窗口中设置 _weaponMountPoint 变量，则会用 _TR 填充它。挂载点应是一个空 GameObject 或类似的 Transform，用于定位和设置武器的旋转。

```csharp
for (int i = 0; i < _weapons.Length; i++)
{
    GameObject _tempGO = (GameObject)Instantiate(_weapons[i], _weaponMountPoint.position, _weaponMountPoint.rotation);
    _tempGO.transform.parent = _weaponMountPoint;
    _tempGO.layer = _weaponMountPoint.gameObject.layer;
    _tempGO.transform.position = _weaponMountPoint.position;
    _tempGO.transform.rotation = _weaponMountPoint.rotation;
}
```

上面，我们遍历 _weapons 数组并逐个实例化每个武器。当游戏启动并且上面的 `Start()` 函数运行时，来自 _weapons List 的武器预制体引用将逐个实例化，并定位到武器挂载 Transform 的位置。为了让武器随玩家移动，我们将新武器的父级设置为武器挂载点（你只能设置 Transform 的父级，而不是 GameObject 的父级，因此使用 .transform.parent）。我们复制武器挂载点使用的层，并将新武器设置为同一层，然后再设置上面的位置和旋转。

```csharp
_weaponSlots.Add(_tempGO);
```

这些新对象将是脚本管理的对象，脚本会按需启用和禁用它们，并在需要时调用它们执行操作。每个新武器都会添加到一个名为 _weaponSlots 的新 List 中：

```csharp
// grab a reference to the weapon script attached to the weapon and store the reference in a List
_tempWeapon = _tempGO.GetComponent<BaseWeaponScript>();
_weaponScripts.Add(_tempWeapon);
```

这些槽位中每个武器上附加的 BaseWeaponScript 实例都会被找到（使用 GameObject.GetComponent()），并存储在另一个名为 _weaponScripts 的 List 中：

```csharp
// disable the weapon
_tempGO.SetActive(false);
```

武器需要一开始处于禁用状态，否则它们会全部重叠显示并且全部处于激活状态。这里使用 Unity 函数 GameObject.SetActive() 禁用它们：

```csharp
// now we set the default selected weapon to visible
SetWeaponSlot(0);
```

现在所有武器都已实例化、设置并隐藏，初始化所需的最后一件事是将默认武器槽位设置为第一个武器（索引为 0）。要设置槽位，请使用 `SetWeaponSlot()` 函数：

```csharp
public void SetOwner(int aNum)
{
    // used to identify the object firing, if required
    ownerNum = aNum;
}
```

当投射物击中敌人或玩家时，被击中的对象需要知道投射物来自哪里，以便知道如何对其作出反应。投射物识别可以通过层来完成。在枪挂载点对象（将成为武器父级的对象）上设置层，这个武器脚本将为其投射物使用相同的层。

另一种检查投射物来源的方法是为每个玩家分配唯一的 ID 编号，并使用 `SetOwner()` 函数告诉投射物每个投射物归谁所有。该 ID 编号会传递给投射物，并存储在投射物所附加的脚本中：

```csharp
public virtual void SetWeaponSlot(int slotNum)
{
    // if the selected weapon is already this one, drop out!
    if (slotNum == lastSelectedWeaponSlot)
        return;
}
```

函数 `SetWeaponSlot()` 接收一个整数作为索引号，用于引用存储在名为 _weaponSlots 的 List 中的武器。_weaponSlots List 的顺序将与在 Unity 编辑器 Inspector 窗口中添加到原始武器数组的武器顺序相同。

`SetWeaponSlot()` 函数一开始会确保我们尝试设置的武器（在 slotNum 中）不是已经激活的武器（lastSelectedWeaponSlot）：

```csharp
// disable the current weapon
DisableCurrentWeapon();
```

由于即将激活新武器，当前武器会通过调用 `DisableCurrentWeapon()` 函数被禁用：

```csharp
// set our current weapon to the one passed in
selectedWeaponSlot = slotNum;
```

selectedWeaponSlot 是用于存储当前激活武器槽位的索引。这里，它被设置为传入的参数值 slotNum：

```csharp
// make sure sensible values are getting passed in
if (selectedWeaponSlot < 0)
    selectedWeaponSlot = _weaponSlots.Count - 1;

// make sure that the weapon slot isn't higher than the total number of weapons in our list
if (selectedWeaponSlot > _weaponSlots.Count - 1)
    selectedWeaponSlot = _weaponSlots.Count - 1;
```

随后会验证 selectedWeaponSlot 的新值，以确保它不小于 0，也不大于已占用槽位的总数 -1（因为 _weaponSlots

