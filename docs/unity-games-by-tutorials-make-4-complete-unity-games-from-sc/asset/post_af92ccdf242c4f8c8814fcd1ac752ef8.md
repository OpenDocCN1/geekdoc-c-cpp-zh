
# Hooking up character animations

You've completed the Character Controller with regard to input, and will now complete the animation controller. This will allow you to extend the character controller to control animations! If you need to brush up on Unity’s animation, please review Chapter 6, "Animation."

Click the SoyBoy GameObject, then open the Animator window. Inside this window click the Parameters tab.

There are no parameters at the moment. You'll add these next.

In the Parameters area of the Animator window, click the + (plus) icon three times, each time adding one of the three parameters:

- Speed as a Float with value 0.0.
- IsJumping as a Bool, unchecked.
- OnWall as a Bool, unchecked.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_366_0.png)

Now create states. Start by defining a state change from the default Entry state to the IdleAnimation. Right-click the Entry state, select Make Transition and then click the IdleAnimation block.

An arrow is created from Entry pointing to IdleAnimation.

Now, you need to make the IdleAnimation the new default state (indicated by an orange block). Right-click IdleAnimation and click Set as Layer Default.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_366_1.png)

No condition is required to make this transition. It will happen as the game starts.

Now create a transition from IdleAnimation to RunAnimation, and again from RunAnimation back to IdleAnimation. You may want to drag the state blocks around in the window to position them better, too.

This is what you should now have:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_367_0.png)

Click the transition arrow pointing from IdleAnimation to RunAnimation. The Inspector window should show you the details of this transition.

Click the + (plus) icon under Conditions, and select the Speed parameter in the Condition drop-down. Ensure the check is set to Greater than 0. Uncheck the box for Has Exit Time. This makes sure the animation changes state as soon as the parameter metric is met.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_367_1.png)

Click the transition arrow pointing from RunAnimation to IdleAnimation.
Click the + (plus) icon under Conditions, select the Speed parameter in the Condition drop-down. This time you want to transition from running back to idle, so set the check Less than 0.05. When the player lets go of the horizontal movement controls, speed will go down to 0, and meet this condition.

Don't forget to uncheck the Has Exit Time check box, as you want this animation to exit as soon as it can when the condition is met.

Finish creating all the transition arrows, you'll need by setting up the transitions as per the image below:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_368_0.png)

On every transition you make, ensure you uncheck the **Has Exit Time** check box in the **Inspector** for that transition.

There are transitions to and from every state, except between **SlideAnimation** and **IdleAnimation** where there is only one state change from sliding to idle.

Click each transition arrow in the **Animator** editor and create conditions as specified in the tables below to complete the Animator Controller.

| Idle -> Jump | Jump -> Idle | Run -> Jump | Jump -> Run |
|---|---|---|---|
| IsJumping = true | Speed Less 0.05 | IsJumping = true | IsJumping = false |
| Speed Less 0.5 | IsJumping = false | | Speed Greater 0 |
| | IsOnWall = false | | |

| Run -> Slide | Slide -> Run | Slide -> Jump | Jump -> Slide | Slide -> Idle |
|---|---|---|---|---|
| IsOnWall = true | IsOnWall = false | IsJumping = true | IsOnWall = true | IsOnWall = false |
| Speed Greater 0 | IsOnWall = false | IsJumping = false | Speed Less 0.5 | |

Lastly, select the **RunAnimation** block, and change the speed for the animation to **2.5**.

Next, you'll change the player controller script to modify your new animation parameters. This will allow the animations to change based on the player's state.

Open **SoyBoyController.cs** in your code editor.

In the **Update()** method, use the **Input.GetAxis()** method calls (right near the top), add the following:

```c
animator.SetFloat("Speed", Mathf.Abs(input.x));
```

In the same Update() method, change the block of code that checks for input on the Y axis from:

```c
if (input.y >= 1f)
{
    jumpDuration += Time.deltaTime;
}\else{
    isJumping = false;
    jumpDuration = 0f;
}
```

to:

```c
if (input.y >= 1f) {
    jumpDuration += Time.deltaTime;
    animator.SetBool("IsJumping", true);
}else{
    isJumping = false;
    animator.SetBool("IsJumping", false);
    jumpDuration = 0f;
}
```

