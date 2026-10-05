# Projectiles

This simple script will follow an enemy around until it hits target, damaging it in the process!

Make a new folder in Scripts ▸ Game ▸ Tower new Weapons and create a new C# Script named FollowingProjectile. Open it in a code editor and remove the Start() and Update() methods.

This class will be another abstract class as the actual scripts you'll be putting on the projectiles will be derived from it. This makes it easy to add new types of projectiles. Add the abstract keyword between public and class to make it into an abstract class.

```
public abstract class FollowingProjectile : MonoBehaviour {
```

An abstract is to be subclassed, but can still provide behavior that subclasses can inherit. Add this underneath the line you edited:

```
//1
public Enemy enemyToFollow;
//2
public float moveSpeed = 15;

private void Update()
{
//3
    if (enemyToFollow == null)
{
        Destroy(gameObject);
    }
else
//4
    transform.LookAt(enemyToFollow.transform);
    GetComponent<Rigidbody>().velocity = transform.forward * moveSpeed;
}

//5
public void OnTriggerEnter(Collider other)
{
    if (other.GetComponent<Enemy>() == enemyToFollow)
{
        OnHitEnemy();
    }
}

//6
protected abstract void OnHitEnemy();
```