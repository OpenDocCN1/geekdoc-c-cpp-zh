![](bbox=[0.318, 0.031, 0.781, 0.456])

wheels, turn them, or operate extra vehicle-specific functions like a horn, headlights, etc. A human would require a code to drive a character controller. A spaceship might require use physics forces to drive a spaceship.

+   3. **Player manager.** This script is intended to be a bridge between the player controller and the user data manager. The user data manager takes care of storing player stats, such as score, lives, level, etc.

+   4. **Data manager.** The data manager takes care of the manipulation of player data and how the data are stored and retrieved. Score and health values would be stored here, and the data manager would also provide functions for saving and loading its data.

Along with these main components, we can add some extra components to mix and match player types into different forms. A weapon control script may be attached to a human to create the player in a first-person shooter, or the same weapon control script could be added to a vehicle-type player to turn it into a tank. An AI control script may be added to drive the player or to operate the weapons and so on.

In this chapter, we will be going through some of the main components that will be used later in the book to create a user-controlled player.