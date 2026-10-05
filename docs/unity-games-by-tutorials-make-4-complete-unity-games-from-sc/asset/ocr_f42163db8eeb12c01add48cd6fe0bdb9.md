Starting from the topmost PickupSpawn GameObject and moving down, set the following positions:

+   - (-26.0, 0.5, 3)
- (26.0, 0.5, -17)
- (7.0, 0.5, 3.0)
- (-27.0, 0.5, 3.0)
- (28, 0.5, -10.0)
- (-1.5, 0.5, 29.0)

Click Play and you'll see seven pickups spawn in the scene. Feel free to walk around and pick them up.

![](bbox=[0.306, 0.417, 0.692, 0.626])

# Robot spawning

Now that the pickups are spawning, you can work on the robots. Drag the Teleporter prefab from the Resources folder into the scene at ground level.

Create a C script and name it RobotSpawn. Open it in your code editor and add the following variables after opening the brace of the class:

```
[SerializeField]
GameObject[] robots;

private int timesSpawned;
private int healthBonus = 0;
```