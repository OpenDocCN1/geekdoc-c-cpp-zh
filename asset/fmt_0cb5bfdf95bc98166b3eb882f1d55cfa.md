
正如列表所示，我们需要引用之前编写的 `EnemySonar` 脚本、“Game Controller”（游戏控制器）的 `EPController` 脚本以及我们自己的动画组件。之后我们想要调用动画器中的“Hit”（击中）和“Die”（死亡）变量，因此我们将它们的哈希值保存在变量中。当然，击败对手还应该有经验值，这就是为什么我们仍然需要 `eps` 变量。最后，我们需要两个变量来处理对手在受伤时进入的受击状态。为此，我们需要一个 `isShocked` 布尔变量来保存该状态，以及一个供两个方法用于设置此持续时间的变量。

在下一步中，我们在基类 `HealthController` 中编写了 `Damaging` 和 `Dying` 方法。作为首次调用，我们在 `Damaging` 方法中设置触发器参数“Hit”，以便动画器控制器切换到“Hit”状态。此外，还应该播放你自己的音频源的声音，并将 `isShocked` 变量设置为 TRUE。当然，这应该在变量 `shockedTime` 指定的时间后重置。我们在一个单独的 `ResetShocked` 方法中执行此操作。

```csharp
public override void Damaging() {
    anim.SetTrigger(hitTrigger);
    audio.Play();
    isShocked = true;
    if (!enemySonar.playerDetected)
        enemySonar.StopSearching();
    Invoke("ResetShocked", shockedTime);
}
```

```csharp
void ResetShocked() {
    isShocked = false;
}
```

我们还希望玩家在伤害对手时立即被识别。这就是为什么如果还没有被检测到，我们还会从 `EnemySonar` 脚本调用 `StopSearching`。在 `Dying` 方法中，除了设置“Hit”触发器外，我们还将“Die”参数设置为 TRUE。我们在这里还播放了 AudioClip 并将 `isShocked` 设置为 TRUE。然而，我们现在调用的是 `DestroyMe` 方法而不是第二次延迟，它会销毁整个 GameObject 并将经验值分配给 `EPController`。

```csharp
public override void Dying() {
    anim.SetBool(dieBool, true);
    anim.SetTrigger(hitTrigger);
    audio.Play();
    isShocked = true;
    Invoke("DestroyMe", 1);
}
```

```csharp
void DestroyMe() {
    Destroy(gameObject);
    epController.AddPoints(eps);
}
```

现在也将此脚本分配给“Bat”（蝙蝠）预制体。实际上，就是这样。只需确保你在迷宫中放置足够的“Stone”（石头）物品，以便玩家之后可以杀死蝙蝠。

![](img/e263e4c2a46d978fb73216c778f3ec48_247_0.png)

如果你想选择如图 21.28 所示的结构，请注意预制体没有刚体。如果玩家首先移除了下方的石头，其他石头将留在空中。在这种情况下，你应该对场景中所有不在底部的“Stone”实例进行以下更改：

- 在场景中高亮这些 GameObject。
- 为这些对象添加刚体。
- 开启 X、Y 和 Z 的冻结旋转。

结果是石头金字塔保持直立，但一旦底部的石头被移除，上面的石头就会掉落。

### EnemyHealth.cs

以下 `EnemyHealth` 脚本管理敌人 NPC 的生命。由于它访问了之前的 `EnemySonar` 脚本，如果你想将此分配给 GameObject，则需要这两个脚本。

```csharp
using UnityEngine;
using System.Collections;

public class EnemyHealth : HealthController {
    public bool isShocked = false;
    public float shockedTime = 0.5F;
    private int eps = 1;
    private EnemySonar enemySonar;
    private EPController epController;
    private Animator anim;
    private int hitTrigger;
    private int dieBool;

    void Start() {
        enemySonar = GetComponent<EnemySonar>();
        epController = GameObject.FindWithTag("GameController").GetComponent<EPController>();
        hitTrigger = Animator.StringToHash("Hit");
        dieBool = Animator.StringToHash("Die");
        anim = GetComponent<Animator>();
    }

    public override void Damaging() {
        anim.SetTrigger(hitTrigger);
        audio.Play();
        isShocked = true;
        if (!enemySonar.playerDetected) {
            enemySonar.StopSearching();
        }
        Invoke("ResetShocked", shockedTime);
    }

    public override void Dying() {
        anim.SetBool(dieBool, true);
        anim.SetTrigger(hitTrigger);
        audio.Play();
        isShocked = true;
        Invoke("DestroyMe", 1);
    }

    void ResetShocked() {
        isShocked = false;
    }

    void DestroyMe() {
        Destroy(gameObject);
        epController.AddPoints(eps);
    }
}
```
