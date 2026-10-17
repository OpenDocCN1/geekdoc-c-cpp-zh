
### 游戏控制器

在游戏中，总有一些功能无法具体分配给某个游戏对象，但它们与整个游戏或至少与当前场景有关。一个很好的例子是暂停菜单或背景音乐。此类组件通常被分配到一个名为“Game Controller”的 GameObject 上。“游戏控制器”是游戏中典型的组件，这就是为什么 Unity 默认已经提供了一个“Game Controller”标签，以便更快速地识别它们。由于我们的游戏也需要一个“Game Controller”，现在就创建一个名为“Game Controller”的新游戏对象。首先，你向它传输一个 `AudioSource`，并激活 `Play On Awake` 和 `Loop`。现在将“backgroundMusic”文件分配给 `AudioClip` 属性，并将音量暂时设置为 0.3，稍后你可以根据喜好进行调整。为了让背景音乐在任何地方的音量都相同且始终均匀分布在两个声器上，我们在“backgroundMusic”的导入设置中取消勾选 `3D Sound` 参数。

### 创建玩家

接下来，让我们来处理玩家。由于内容较大，我想将其分为三个部分。首先，我们将为玩家配备它的主要组件。然后，我们将开发生命管理系统，这对我们未来的对手来说也很重要。最后，我们才会处理实际的玩家控制和攻击。

1. 首先，我们在场景中添加一个新的空游戏对象并将其命名为“Player”。为了以后通过代码更容易找到它，我们也给它赋予“Player”标签。Unity 默认提供了这个标签，所以我们不需要担心进一步创建此标签。
2. 现在，我们通过 `Component > Physics > Character Controller` 为“Player”添加一个字符控制器，稍后我们将使用单独的脚本控制它。将半径设置为 0.5，高度设为 1.5。
3. 然后，我们向该 GameObject 添加一个 `AudioSource`，通过它播放玩家所有的语音样本。你可以根据需要调整音量。确保 `Play On Awake` 和 `Loop` 处于未勾选状态。
4. 现在，将“Main Camera”作为子对象添加到“Player”中，并使用 `Reset` 将其重置为默认值。为此，选择“Main Camera”，并在 Transform 上下文菜单中点击 `Reset`。然后将位置调整为 `position (0, 0.4, 0)`。
5. 现在创建另一个空游戏对象并将其命名为“SpawnPoint”。此对象稍后将用作投掷武器的位置。为了更好的视觉呈现，可以在 GameObject 的 Inspector 中为“SpawnPoint”设置自己的图标，例如黄色菱形。

### LifePointController

我们需要的变量是一个用于管理生命值的私有变量，以及一个用于访问 `UIText` 对象的公共变量，随后我们将 "LpText" 对象赋值给该变量。

```csharp
public UIText LpText;

private int lifePoints = 0;
```

由于我们将使用属性方法来访问 `lifePoints` 变量，因此该 `int` 变量被声明为私有。这样做是为了在赋值时，我们可以确保 `lifePoints` 的值永远不会小于 0。我们还希望确保在每次分配新值时 GUI 都会更新。为此，我们将再次实现一个执行此操作的 `UpdateView` 方法。

```csharp
public int LifePoints {
    get {
        return lifePoints;
    }
    set {
        lifePoints = value;
        if (lifePoints < 0) lifePoints = 0;
        UpdateView();
    }
}
```

在 `UpdateView` 方法中，将新的 `lifePoints` 值赋值给 GUI 对象。

```csharp
void UpdateView() {
    LpText.text = lifePoints.ToString();
}
```

现在我们要做的最后一件事是在场景开始时将当前的生命值数量赋值给控制器。我们将使用 `PlayerPrefs` 类和 "LPs" 参数来实现这一点。在游戏开始时，我们将在启动场景中保存带有初始值的 "LPs" 参数。如果带有 `LifePointController` 启动 "Dungeon" 场景，后者会将值加载到 `lifePoints` 变量中。

```csharp
void Awake() {
    LifePoints = PlayerPrefs.GetInt("LPs");
}
```

在场景结束时，脚本会再次将其当前值写回。这是通过 `OnDestroy` 方法实现的，该方法会在脚本被销毁时执行（即场景终止时）。

```csharp
void OnDestroy() {
    PlayerPrefs.SetInt("LPs", lifePoints);
}
```

如果场景因为玩家死亡而结束，那么写入 "LPs" 的值将比他开始时的值小。一旦玩家死亡，`PlayerHealth` 脚本中的 `lifePoints` 就会扣除一个生命值，我们稍后会编写该脚本。因此，当场景重启时，加载的值会减少。完整的 `LifePointController` 脚本可以在本节末尾找到。

### HealthController

