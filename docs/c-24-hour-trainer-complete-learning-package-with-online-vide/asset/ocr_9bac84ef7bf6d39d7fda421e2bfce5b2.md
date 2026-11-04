# 20

# Reusing Code with Methods

Sometimes a program needs to perform the same action in several places. For example, consider the UFO shooting gallery game you wrote for Exercise 19-12 and shown in Figure 20-1.

![](bbox=[0.18, 0.49, 0.48, 0.68])

FIGURE 20-1

When a laser bolt hits a UFO, the program takes these steps:

+   1. Plays the "hit a UFO" sound effect.
+   2. Increases the player's score and shows it in the score `Label`.
+   3. Hides the laser bolt `PictureBox`.
+   4. Sets `BoltIsAway = false` to remember that no laser bolt is currently on the form.
+   5. If that was the player's last laser bolt:
+      a. Plays the "game over" sound effect.
+      b. Displays the "game over" label showing the player's final score.
+      c. Disables the `Timer`.
+      d. If the player's score is greater than the smallest high score: