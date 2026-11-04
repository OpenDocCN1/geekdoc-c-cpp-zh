# Space Fighters: Putting It All Together

Again, a managing subprogram is necessary to weave these components into the game.
Here, I’ve ported the final product to the book’s CD-ROM. (Note that Chapter 3 includes
four versions of this game, e.g., Forms, GDI+, GDI+ with DirectX, and pure DirectX. See
Example 3.74/SpaceFighter on the CD-ROM for details.)

# Game 3—Asteroid Miner

We can also construct a third game that relies mainly on what we’ve already developed.
Asteroid Miner includes the goal of destroying asteroids rather than an enemy’s vessel.
Here we’ll also want to review the techniques used to create a rendered version of the game
(see Example 3.75).

![](bbox=[0.143, 0.4, 0.433, 0.457])

# Example 3.75. Brainstorming Asteroid Miner.

+   1. The game should have one player (a spaceship), which starts in the center of the screen.
+   2. The game starts the moment it’s loaded.
+   3. The player’s movement should be two-dimensional in respect to the screen, but it should include diagonal movement.
+   4. The ship should have a thrust, but not a brake or reverse, allowing momentum to carry it forward.
+   5. The ship will have weapons, or at least one weapon, namely a missile that can be fired at the asteroids. To keep things simple, the missiles won’t be able to injure other player.
+   6. We’ll use a black background with stars randomly placed across it.
+   7. The ship should make sounds including a thrust, weapon’s fire, and an explosion when hit. The Asteroids should also make a sound when they are hit.
+   8. The ship should not be able to fire when dead, with the asteroids able to pass through the exploding vessel without damage.