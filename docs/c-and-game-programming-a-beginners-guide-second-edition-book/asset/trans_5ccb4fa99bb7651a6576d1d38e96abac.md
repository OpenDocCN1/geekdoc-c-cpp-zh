

## C# 与游戏编程

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_196_0.png)

截图 3.13.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_196_1.png)

截图 3.14.

要添加适当的菜单项，只需双击该菜单（或子菜单）并键入相应的标题（见截图 3.15）。为便于参考，我将这些项标记为 1、2 和 3。你还应注意右侧可用的次要列表；单击此选项允许我们创建额外的子菜单（见截图 3.16）。

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_197_0.png)

截图 3.15.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_197_1.png)

截图 3.16.

现在，只需切换回我们项目的文本部分（Forms.cs）并注意其中的变化。这里我们会发现从基本引用到我们作为菜单项插入的名称的所有内容（见示例 3.32）。当然，如果我们想手动创建这些文件，只需手动输入这些引用即可。重要的是要记住列出每一项及其附带的索引点。

### 示例 3.32. 创建文本菜单。

```csharp
using System;
using System.Windows.Forms;

namespace Example32 {
    public class Form1 : System.Windows.Forms.Form {
        private System.Windows.Forms.MainMenu mainMenu1;
        private System.Windows.Forms.MenuItem menuItem1;
        private System.Windows.Forms.MenuItem menuItem2;
        private System.Windows.Forms.MenuItem menuItem3;
        private System.Windows.Forms.MenuItem menuItem4;

        public Form1() {
            InitializeComponent ();
        }

        #region Windows Form Designer generated code
        private void InitializeComponent() {
            this.mainMenu1 = new System.Windows.Forms.MainMenu ();
            this.menuItem1 = new System.Windows.Forms.MenuItem ();
            this.menuItem2 = new System.Windows.Forms.MenuItem ();
            this.menuItem3 = new System.Windows.Forms.MenuItem ();
            this.menuItem4 = new System.Windows.Forms.MenuItem ();

            this.mainMenu1.MenuItems.AddRange (
                new System.Windows.Forms.MenuItem [] {this.menuItem1});
            this.menuItem1.Index = 0;

            this.menuItem1.MenuItems.AddRange (
                new System.Windows.Forms.MenuItem [] {
                    this.menuItem2,
                    this.menuItem3,
                    this.menuItem4});
            this.menuItem1.Text = "Menu";

            this.menuItem2.Index = 0;
            this.menuItem2.Text = "One";
            this.menuItem3.Index = 1;
            this.menuItem3.Text = "Two";
            this.menuItem4.Index = 2;
            this.menuItem4.Text = "Three";

            this.ClientSize = new System.Drawing.Size (292, 266);
            this.Menu = this.mainMenu1;
            this.Name = "Form1";
            this.Text = "Form1";

        }
        #endregion

        [STAThread] static void Main() {
            Application.Run (new Form1());
        }
    }
}
```

从这里开始，我们需要将这些项链接到特定函数和/或一组函数，具体取决于我们使用这些项引用什么。在我们的关键示例——Paddle Tennis 游戏中，我们将使用这些点来引用游戏的起始点、双人、单人和演示版本选项（见示例 3.33–3.36）。

### 示例 3.33. 双人菜单选项。

```csharp
// Menu event handler
private void TwoPlayer_Click(object sender, System.EventArgs e) {
    gameState.currentMode = GameState.Mode.TwoPlayer;
    SetUp();
}
```

### 示例 3.34. 单人菜单选项。

```csharp
// Menu event handler
private void SinglePlayer_Click(object sender, System.EventArgs e) {
    gameState.currentMode = GameState.Mode.SinglePlayer;
    SetUp();
}
```

### 示例 3.35. 演示版本菜单选项。

```csharp
// Menu event handler
private void DemoVersion_Click(object sender, System.EventArgs e) {
    gameState.currentMode = GameState.Mode.DemoMode;
    SetUp();
}
```

### 示例 3.36. 由菜单选项调用的子函数。

