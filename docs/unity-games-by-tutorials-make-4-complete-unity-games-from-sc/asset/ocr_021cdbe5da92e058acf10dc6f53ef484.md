```
activeGun = pistol;
}
```

Here, you initialize the starting gun as the pistol.

You now need to load the appropriate gun when the player switches weapons. Add the following method:

```
private void loadWeapon(GameObject weapon)
{
pistol.SetActive(false);
assaultRifle.SetActive(false);
shotgun.SetActive(false);
nweapon.SetActive(true);
activeGun = weapon;
}
```

This method will turn off all GameObjects, the passed-in GameObject as active, then update the activeGun reference. You will call this code from Update(). Update that method so that it looks like the following:

```
void Update()
{
 (Input.KeyDown("1")) {
loadWeapon(pistol);
activeWeaponType = Constants.Pistol;
loadWeapon(assaultRifle);
activeWeaponType = Constants.AssaultRifle;
}
else if (Input.KeyDown("3")) {
loadWeapon(shotgun);
activeWeaponType = Constants.Shotgun;
}
}
```

The code in if statement checks whether the pressed key is 1, 2 or 3. Checking for input in every frame this is known as polling. If one of those number is hit, the appropriate block calls loadWeapon() and passes the appropriate weapon to activate. It then sets activeWeaponType as a static. This makes it easy for other scripts to query which gun the player has equipped themselves with.

Finally add the following convenience method:

```
public GameObject GetActiveWeapon()
{
return activeGun;
}
```