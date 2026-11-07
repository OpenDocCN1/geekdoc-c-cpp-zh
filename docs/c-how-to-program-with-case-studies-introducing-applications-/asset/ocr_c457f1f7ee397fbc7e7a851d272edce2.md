![](bbox=[0.25, 0.092, 0.75, 0.335])

The game has four types of visual components:

+   - a **cannon** that you control,
+   - a **cannonball**,
+   - **nine targets** that move up and down at various speeds, and
+   - a **blocker** that moves up and down, defending the targets.

The targets and the blocker move vertically at different but fixed speeds, reversing direction when they hit the screen's top or bottom.

To fire the cannon, you click the mouse. The cannon rotates toward the click point, fires a fast-moving cannonball in a straight line in that direction and plays a **boom sound**. Only one cannonball can be on the screen at a time.

Each time you destroy a target, a **target-destruction sound** plays, the target disappears, and the time remaining increases by a three-second time bonus. The blocker cannot be destroyed. When the cannonball hits the blocker, a **blocker-hit sound** plays, the cannonball bounces back, and the time remaining decreases by a two-second time penalty.

You win by destroying all nine target sections before the time expires. If the timer reaches zero, you lose. At the end of the game, the app displays whether you won or lost and shows the number of shots fired and the elapsed time. You may pause the game at any time by pressing the **P** key, and resume the game by pressing **P** again.

Compile and run the game and play it several times. Next, study this game's code and extensive comments. This application requires some trigonometry to:

+   - determine the cannon barrel's endpoint, based on its angle, and
+   - determine the cannonball's *x* and *y* increments used to move the cannonball in each animation frame—these also are based on the cannon's barrel angle.

**We provide the trigonometry calculations for you.**

Consider tweaking the code to see how your changes affect gameplay. For example, you could change how fast the cannonball moves. Finally, improve the game by implementing the enhancements we suggest in Exercise 10.27.