现在我们进入玩家健康管理的实际部分。但由于我们的对手也有血量状态，我们现在想要使用继承性。我们将创建一个基类 `HealthController`，玩家和对手的脚本将基于该类创建。`HealthController` 类仅包含存储血量状态的公共变量 `health` 以及私有变量 `isDead`。

```csharp
public float health = 3;
private bool isDead = false;
```

该类还拥有 `ApplyDamage` 方法，它会对所有者造成伤害。在这里，`health` 根据伤害量进行减少，并调用一个名为 `Damaging` 的方法。然而，如果伤害导致 `health` 降至 0 甚至为负，则会调用 `Dying` 方法，并将变量 `isDead` 设置为 `true`。

```csharp
void ApplyDamage(float damage) {
    health -= damage;
    if (health <= 0 && !isDead) {
        isDead = true;
        Dying();
    } else {
        Damaging();
    }
}
```

由于玩家和对手的 `Damaging` 和 `Dying` 两个方法差异很大，它们仅被声明为可以重写的空方法。

```csharp
public virtual void Damaging() {
}

public virtual void Dying() {
}
```

### PlayerHealth

现在我们可以基于 `HealthController` 类创建 `PlayerHealth` 脚本了。该脚本也将有一个 `UpdateView` 方法，在该方法中，玩家的健康值将以图形方式显示。然而，在这种情况下，我们不想简单地显示一个数字，而是想以进度条的形式显示此值。对于这个条，我们使用已经创建的 "HealthBar" `UIText` 对象。最后，我们将该对象赋值给公共变量 `healthGui`。在 `UpdateView` 方法中，该图形对象的长度将根据健康值和指定的最大长度计算。

```csharp
void UpdateView() {
    if (healthGui != null) {
        guiRect.width = guiMaxWidth * health / maxHealth;
        healthGui.pixelInset = guiRect;
    }
}
```

注意列表中未声明的各种变量。这些是在类头部声明的公共和私有变量，并在 `Start` 方法中赋值。`guiRect` 在此处接收原始值，随后将其宽度传递给 `guiMaxWidth`。`maxHealth` 也从 `health` 的初始值获取值。除了这些，还有两个变量在 `Start` 中赋值。`lifePointController` 变量被赋值给游戏控制器的特定实例，`messageText` 变量被赋值标记为 "Message" 的对象的 `UIText` 组件，我们在上面进一步创建了它。最后，在 `Start` 方法中再次调用 `UpdateView`，以便在 GUI 中显示正确的条长度。

```csharp
public AudioClip hurtClip;
public AudioClip deathClip;
public UIText healthGui;
private LifePointController lifePointController;
private float maxHealth;
private UIText messageText;
private Rect guiRect;
private float guiMaxWidth;

void Start() {
    messageText = GameObject.FindGameObjectWithTag("Message").GetComponent<UIText>();
    lifePointController = GameObject.FindGameObjectWithTag("GameController").GetComponent<LifePointController>();
    guiRect = new Rect(healthGui.pixelInset);
    guiMaxWidth = guiRect.width;
    maxHealth = health;
    UpdateView();
}
```

#### PlayerHealth.cs 完整代码

玩家血值的实际管理由 `PlayerHealth` 脚本完成，它继承自 `HealthController` 类。将其直接添加到玩家上。然后，将 "hit" 和 "death" 音频片段赋值给两个 `AudioClip` 变量 `hurtClip` 和 `deathClip`。

```csharp
using UnityEngine;
using System.Collections;

public class PlayerHealth : HealthController {
    public AudioClip hurtClip;
    public AudioClip deathClip;
    public UIText healthGui;
    private LifePointController lifePointController;
    private float maxHealth;
    private UIText messageText;
    private Rect guiRect;
    private float guiMaxWidth;

    void Start() {
        messageText = GameObject.FindGameObjectWithTag("Message").GetComponent<UIText>();
        lifePointController = GameObject.FindGameObjectWithTag("GameController").GetComponent<LifePointController>();
        guiRect = new Rect(healthGui.pixelInset);
        guiMaxWidth = guiRect.width;
        maxHealth = health;
        UpdateView();
    }

    public override void Damaging() {
        audio.clip = hurtClip;
        audio.Play();
        UpdateView();
    }

    public override void Dying() {
        audio.clip = deathClip;
        audio.Play();
        UpdateView();
        lifePointController.LifePoints -= 1;
        if (lifePointController.LifePoints > 0)
            Invoke("Restart", 1);
        else
            messageText.text = "Game Over";
    }

    void Restart() {
        Application.LoadLevel(Application.loadedLevel);
    }

    void UpdateView() {
        if (healthGui != null) {
            guiRect.width = guiMaxWidth * health / maxHealth;
            healthGui.pixelInset = guiRect;
        }
    }
}
```
