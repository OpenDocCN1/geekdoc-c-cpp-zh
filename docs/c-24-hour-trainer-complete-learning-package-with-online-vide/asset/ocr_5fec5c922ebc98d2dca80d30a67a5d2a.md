Modify the program to make the following changes (which should make the program much smaller):

+   * Remove the X and O Labels so there's only one Label per square.
+   * Set each Label's Tag property to indicate its row and column. For example, set the Tag property for the upper-left Label to "0, 0."
+   * Make a class-level variable to keep track of which player's turn it is.
+   * Use the same Click event handler for all of the Labels.
+   * When the user clicks a square, convert the event handler's sender parameter into the Label that raised the Click event.
+   * If the square has already been taken, ignore the click.
+   * Otherwise, take the square for the player whose turn it is.
+   * Parse the clicked Label's Tag property to see which entry in the Board array to set. (Hint: Use ToString to convert the Tag property into a string.)

+   5. [Games] Copy the program you made for Exercise 4 and modify it so that when the last square is taken, the program says “All squares are taken” in the turn Label (instead of saying “O's turn”).

+   6. [Games, Hard] Copy the program you made for Exercise 5 and modify it so it checks for a winner after each square is taken. When the game ends, display the winner (or the fact that it's a tie) in the turn Label. After the game is over, ignore any click events until the user starts a new game.

+   7. [Games, Hard] Make a program that displays a bouncing ball (shown in a PictureBox). When the program starts, give the PictureBox a random position on the form and random X and Y velocities. When a Timer ticks, use the velocities to calculate the PictureBox's new position. If the position makes the PictureBox move beyond one of the form's edges, move it back onto the form and reverse the corresponding velocity.

+   8. [Games, Hard] Copy the program you made for Exercise 7 and add a sound effect by following these steps:
+      * In the Solution Explorer, double-click the Properties item. Select the References tab, open the Add Resource dropdown, and select Add Existing File. Select the sound effect's source file and click Open.
+      * Use class-level code similar to the following to create a sound player associated with the sound resource. (Here “boing” is the name of the resource I used.)
+        ```csharp
+        // The SoundPlayer.
+        private System.Media.SoundPlayer BoingSound =
+            new System.Media.SoundPlayer(Properties.Resources.boing);
+        ```
+      * Use the statement `BoingSound.Play()` to play the sound when necessary.