```csharp
public void SetUp() {
    // (Re) set member variables.
    gameState.currentState = GameState.State.Started;
    gameState.currentSpeed = GameState.SPEED_DEFAULT;

    playerR.imagePosX = 595;
    playerR.imagePosY = 200;
    playerR.score = 0;
    playerL.imagePosX = 5;
    playerL.imagePosY = 200;
    playerL.score = 0;
    theBall.isActive = false;
    theBall.imagePosX = playerR.imagePosX;
    theBall.imagePosY = playerR.imagePosY;

    Cursor.Hide();

    Invalidate();
}
```

## 人工智能导论

人工智能（AI）最简单的形式，本质上是针对特定情境或条件集的人类反应的建模或模拟。这些反应可能基于模式或数学方程，例如追踪或规避，但初始反应通常是随机的基线运动。人工驱动的程序必须既包含人类局限性的现实表现，如犯错和/或偶尔的幸运一击的能力，同时也必须表现为一个非人格化的、始终如一的对手，能够一遍又一遍地重复相同的技能水平（至少直到我们厌倦并关闭它为止）。当然，我们这里讨论的 AI 只是对该主题的一个简要介绍，但不要被这些参考的简单性所迷惑——人工智能编程可能出人意料地引人深思、策略上棘手，并且值得花时间去掌握。首先，我们将关注完成此游戏所需的关键点：追踪和随机运动的模型。

### 追踪

追踪，顾名思义，是跟踪或跟随一个移动角色在预定区域内移动的能力。这由程序的独立部分（子例程）完成，它既可以实现位置变化，也可以将该信息发送给另一个子例程。用于追踪对象的代码类似于用于实现角色移动的代码。唯一区别在于它是由计算机的判断执行的，例如，当比较“说”被追踪对象更高或更低时，它能够调整自身位置。不幸的是，这种技术有一个缺点，即计算机不会犯错，这打破了人文现实主义的主要规则。幸运的是，我们可以通过添加随机事件来克服这种对完美的需求，因此有必要将这些技术协同应用。

### 随机运动

在最后两章中，我们多次使用随机数来创建新信息，并动态改变原本可预测行为的结果。在试图打破预期动作的单调性时，这个过程也非常有用，并且是我们人工角色使用的新输入的主要来源。使这个过程略有不同的一个关键转折是，我们将使用该随机输入来降低人工玩家追踪投射物的能力。这一策略背后的想法是增加错误水平，从而提高游戏的可玩性（见示例 3.37 和 3.38）。

### 示例 3.37. 网球 AI 左玩家。

```csharp
// Left player artificial intelligence
public void TennisAIPlayerL() {
    // if ball active move left player
    if(theBall.isActive == true) {
        switch(theBall.direction) {
            case 1:  // if ball is moving SW move south to meet
                if(theBall.imagePosY > playerL.imagePosY) {
                    playerL.direction = AnimatedImage.SOUTH;
                }
                break;

            case 4: // if ball is moving W playerL will line up to meet
            case 8:
                if(theBall.imagePosY < playerL.imagePosY) {
                    playerL.direction = AnimatedImage.NORTH; // move north
                } else if(theBall.imagePosY > playerL.imagePosY) {
                    playerL.direction = AnimatedImage.SOUTH; // move south
                }
                break;

            case 7: // if ball is moving NW move north to meet
                if(theBall.imagePosY < playerL.imagePosY) {
                    playerL.direction = AnimatedImage.NORTH;
                }
```

### 示例 3.38. 网球 AI 右玩家。

```csharp
// Right player artificial intelligence
public void TennisAIPlayerR() {
    // stops playerR from trying to hit the ball after it passes
    if(theBall.imagePosX > playerR.imagePosX+25){
        return;
    }
    
    switch(theBall.direction) {
        case 3: // ball moving southwest
            if(theBall.imagePosY > playerR.imagePosY) {
                if(theBall.imagePosY < this.Width/2)
                    // move SW to spike
                    playerR.direction = AnimatedImage.SOUTHWEST;
                else
                    // move south to line up with ball
                    playerR.direction = AnimatedImage.SOUTH;
            } else
                // move back to give playerR more time
                playerR.direction = AnimatedImage.EAST;
            break;
```

