Core framework classes in the BASE folder that will be covered in this chapter are:

+   - 3.2.1. BaseGameManager
+   - 3.2.2. ExtendedCustomMonoBehaviour
+   - 3.2.3. BaseCameraController

Other base scripts will be covered in specific parts of this book. For example, the scripts found in the GPC_Framework/BASE/PLAYER are covered in Chapter 4 when we look at the player structure.

# 3.2.1 BaseGameManager

The Game Manager is the core of gameplay, where overall game functions are described and dealt with and where current game state is held.

Core functions of the Game Manager are:

+   1. Tracking game state:
+      a. Storage of the game state
+      b. Providing functions for changing game state
+      c. Changing the game state based on calls to functions such as EndGame(), StartGame(), or PauseGame()
+   2. Creating player(s)
+   3. Camera set up and specifics such as telling the camera what to follow
+   4. Communicating between session manager, user manager, and game actions
+   5. Any communications between scripts that we would like to keep as standalone and not have to recode to talk directly to each other

Keeping track of game state is important, as some elements will need to change their behavior. If the game is paused, for example, we may want to suspend all input, freeze game time, and show a pop up. When the game ends, we will need to disable player input and so on. Tracking game states is the job of the Game Manager script.

A typical game may have several different core states, such as:

+   1. Game running
+   2. Game paused
+   3. Loading
+   4. Game ended

There may also be several custom states, such as a state for showing a cutscene or perhaps a state for playing a special audio clip. I recommend creating a new