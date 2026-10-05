# Unity Games by Tutorials

```
GameObject particles = (GameObject)Instantiate(fireParticlesPrefab,
transform.position + new Vector3(0, .5f),
fireParticlesPrefab.transform.rotation);
```

```
//5
// Scale fire particle radius with the aggro radius
particles.transform.localScale *= aggroRadius / 10f;
//6
foreach (Enemy enemy in EntityManager.Instance.GetEnemiesInRange(
transform.position, aggroRadius)
{
    enemy.TakeDamage(attackPower);
n}
```

Here's what you have above:

+   1. A reference to the fire particles that will spread out from the tower each time it attacks.

+   2. Override the AttackEnemy() method from the Tower class to expand on it.

+   3. Call the Tower class AttackEnemy() method.

+   4. Spawn new fire particles.

+   5. Change the particle radius depending on this tower's aggro radius.

+   6. Damage all enemies in this tower's range. This is often referred to as AOE (Area of Effect) attack in games.

Save this script and return to Unity. Select FireTower in the Prefabs ▸ Tower tower and add the FireTower script to it.

![](bbox=[0.31, 0.621, 0.682, 0.763])

Set its Attack Power to 12, adjust Time Between Attacks In Seconds to 3 and change Aggro Radius to 8.

Now, change its Type to Fire and choose FireTowerAttack as the Shoot Sound.

Finally, drag Fire Tower Particles from the Prefabs ▸ Particles folder to the Fire Particles Prefab field.