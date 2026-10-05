# Unity Games by Tutorials

The three new components are:

+   1. The Mesh Filter is a component that contains data about your model's mesh and passes it to a renderer.

+   2. The Mesh Renderer displays the mesh. It contains a lot of information about lighting, such as casting and receiving shadows.

+   3. Finally, you'll notice the sphere contains a Sphere Collider. This component serves as the GameObject's boundaries. You'll learn cover colliders in Chapter 4.

Since you want the bullet to participate in Unity's physics, it needs a Rigidbody.

Luckily, you've done this before. Click the Add Component button and select Rigidbody from the Physics category. Make sure to uncheck Gravity.

Since the mine will burn through lots of projectiles, drag it from the Hierarchy to the Prefabs folder in the Project Browser. Delete the projectile from the Hierarchy because you don't need it that it's going to be a prefab.

At this point, you need to create a script to launch the projectile. In the Project Browser, select the Scripts folder then click the Create. Choose C# Script and name it Gun. Double-click the file to launch the code editor.

This needs a few properties underneath the class definition. Add the following:

```
public GameObject bulletPrefab;
public Transform launchPosition;
```

Again, when you create a public variable on a script, Unity exposes these variables in the editor. You will use the bulletPrefab to the bullet prefab you just created, and you will launch the launchPosition to the position of the barrel of the Space Marine's gun.

Next, add the following method:

```
void fireBullet()
{
// 1
GameObject bullet = Instantiate(bulletPrefab) as GameObject;
// 2
bullet.transform.position = launchPosition.position;
// 3
bullet.GetComponent<Rigidbody>().velocity =
transform.parent.forward * 100;
}
```

![](bbox=[0.118, 0.936, 0.28, 0.95])

91