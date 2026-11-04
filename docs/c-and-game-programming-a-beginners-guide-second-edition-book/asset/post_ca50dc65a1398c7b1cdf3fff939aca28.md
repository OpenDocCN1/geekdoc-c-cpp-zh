
## C# and Game Programming

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_196_0.png)

Screen Shot 3.13.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_196_1.png)

Screen Shot 3.14.

To add the appropriate menu items, simply double click onto that menu (or submenu) and type in the appropriate headings (see Screen Shot 3.15). For reference, I've labeled those items 1, 2, and 3. You should also notice the secondary listing available to the right; clicking this option allows us to create additional submenus (see Screen Shot 3.16).

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_197_0.png)

Screen Shot 3.15.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_197_1.png)

Screen Shot 3.16.

Now, simply switch back to the text portion of our project (Forms.cs) and note the changes. Here we'll find everything from the basic references to the names we inserted as menu items (see example 3.32). Of course, if we wanted to create these files by hand, it would just be a question of inputting those references manually. It is important to remember to list each item, as well as their accompanying index points.

### Example 3.32. Creating a text menu.

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

From here, we'll want to link those items to a specific function and/or a set of functions, depending upon what we're using those items to reference. In our key example, the Paddle Tennis game, we'll use these points to reference the game's starting points, the two-player, single-player, and demo version options (see Examples 3.33–3.36).

### Example 3.33. Two-player menu option.

```csharp
// Menu event handler
private void TwoPlayer_Click(object sender, System.EventArgs e) {
    gameState.currentMode = GameState.Mode.TwoPlayer;
    SetUp();
}
```

### Example 3.34. Single-player menu option.

```csharp
// Menu event handler
private void SinglePlayer_Click(object sender, System.EventArgs e) {
    gameState.currentMode = GameState.Mode.SinglePlayer;
    SetUp();
}
```

### Example 3.35. Demo version menu option.

```csharp
// Menu event handler
private void DemoVersion_Click(object sender, System.EventArgs e) {
    gameState.currentMode = GameState.Mode.DemoMode;
    SetUp();
}
```

### Example 3.36. Subfunction called by the menu option.

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

## Introduction to Artificial Intelligence

Artificial Intelligence (AI), in its simplest form, is essentially the modeling or simulation of human responses that pertain to a certain situation or set of conditions. These responses might be based on patterns or mathematical equations such as tracking or evasion, but the initial reactions are usually random base movements. Artificially driven programs must include both a realistic representation of human limitation, like the ability to make errors and/or the occasional lucky shot, but it must also represent an impersonal, consistent opponent in its ability to repeat the same level of skill over and over (at least until we tire and shut it off). Of course, the AI we'll discuss here is only a minor introduction to that subject, but don't let the simplicity of these references fool you—programming for artificial intelligence can be surprisingly thought provoking, tactically tricky, and well worth the time it will take to master. To begin, we'll focus on the key points needed to complete this game: a model of tracking and random motion.

### Tracking

Tracking, as its name implies, is the ability to keep track of, or follow, a moving character as it travels across a predefined area. This is accomplished by an independent portion of programming, a subroutine, that can either implement position changes or send that information to a secondary subroutine. The coding used to track an object resembles the coding used to implement our characters' movements. The only difference is that it is implemented by the computer's judgment, for example, when a comparison "says" that the tracked object is higher or lower, allowing it to adjust its position. Unfortunately, this technique has one fault, which is that the computer cannot make mistakes, and that breaks the primary rule of humanistic realism. Luckily, we can overcome this need for perfection by adding in random events, hence the necessity of applying these techniques in unison.

### Random Motion

In the last two chapters, we've used random numbers several times to create new information and to dynamically change the results of otherwise predictable behaviors. This process is also very useful when attempting to break the monotony of projected movements and is the primary source of new input used by our artificial characters. The one key twist that makes this procedure a bit different is that we'll use that random input to reduce the artificial players' ability to seek the projectile. The idea behind this maneuver is to increase the level of error, and hence, the playability of the game (see Examples 3.37 and 3.38).

### Example 3.37. Tennis AI left player.

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

### Example 3.38. Tennis AI right player.

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
