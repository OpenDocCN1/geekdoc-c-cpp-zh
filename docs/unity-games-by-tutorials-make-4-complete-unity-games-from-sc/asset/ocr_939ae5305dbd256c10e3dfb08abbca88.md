Open the Player script in the code editor and add the following:

```
// 1
private void pickupHealth() {
    health += 50;
    if (health > 200) {
        health = 200;
    }
}

private void pickupArmor() {
    armor += 15;
}

// 2
private void pickupAssaultRifleAmmo() {
    ammo.AddAmmo(Constants.AssaultRifle, 50);
}

private void pickupPistolAmmo() {
    ammo.AddAmmo(Constants.Pistol, 20);
}

private void pickupShotgunAmmo() {
    ammo.AddAmmo(Constants.Shotgun, 10);

```

+   1. This adds to the players health and armor.

+   2. This adds ammunition for that gun type.

Now, add the following:

```
public void PickupItem(int pickupType) {
    switch (pickupType) {
        case Constants.PickUpArmor:
            pickupArmor();
            break;
        case Constants.PickUpHealth:
            pickupHealth();
            break;
        case Constants.PickUpAssaultRifleAmmo:
            pickupAssaultRifleAmmo();
            break;
        case Constants.PickUpPistolAmmo:
            pickupPistolAmmo();
            break;
        case Constants.PickUpShotgunAmmo:
    }

```