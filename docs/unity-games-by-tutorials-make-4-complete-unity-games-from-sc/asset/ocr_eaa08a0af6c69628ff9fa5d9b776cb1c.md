# Unity Games by Tutorials

5. Iterate through all enemies within range and keep storing the enemy that's the closest by. When the whole list has been iterated, the NearestEnemy will be the one's closest.

6. Return the nearest enemy.

The biggest and most important method of Tower is Update(); it handles the rotation, targeting and attacking. Add this below the other methods:

```
public virtual void Update()
{
    //1
    attackCounter -= Time.deltaTime;
    //2
    if (targetEnemy == null)
    {
        //3
        if (towerPieceToAim)
        {
            SmoothlyLookAtTarget(towerPieceToAim.transform.position,
new Vector3(0, 0, 1));
        }
        //4
        if (GetNearestEnemyInRange() != null
            && Vector3.Distance(transform.position,
GetNearestEnemyInRange().transform.position)
<= aggroRadius)
            targetEnemy = GetNearestEnemyInRange();
    }
    else
        // 5
        //6
        if (towerPieceToAim)
        {
            SmoothlyLookAtTarget(targetEnemy.transform.position);
        }
        //7
        if (attackCounter <= 0f)
        {
            // Attack
            AttackEnemy();
            // Reset attack counter
            attackCounter = timeBetweenAttacksInSeconds;
        }
    //8
    if (Vector3.Distance(transform.position,
        targetEnemy.transform.position) > aggroRadius)
    {
        targetEnemy = null;
    }
}
```