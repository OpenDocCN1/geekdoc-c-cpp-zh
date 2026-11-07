er than the hare, so you may want to toggle between the tortoise’s two images slower than between the hare’s two images. When the hare sleeps, stop toggling between its images.

+   e) When the tortoise and the hare are at the same position, display “OUCH!” for the turtle biting the hare and optionally play a high-pitched “OUCH!” audio clip.
+   
+   f) If the tortoise wins, display “Tortoise wins!” and optionally play a “Tortoise wins!” audio clip followed by cheering. If the hare wins, display “Hare wins” and optionally play a “Hare wins” audio clip followed by booing. If the race ends in a tie, you may want to favor the tortoise as the underdog or have the announcer say, “It’s a tie!”
+   
+   g) You could play crowd cheering and booing sounds and additional announcer commentary as appropriate throughout the race. You might be able to find public-domain crowd sounds online.

# Random-Number Simulation Case Study: High-Performance Card Shuffling and Dealing with Card Images and raylib

**10.23** *(Card Shuffling and Dealing with Card Images and Raylib)* In Section 10.7, you implemented a high-performance card-shuffling-and-dealing simulation using an array of Card objects. In this exercise, you’ll incorporate raylib capabilities into your simulation and use them to display attractive, free public-domain card images for each card in the deck. Once you complete this exercise, you’ll have the fundamental capabilities you need to begin implementing your favorite card games and to upgrade your solutions to the card-game exercises in earlier chapters.

You’ll load the unshuffled 52 card images as raylib Texture2D objects, then display them in a 4-by-13 grid:

![](bbox=[0.143, 0.621, 0.858, 0.912])