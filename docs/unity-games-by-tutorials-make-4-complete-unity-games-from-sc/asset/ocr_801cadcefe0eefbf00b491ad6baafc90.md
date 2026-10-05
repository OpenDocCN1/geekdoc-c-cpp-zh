Then create the following method:

```
public DeathParticles GetDeathParticles()
{
    if (deathParticles == null)
    {
        deathParticles = GetComponentInChildren<DeathParticles>();
    }
    return deathParticles;
}
```

The magic occurs in GetComponentChildren(). It returns the first death particle script
it that finds. With only one script there's no possibility of grabbing the wrong one.

In Die(object), add the following before Destroy(gameObject):

```
if (deathParticles)
{
    deathParticles.transform.parent = null;
    deathParticles.Activate();
}
```

This makes the blood splatter when an alien dies. You have to remove the parent.
Otherwise, the particles are destroyed along with the GameObject.

Open GameManager add this instance variable:

```
public GameObject deathFloor;
```

This contains a reference to the death floor.

Add the following after alienScript.OnDestroy.AddListener(AlienDestroyed); in
Update():

```
alienScript.GetDeathParticles().SetDeathFloor(deathFloor);
```

Finally, save all your files and switch to Unity.

In the Project view, expand the Alien prefab and select the AlienParticlesGameObject. Click Add Component and under scripts, choose DeathParticles.

Next, select the GameManager in the Hierarchy and drag the DeathFloor to the
DeathFloor property in the Inspector.

Delete the Alien from the hierarchy as that was only a temporary copy and you don't
eed it anymore.

Now play your game and shoot some aliens — you might need a mop.