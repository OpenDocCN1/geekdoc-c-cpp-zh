This chunk of code does quite a lot for you:

+   1. Decrement the attackCounter.

+   2. Check if there's currently no enemy targeted.

+   3. If there's a Transform to rotate, look at a neutral position. This is the tower's idle state.

+   4. Attempt to find a new target enemy.

+   5. Check if there's a target enemy assigned.

+   6. If so, look at the target enemy.

+   7. If attackCounter is equal or below zero, call AttackEnemy() and reset the counter.

+   8. If the target enemy moves out of range, set the targetEnemy to nothing.

Almost done! Add this method to complete the Tower script:

```
public void LevelUp() {
    towerLevel++;
    //Calculate new stats for this tower
    attackPower *= 2;
    timeBetweenAttacksInSeconds *= 0.7f;
    aggroRadius *= 1.20f;
}
```

This levels up the tower: It adds a level and increases the tower's attack power, shooting cooldown and aggro radius by multiplying the values. This ensures an upgraded tower is more powerful than a new Level 1 variant.

Save this script and return to the Scripts > Game > Tower folder named StoneTower. Create a C# Script in the StoneTower and open it up. Remove the Start() and Update() methods completely and replace this line:

```
public class StoneTower : MonoBehaviour {
with:
public class StoneTower : Tower {
```

This makes sure this class inherits from Tower.