In the Update() method once more, just after the closing brace in the code that says:

```csharp
if (input.y > 0f)
{
    isJumping = true;
}
```

add the following:

```csharp
animator.SetBool("IsOnWall", false);
```

Move to the FixedUpdate() method next and replace this code block:

```csharp
if (IsWallToLeftOrRight && !PlayerIsOnGround)
{
    rb.velocity = new Vector2(-GetWallDirection()) * speed * 0.75f, rb.velocity.y);
}
```

With this:

```csharp
if (IsWallToLeftOrRight && !PlayerIsOnGround && input.y == 1)
{
    rb.velocity = new Vector2(-GetWallDirection()) * speed * 0.75f, rb.velocity.y);
    animator.SetBool("IsOnWall", false);
    animator.SetBool("IsJumping", true);
}
```

```csharp
else if (!IsWallToLeftOrRight())
{
    animator.SetBool("IsNotWall", false);
    animator.SetBool("IsJumping", true);
}
if (IsWallToLeftOrRight() && !PlayerIsOnGround())
{
    animator.SetBool("IsNotWall", true);
}
```

Save your changes and run the game, and use some basic controls. Super Soy Boy should transition between all the different states, including sliding down the wall when you're up against a wall and falling. Well done!

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_370_0.png)

# Building game hazards

No platform style game is complete without hazards that can hurt the player. In this section you'll be making a saw blade hazard that has the ability to chop Super Soy up into minced soy!

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_370_1.png)

Start by creating a new saw blade hazard. Name it Hazard. Drag the saw blade sprite from Sprites folder to the Scene.

Select the saw blade GameObject, click Add Component and choose the new C# Script. Open the Hazard script in your code editor. Add the following fields to the top of the class:

```csharp
public GameObject playerDeathPrefab;
public AudioClip deathClip;
public Sprite hitSprite;
private SpriteRenderer spriteRenderer;
```

Add the following, just above the Start() method:

```csharp
void Awake()
{
    spriteRenderer = GetComponent<SpriteRenderer>();
}
```

This caches a reference to the SpriteRenderer when the script starts. You will now implement the logic that occurs when the player touches the saw blade. Using the Unity physics 2D method:

```csharp
void OnCollision2D(Collision2D coll)
{
    // 1. First check the GameObject has the "Player" tag
    if (coll.transform.tag == "Player")
    {
        // 2. Next, determine if an AudioClip has been assigned to the script and that a valid Audio Source exists
        var audioSource = GetComponent<AudioSource>();
        if (audioSource != null && deathClip != null)
        {
            audioSource.PlayOneShot(deathClip);
        }

        // 3. Instantiate the playerDeathPrefab at the collision point
        Instantiate(playerDeathPrefab, coll.contacts[0].point, Quaternion.identity);

        // 4. Swap the sprite of the saw blade with the hitSprite
        spriteRenderer.sprite = hitSprite;

        // 5. Lastly, destroy the colliding object (the player)
        Destroy(coll.gameObject);
    }
}
```

Set the main Particle System properties up with the following changes:

-   Duration: 0.15
-   Looping: Unchecked
-   Start Lifetime: 2
-   Start Speed: Random between two constants 10 and 15
-   Start Size: 0.15
-   Start Rotation: Random between two constants 0 and 360
-   Gravity Modifier: 3

Enable the Emission section on the Particle System and set the Rate over Time to 300. Enable the Shape section, and set the Shape to Cone, Angle to 35, and Radius to

Create a new GameObject in the Scene. Name it DeathParticleSystem and add a Particle System component to it. Change the Transform component's X rotation to -90.

The last reference you need to make is for the Player Death Prefab on the Hazard script. This is for the particle effect that is instantiated when the player touches the hazard.

Save the script, and go back to Unity to take a look at the Hazard script on the Buzzsaw GameObject. Drag and drop the buzzsaw-hit sprite from Sprites folder to the Hit Sprite field in the Hazard script of your Buzzsaw GameObject. Do the same to your ssb_death audio clip from Sound folder to the Death Clip field.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_372_0.png)

# Unity Games by Tutorials Chapter 13: More Unity 2D
