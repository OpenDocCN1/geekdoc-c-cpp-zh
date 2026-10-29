# Note

Max lets you use shorthand when adjusting the values of variables. Instead of saying a = a + b, you can just say a += b. Both have the same effect.

# Part 3: Animating the second fish

This scene actually has two fish in it (the other one has been sitting patiently off to the side), so for the final part of this tutorial, you get both fish involved in the animation. To animate the second fish alongside the first one, follow these steps:

+   1. At the top of the script, change these three lines (changes are in bold):
+   ```
+   pathObj = $Dummy01
+   fishObj = $Fish2/FishBody
+   fishTail = $Fish2/FishBody/FishTail
+   relPos = [50,75,0]  -- How close the fish is to the path
+   ```

+   2. Choose Tools» Evaluate All (or press Ctrl+E) to run the script again, and then animate it. Figure 49.17 shows both fish swimming merrily.

This script generates keyframes for the second fish because you changed the fishObj and fishTail variables to refer to the second fish. You've also moved the second fish's relative position so that the two don't run into each other.

# FIGURE 49.17

Both fish swimming together

![](bbox=[0.025, 0.69, 0.8, 0.92])