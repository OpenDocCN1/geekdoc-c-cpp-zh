
In Start(), add the following:

```
arenaAnimator = GetComponent<Animator>();
sphereCollider = GetComponent<SphereCollider>();
```

You should be this by now; in here, you're getting access to the components.

There needs to be a chain of events to specify what happens after the marine steps onto the trigger.

You want the marine to ride the elevator to the ceiling. Animating the player is one approach that might work, but it's easier to make the marine child of the elevator. As it goes up, the marine has no choice but to follow. Additionally, the camera will try to follow, so you need to disable it.

Add the following:

```
void OnTriggerEnter(Collider other)
{
    Camera.main.transform.parent.gameObject.
    GetComponent<CameraMovement>().enabled = false;
    player.transform.parent = elevator.transform;
}
```

The first line gets the camera disables the movement. Then the player is made into a child of the platform.

You need to disable the player's ability to control the marine. Add the following to OnTriggerEnter():

```
player.GetComponent<PlayerController>().enabled = false;
```

This stops the player from turning, shooting or doing anything with the marine.

Now you need to add an audio cue to alert the player to the elevator's arrival. Add the following:

```
SoundManager.Instance.PlayOneShot(SoundManager.elevatorArrived);
```

You also need to kick off the animation, so add this line after the previous code you entered:

```
arenaAnimator.SetBool("OnElevator", true);
```

This will start the animation state and work when the player enters the sphere collider, but remember that the collider is disabled. It should be active when the platform arrives but not before. Save and switch to Unity.

Select BobbleArena in the Hierarchy. In the Inspector, drag the SpaceMarine to the player extendend. Expand the BobbleArena and look for a child GameObject named Elevator_Platform. Drag it to the Elevator property in BobbleArena.

You're down to the last step of calling your code. Frankly, animation events can do this. How cool is that?

## Animation events

An animation event is very much like a keyframe. You determine a point in the animation at to run the code, and then you assign it a method. This approach allows precision control over when the code runs.

> Note: Remember, you can animate all properties, including the collider you've enabled.

You imported the animations for summoning and rising in Chapter 1, "Hello, Unity," and just need to associate them with the Animator.

With BobbleArena selected in the Hierarchy, open the Animator window. You'll see the wall states you set up in Chapter 6, "Animation."

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_234_0.png)

You need a new state to summon the elevator, and it should be accessible from all the states because a win may occur at any time. You could create a transition from each state, but Unity has covered you with the "Any State"

In the Animator, right-click anywhere and select Create State ▸ Empty. Select New State, and name it ElevatorSummon in the Inspector. Set Motion to be the ElevatorSummon animation clip and Speed to 0.5 to slow the elevator to half its normal speed. As-is, it runs a little fast and stops before its audio clip ends. Slowing it down keeps the elevator in sync with its audio.

Create another empty state, call it ElevatorRise and assign the ElevatorRise animation clip to it.

The Animator should look like follows:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_235_0.png)

Create a transition from AnyState to ElevatorSummon and another from ElevatorSummon to ElevatorRise. It should look like the following:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_235_1.png)

Now you need a condition. Click the **parameters** tabs then + , choose **Trigger** and name it **PlayerWon.**

Select the transition from AnyState to ElevatorSummon. In the Inspector, add a condition and set it to **PlayerWon**. You don't have to set a value for the condition because it's a trigger.

Why use a trigger? By creating a transition from AnyState, then any state can reach the condition, including the destination of that transition.

If you were to use a Boolean condition like you did before, once you transition from AnyState to ElevatorSummon, the Animator would repeat the transition until the bool value switches to false. It would creates an infinite loop, but using a trigger means the transition only occurs once.

Next, create a new **Bool** parameter and name it **OnElevator.**

Select the transition between **ElevatorSummon** and **ElevatorRise**. In the Inspector, **uncheck Has Exit Time** and give it a new condition: **OnElevator** is equal to **true.**

## Open Arena in your code editor and add the following method:

```
public void ActivatePlatform()
{
    sphereCollider.enabled = true;
}
```

**Save** and switch back to Unity. Select **BobbleArena** in the Hierarchy and open the **Animation** window. From the animation drop-down, select **Elevator Summon**.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_236_0.png)

Over the last keyframe (which is at 0:28), **right-click** the gray bar above the frame counters and select **Add Animation Event**. You'll see a blue or white pip appear over that frame, and this is where you call your code. In the Inspector, select **ActivatePlatform()** from the drop-down:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_236_1.png)

All the public methods attached to the current GameObject show in this dialog. Remember, you just wrote ActivatePlatform to enable the sphere collider on top of the elevator once the winner has won the game, so you can detect when the player enters that area.

You're down to writing your last bit of code for **Bobblehead Wars!** Whoa! Open the **GameManager** in your code editor and add a public reference for the Arena Animator:

Add the following to initiate the game's end:

```
private void endGame()
{
    SoundManager.Instance.PlayOneShot(SoundManager.Instance.
elevatorArrived);
    arenaAnimator.SetTrigger("PlayerWon");
}
```

## Chapter 8: Finishing Touches

Unity kicks off the entire process and you just need to call it. In AlienDestroyed(), add the following before the closing brace:

```
if (totalAliens == 0)
{
    Invoke("endGame", 2.0f);
}
```

You've done a lot, here, so review how the entire end-game process works:

- 1. Once the count of aliens hits 0, you schedule the endGame() method to be called after two seconds.

- 2. This fires the "PlayerWon" trigger on the Arena Animator.

- 3. Once the Arena Animator detects this, it plays the elevator summon animation.

- 4. You configured the elevator summon animation to fire an animation event when the animation completes, to call the ActivatePlatform() method.

- 5. This enables a collider on the elevator.

- 6. When the player hits the collider, OnTriggerEnter() is called on the arena. This attaches the player to the elevator and sets the "OnElevator" Boolean on the Arena Animator.

- 7. This causes the Arena Animator to play the elevator's rise animation.

- 8. Pew! If you understand this sequence, pat yourself on the back — you've learned lot about Unity!

Save the code and head back to Unity. Select GameManager in the Hierarchy and drag the BobbleArena to the Arena Animator property.

Now for the final play test. Kill all the aliens and then step on the elevator. Victory is yours!

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_238_0.png)

## Where to go from here?

Congratulations on completing your first Unity Game! It's no small feat, but now you can see that building games is fun and probably easier than you thought when you decided to pick up this book.

In the process of finishing *Bobblehead Wars*, you learned some new concepts, including:

- UnityEvent and how to use it inside your code.
- Particle System and how it can make some cool effects.
- Animation Events and how they can be used to call code from your animation clips.

Believe it or not, you've barely explored Unity's capabilities and have a lot more to look forward to in this book.

In the next section, you'll put your skills to use to create a first-person shooter that features some rather angry robots. Pick up your gun and get blasting. You're in for a fun ride!
