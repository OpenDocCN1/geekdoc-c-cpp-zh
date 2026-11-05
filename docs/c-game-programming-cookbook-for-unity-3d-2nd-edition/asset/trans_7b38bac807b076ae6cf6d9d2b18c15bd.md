
```
private void Awake()
{
    // reset all of the user data we have stored in the ScriptableObject
    gameObject.SendMessage("ResetAllPlayerStats");
}

public void Start()
{
    SetTargetState(Game.State.loaded);
}

public override void UpdateTargetState()
{
    switch (targetGameState)
    {
        case Game.State.loaded:
            Loaded();
            break;

        case Game.State.gameStarting:
            StartGame();
            break;

        case Game.State.gameStarted:
            // fire the game started event
            OnGameStarted.Invoke();
            SetTargetState(Game.State.gamePlaying);
            break;

        case Game.State.gamePlaying:
            break;

        case Game.State.gameEnding:
            EndGame();
            break;

        case Game.State.gameEnded:
            OnGameEnded.Invoke();
            break;
    }
}

public override void Loaded()
{
    base.Loaded();

    // set high score
    _uiManager.SetHighScore(GetComponent<BaseProfileManager>().GetHighScore());
    // reset score
    _RunManCharacter.SetScore(0);

    SetTargetState(Game.State.gameStarting);
}

void StartGame()
{
    runSpeed = 0;

    // add a little delay to the start of the game, for people to prepare to run
    Invoke("StartRunning", 2f);
}

void StartRunning()
{
    isRunning = true;
    runSpeed = 1f;
    distanceCounter = 1f;

    SetTargetState(Game.State.gameStarted);

    // start animation
    _RunManCharacter.StartRunAnimation();

    InvokeRepeating("AddScore", 0.5f, 0.5f);
}

void EndGame()
{
    // stop running
    isRunning = false;
    runSpeed = 0;

    // schedule return to main menu in 4 seconds
    Invoke("ReturnToMenu", 4f);

    // stop the repeating invoke that awards score
    CancelInvoke("AddScore");

    // let's try to store the high score (profile manager takes care of checking if it's a high score or not, we just submit a score)
    if (GetComponent<BaseProfileManager>().SetHighScore(_RunManCharacter.GetScore()) == true)
        _uiManager.ShowGotHighScore();

    // update final score ui
    _uiManager.SetFinalScore(_RunManCharacter.GetScore());

    // update target state
    SetTargetState(Game.State.gameEnded);
}

void AddScore()
{
    _RunManCharacter.AddScore(1);
}

void ReturnToMenu()
{
    SceneManager.LoadScene("runMan_menu");
}

public void PlayerFell()
{
    SetTargetState(Game.State.gameEnding);
}

void SpawnPlatform()
{
    runSpeed += 0.02f;
    distanceCounter = 0;
    float randomY = Random.Range(playAreaTopY, playAreaBottomY);
    Vector2 startPos = new Vector2(platformStartX, randomY);
    Instantiate(_platformPrefab, startPos, Quaternion.identity);
    distanceCounter = Random.Range(-0.5f, 0.25f);
}

void Update()
{
    if (isRunning)
    {
        distanceCounter += (runSpeed * Time.deltaTime);

        // check to see if we need to spawn another platform (based on distance travelled)
        if ((distanceCounter >= distanceToSpawnPlatform))
            SpawnPlatform();

        _uiManager.SetScore(_RunManCharacter.GetScore());
    }
}
```

现在试玩游戏。开始时应出现准备就绪的提示信息，一旦游戏开始，分数和高分将被显示。当 RunMan 从屏幕上掉落时，你还应看到一个漂亮的游戏结束提示，并显示最终分数！

唯一的问题是结束游戏时会报错，例如“Scene ‘runMan_menu’ couldn’t be loaded because it has not been added to the build settings or the AssetBundle has not been loaded”——这是因为 Unity 找不到主菜单，所以接下来让我们修复这个问题。

### 2.9.1 主菜单设置

