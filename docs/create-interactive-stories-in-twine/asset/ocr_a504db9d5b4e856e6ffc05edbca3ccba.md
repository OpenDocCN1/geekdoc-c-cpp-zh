# # Saving and Loading Games

15–20 minutes

# ## Activity Overview

By now, you probably have a pretty great game in the works, with twists and turns and a few horrible endings for careless players. Maybe your game is a tough one, and you want to give your players the ability to save their games rather than having to start all the way back from the beginning. Twine will let you do that!

# ## Instructions

This–the last activity!–will show you how to set your Twine story up so that players can save and load a game. Twine will use your browser to save a player's progress. There are two components to making this happen. The first bit of code will create a link titled Save Game that, when clicked, will save the current state of the game in Slot A. This includes which passages have been visited and any variables that were set.

```
(link:"Save Game")[(if:(save-game:"Slot A")][Game saved!])
```

It will also give a "Game Saved!" message to let the player know the game was saved. This code will only keep one active save. If the player saves the game a second time, it will overwrite the last save. The second bit of code is to load the last saved game.

```
(link:"Load Game")[(load-game:"Slot A")]
```

The code creates a link titled Load Game that, when clicked, will load the last game saved in Slot A. You can change the name