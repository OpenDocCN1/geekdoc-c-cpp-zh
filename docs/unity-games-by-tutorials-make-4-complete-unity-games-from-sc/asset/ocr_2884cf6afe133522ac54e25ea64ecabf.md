# Unity Games by Tutorials

You've probably guessed that you simply need a variable to track the amount of ammunition. That would work, but in Robot Ramp you need to worry about the type of ammunition as well. In this case, it makes sense to have an Ammo class.

Create a C# script and name it Ammo. Open it in your code editor and add the following import to the top (if it's not already):

```
using System.Collections.Generic;
```

This lets you use Dictionary type. In the body of the class at the top, add the following variables:

```
[SerializeField]
GameUI gameUI;
[SerializeField]
private int pistolAmmo = 20;
[SerializeField]
private int shotgunAmmo = 10;
[SerializeField]
private int assaultRifleAmmo = 50;
public Dictionary<string, int> tagToAmmo;
```

The variables pistolAmmo, shotgunAmmo and assaultRifleAmmo track their ammunition counts. tagToAmmo is a dictionary of type string and int, which lets you map your gun's type to its ammunition count.

You need to initialize the Dictionary at game start, so add the following method below where you declare the Dictionary:

```
void Awake()
{
  tagToAmmo = new Dictionary<string, int>
{
    Constants.Pistol, pistolAmmo,
    Constants.Shotgun, shotgunAmmo,
    Constants.AssaultRifle, assaultRifleAmmo,
},
}
```

Awake() is a special method called before Start(). In this case, you want the Dictionary to initialize before any Start() methods to prevent null access errors. This method simply makes each gun type a key in the Dictionary and sets each key's value to the appropriate ammunition type. If you ever wanted to add another ammunition type, you can simply extend the Dictionary.

![](bbox=[0.125, 0.938, 0.275, 0.952])