# Unity Games by Tutorials

The towers need a way to detect enemies by and select the nearest one as a target.
Add the following methods:

```
//1
public List<Enemy> GetEnemiesInAggroRange()\{
    List<Enemy> enemiesInRange = new List<Enemy>();
    //2
    foreach (Enemy enemy in EnemyManager.Instance)
    {
        if (Vector3.Distance(transform.position, enemy.transform.position) <= aggroRadius)
        {
            enemiesInRange.Add(enemy);
        }
    }
    //3
    return enemiesInRange;
}

//4
public Enemy GetNearestEnemyInRange()\{
    Enemy nearestEnemy = null;
    float smallestDistance = float.PositiveInfinity;
    //5
    foreach (Enemy enemy in GetEnemiesInAggroRange())
    {
        if (Vector3.Distance(transform.position, enemy.transform.position) < smallestDistance)
        {
            smallestDistance = Vector3.Distance(transform.position, enemy.transform.position);
            nearestEnemy = enemy;
        }
    }
    //6
    return nearestEnemy;
}
```

Here's what's going on above:

+   1. GetEnemiesInAggroRange() returns a list of all enemies within this tower's aggro radius.
2. Iterate through all enemies and add enemies that are within range to the enemiesInRange list.
3. Return the list.
4. GetNearestEnemyInRange() returns the enemy that's closest to this tower.