在 Project 面板中，双击 Scenes 文件夹。双击 runMan_menu 场景以打开它。为节省时间，该场景已几乎准备就绪。它基于 GPC_Framework/TemplateScenes 文件夹中的 MenuTemplate 场景，该模板提供了一个基本模板，可帮助你快速构建菜单场景。要完成菜单设置，我们需要通过将其添加到 Build Settings 来告诉 Unity 菜单场景的位置。

点击编辑器左上角的 File 菜单，然后选择 Build Settings。打开 Build Settings 后，从 Project 面板中点击并拖拽 runMan_menu，将其拖放到 Build Settings 的 Scenes In Build 区域（图 2.19）。完成后关闭 Build Settings 窗口。

你刚刚复制过来的菜单模板场景已包含主菜单所需的一切，但我们仍需要告诉它游戏的位置，以便在玩家点击开始按钮时加载游戏场景。

在 Hierarchy 中找到并点击 MenuManager GameObject 以突出显示它。在 Inspector 中，找到 Menu With Profiles 组件。在 Game Scene Name 字段中输入 runMan_core（区分大小写！）。

按 CTRL+S 保存场景（或使用 File/Save 菜单），然后在工具栏中点击 Play 试玩游戏。菜单应该会出现。

点击 Start Game 按钮开始游戏。主游戏应加载、运行，并在游戏结束后返回主菜单。

![](img/e4b578cd512539e7261e070d87b6550a_64_0.png)

图 2.19 Unity 的 Build Settings 面板。

## 3 构建核心游戏框架

本章将介绍核心框架中设计决策的背景，并为理解各个代码示例如何协同工作以及为何有时会依赖其他组件提供良好的基础。

本书的框架（如图 3.1 所示）包含六个主要区域：

- **游戏管理器**：游戏管理器充当游戏中所有部分的中央通信脚本，并监督游戏状态。
- **玩家**：玩家可能已存在于游戏场景中，也可能由游戏管理器实例化。玩家结构将在本书第 4 章后面进行探讨。
- **AI 和敌人**：与玩家一样，AI 控制的角色或敌人可能在加载时已存在于场景中，也可能在运行时创建。我们将在第 10 章全面介绍 AI。
- **UI 管理器**：UI 管理器绘制所有主要游戏内用户界面元素，例如分数显示和生命值。我们将在第 11 章介绍 UI。
- **音效管理器**：音效管理器处理声音播放。声音内容在第 9 章。

![](img/e4b578cd512539e7261e070d87b6550a_68_0.png)

图 3.1 游戏框架图。

为了最大化灵活性，基类需要能够适应不同的配置。例如，玩家控制器应允许输入从另一个脚本传入，以便控制系统可以轻松更换，例如使用手柄与键盘控制。玩家脚本不需要知道输入来自何处，但需要提供一个供输入脚本通信的通用接口。正如使用通用接口与玩家控制器通信一样，玩家控制器也不应关心输入来自何处。

### 3.1 控制器与管理器

在本書中，我使用两个术语来指定主要类的类型；它们是 Controllers 和 Managers。

### 3.1.1 管理器

在本書中，Managers 用于表示专门管理对象或数据的脚本（以与公司经理管理员工类似的方式处理玩家、音频或其他游戏元素）。例如，可以有一个 GlobalRaceManager 类，用于跟踪并获取附加到赛车上的 RaceController 脚本组件集合的信息。管理器脚本使用来自 RaceController 组件的信息来计算玩家的比赛位置，并向玩家告知游戏的当前运行状态，管理整体比赛逻辑。

### 3.1.2 控制器

Controllers 专注于特定任务，例如帮助脚本相互通信、保存游戏特定的玩家信息或处理会话数据。例如，本书中的玩家有一个玩家控制器脚本。敌人有一个敌人控制器。Controllers 可以独立于其他脚本，也可以由管理器脚本管理，这取决于它们需要做什么。

### 3.2 核心框架脚本

Scripts/BASE 文件夹中有多个脚本，旨在作为模板或作为你在自己的游戏中派生的类。在本书的这一部分，我们将查看构成主框架的脚本。
