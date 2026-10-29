# Tutorial: Talking to the MAXScript interpreter

This tutorial gives you a little experience in working with the MAXScript Listener window and a chance to try some basic MAXScript commands.

To start using MAXScript, follow these steps:

+   1. Choose File↩ Reset to reset Max.
+   2. Choose MAXScript↩ MAXScript Listener (or press F11) to open the MAXScript Listener window.
+   3. Click anywhere in the bottom pane of the Listener window, type the following, and press Enter:
+      sphere()
+      A sphere object with default parameters is created.
+   4. Next enter the following in the lower pane, and press the Enter key:
+      torus radius1:50 radius2:5
+      Max creates a torus and adds it to your scene. As you specified in your MAXScript, the outer radius (radius1) is 50, and the radius of the torus itself (radius2) is 5. The output tells you that Max created a new torus at the origin of the coordinate system and gave that torus a name: Torus01.
+   5. Now use MAXScript to move the torus. In the Listener window, type the following:
+      $Torus01.position.x = 20
+      After you press Enter, you see the torus move along the positive X-axis. Each object in Max has certain properties or attributes that describe it, and what you've done is access one of these properties programmatically instead of by using the rollout or the mouse. In this case, you're telling Max, "Torus01 has a position property. Set the X-coordinate of that position to 20."

# Note

The $ symbol identifies a named object. You can use it to refer to any named object.

+   6. To see a list of some of the properties specific to a torus, type the following:
+      Showproperties $Torus01
+      A list of the Torus01 properties appears in the window.

Figure 49.5 shows the MAXScript Listener window with all the associated commands and results.

An important thing to understand from this tutorial is that you can do almost anything with MAXScript. Any property of any object that you can access via a rollout is also available via MAXScript. You could go so far as to create entire scenes using just MAXScript, although the real power comes from using MAXScript to do things for you automatically.

# Tip

Max remembers the value of the last MAXScript command that it executed, and you can access that value through a special variable: ? (question mark). For example, if you type 5 + 5 in the Listener window, Max displays the result, 10. You can then use that result in your next MAXScript command by using the question mark variable. For example, you could type $Torus01.radius2 = ?, and Max would internally substitute the question mark with the number 10.

At the left end of the status bar, you can access the MAXScript Mini Listener control by dragging the left edge of the status bar to the right. By right-clicking in this control, you can open a Listener window and view all the current commands recorded by the Listener. Figure 49.6 shows this control with another command along with the objects from the last example.