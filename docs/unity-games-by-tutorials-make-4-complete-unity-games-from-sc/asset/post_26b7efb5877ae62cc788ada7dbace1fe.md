
# Unity Games by Tutorials

# Chapter 10: Adding Enemies

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_285_0.png)

Select the Inspector, and in the Project browser, select the Animations folder. Drag the Pickup Animator to the Inspector.

Once added, make sure to unlock the Inspector.

By adding this animation here, instead of the parent, the animation plays in local space.

Now, drag a copy of each Pickup[Type] onto the scene, lightly just above the ground:

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_285_1.png)

Click Play and move the player over each pickup; it should destroy itself when you make contact. You'll add a UI to show the effects of these pickups on screen, but for, if the pickup GameObjects are floating and spinning, disappearing when you walk into them, you've got it all right so far!

## More spawning logic

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_286_0.png)

Instead of having the robots and pickups exist in the scene at the start of the game, you'll have them spawn at specific locations.

Select all the Pickup[Type] GameObjects and [Color]Robot GameObjects in the Hierarchy and press Delete.

You will now code the pickups and robots to spawn at specific locations around the map.

Create a new C# script, name it PickupSpawn, and replace the contents of the class with the following:

```csharp
[SerializeField]
private GameObject[] pickups;
```

pickups will store all the possible pickup types.

Now add the following methods:

```csharp
// 1
void spawnPickup()
{
    // Instantiate a random pickup
    GameObject pickup = Instantiate(pickups[Random.Range(0, pickups.Length)]);
    pickup.transform.position = transform.position;
    pickup.transform.parent = transform;
}
```

```csharp
// 2
IEnumerator respawnPickup()
{
    yield return new WaitForSeconds(20);
    spawnPickup();
}
// 3
void Start() {
    spawnPickup();
}
// 4
public void PickupWasPickedUp() {
    StartCoroutine("respawnPickup");
}
```

Here's what each method does:

- 1. Instantiates a random pickup and sets its position to that of the PickupSpawn GameObject, which you will make in a moment.
- 2. Waits 20 seconds before calling spawnPickup().
- 3. Spawns a pickup as soon as the game begins.
- 4. Starts the coroutine to respawn when the player has picked up something.

Save your work. The Pickup script and add the following line just above Destroy(gameObject):

```csharp
GetComponentInParent<Pickup>().PickupWasPickedUp();
```

Now, when the pickup collides with the player, it will signal the PickupSpawn script to start the timer.

Save your work and switch back to Unity.

Create an empty GameObject, name it PickupSpawn and add the Pickup script.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_287_0.png)

# Unity Games by Tutorials

# Chapter 10: Adding Enemies

With the PickupSpawn GameObject selected, lock the PickupAmmoAssaultRifle, PickupAmmoPistol,

In the Resources folder, select the PickupAmmoAssaultRifle, PickupAmmoPistol, PickupAmmoShotgun, PickupHealth and PickupArmor prefabs and drag them to the Pickup properties to add them to the array.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_288_0.png)

Unlock the Inspector.

Now, drag the PickupSpawn GameObject into the Resources folder to create a prefab of it.

Create an empty GameObject and name it PickupSpaw. Set its position to (0, 0, 0), Drag the PickupSpawn GameObject underneath the PickupSpaw and duplicate it six times by pressing Control-D (or Command-D, on the Mac).

To stay organized, change each of the names to: PickupSpawn.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_288_1.png)

Starting from the topmost PickupSpawn GameObject and moving down, set the following positions:

- (-26.0, 0.5, 3)
- (26.0, 0.5, -17)
- (7.0, 0.5, 3.0)
- (-27.0, 0.5, 3.0)
- (28, 0.5, -10.0)
- (-1.5, 0.5, 29.0)

Click Play and you'll see seven pickups spawn in the scene. Feel free to walk around and pick them up.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_289_0.png)

# Robot spawning

Now that the pickups are spawning, you can work on the robots. Drag the Teleporter prefab from the Resources folder into the scene at ground level.

Create a C script and name it RobotSpawn. Open it in your code editor and add the following variables after opening the brace of the class:

```csharp
[SerializeField]
GameObject[] robots;

private int timesSpawned;
private int healthBonus = 0;
```

robots is an array of robot GameObject to instantiate; these will be the red, yellow and blue robots. healthBonus is how much health robot gains each new wave to make the game get harder as you go along. timesSpawned tracks the cycle of the robots.

Next add the following to:

```csharp
public void SpawnSpawned() {
  timesSpawned++;
  healthBonus += 1 * timesSpawned;
  GameObject robot = Instantiate(robots[Random.Range(0, robots.Length)]);
  robot.transform.position = transform.position;
  robot.GetComponent<Robot>().health += healthBonus;
}
```

Spawn() spawns a robot, sets its health, then sets the robot's position. Save your work and switch back to Unity.

Drag the RobotSpawn script onto the Teleporter GameObject. Select the Teleporter GameObject in the Hierarchy, lock the Inspector, and drag the RedRobot, Yellow and BlueRobot from the Resources so the Robot field is in the Inspector.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_290_0.png)

Click Apply and unlock the inspector.

In the Hierarchy, create an empty GameObject, name it RobotSpawns and set its position to (0, 0, 0). Drag the Teleporter into the RobotSpawns and duplicate it three times by pressing Control-D three times (or Command-D on the Mac). Rename each of them Teleporter.

# Unity Games by Tutorials

# Chapter 10: Adding Enemies

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_291_0.png)

Starting from the topmost TeleSpawn GameObject and moving down, set the following positions:

- (-26.0, 0.5, 3)
- (26.0, 0.5, -17)
- (7.0, 0.5, 3.0)
- (-27.0, 0.5, 3.0)
- (28, 0.5, -10.0)
- (-1.5, 0.5, 29.0)

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_291_1.png)

Want to make things more challenging? Then add more spawners!

In the Chapter 11, "Introduction to the UI", you will add the logic to continually change waves. For now, you will simply spawn when you click Play.

Create a C# script, name it Game and replace the contents of the class with the following:

```csharp
private static Game singleton;
[SerializeField]
RobotSpawn[] spawns;
public int enemiesLeft;
```

This uses the singleton pattern to have one and only one; hence, a singleton GameObject. You only want one Game to track everything, such as the score, the remaining robots and the current wave. You'll add all of that in the Chapter 11, "Introduction to the UI"; for now, you'll spawn the robots just once.

spawns is the array of teleporters that spawn robots, and enemiesLeft is a counter, which tracks how many robots are alive.

Now, add the following methods below the final variable:

```csharp
// 1
void Start() {
    singleton = this;
    SpawnRobots();
}

// 2
private void SpawnRobots() {
    foreach (RobotSpawn spawn in spawns) {
        spawn.SpawnRobot();
        enemiesLeft++;
    }
}
```

# Unity Games by Tutorials

# Chapter 10: Adding Enemies

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_293_0.png)

Select the Game Object and lock the Inspector. Drag the Teleporter GameObjects onto the Spawns field. When done, unlock the Inspector.

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_293_1.png)

Click Play and you'll see four robots spawn. Feel free to blast them out of existence and grab some pickups while you're at!

![](img/fd5c2ca20ea33da76d2b61297cc57f6c_293_2.png)
