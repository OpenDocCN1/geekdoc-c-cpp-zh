that they contain calls to invoke UnityEvents that we will be using to hide and show the user interface. We will get to setting up the UnityEvents further in the user interface further in this chapter, Section 2.9.

Now that our RunMan_GameManager class has everything it needs to deal with updates to the target state, we need to add in some of those new functions called out in the code, like Loaded(), StartGame() and so on.

Beneath the code you just added (note: staying above the final curly bracket in that script), add this function

```
public override void Loaded()
{
    base.Loaded();
    // reset score
    _RunManCharacter.SetScore(0);
    SetTargetState(Game.State.gameStarting);
}
```

Above, Loaded() starts with a call to base.Loaded(), which tells Unity to run the original Loaded() function from the base class (BaseGameManager). Although here we are overriding that function, the original function still exists and we can still call it via base. This is useful when the base class has things in it that we don't want to replicate in an overridden function, but we still want to run. In this case, the base class only contains a call to invoke the UnityEvent OnLoaded. Again, we will get to the UnityEvents later in the chapter when dealing with user interface.

The next line resets our players score to zero at the start of the game:

```
_RunManCharacter.SetScore(0);
```

Finally, now that we have finished everything that needs doing when the game first loads, there is a call to SetTargetState to move on to the new state Game.State.gameStarting.

Next, we add the function that will be called when UpdateTargetState() receives a call to change the state to gameStarting (from above, at the end of the Loaded() function). Add this code below the Loaded() function:

```
void StartGame()
{
    runSpeed = 0;
    // add a little delay to the start of the game, for people to prepare to run
    Invoke("StartRunning", 2f);
}
```

Above, StartGame() sets the runSpeed to 0, so that RunMan does not start running right away. Remember when we added code to the platforms that used runSpeed from this Game Manager script? When the game starts, we hold everything in place – with runSpeed at 0, the platforms will not move.

Next, the StartGame() function schedules a call to a function named StartRunning() in 2 seconds, using Unity's built in scheduling function Invoke:

```
Invoke("StartRunning", 2f);
```

At this stage, after StartGame() has been called, the game sits in the Game. State.gameStarting state as we wait for the call to StartRunning to be made (by