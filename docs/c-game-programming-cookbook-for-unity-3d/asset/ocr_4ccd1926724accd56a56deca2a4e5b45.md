The player spaceships persist across levels, keeping the same GameObjects and components from the start of the game right through to the end. In the Start() function, DestroyOnLoad tells Unity to keep this gameObject transform alive throughout:

```
public override void Start() {
    // we want to keep the player object alive through the
    // game, so we use DestroyOnLoad to keep it alive
    DestroyOnLoad(this.transform);
}
```

There are some variables that need to be set up by the base class (BaseTopDownSpace-Ship), and rather than duplicating the code in this derived class, we call base.Init() to run the original script's Init() function before calling Init() on this class:

```
didInit=false;

// tell our base class to initialize
base.Init();

// now we do our own init
this.Init();

```

The Boolean variable godMode is used to make the player invulnerable. The intention is that godMode will be set in the Unity editor Inspector window and only used during testing to get through a level easily. When Init() starts up, the first thing that happens is the default state for vulnerability/invulnerability is set. The functions MakeVulnerable() and MakeInvulnerable() will deal, respectively, with showing or hiding a shield mesh around the player, as well as with setting the right variable to make it work:

```
public override void Init() {
    // hide the invulnerability shield(i)
    if (godMode) {
        MakeVulnerable();
    } else {
        MakeInvulnerable();
    }
}
```

The weapon control system needs to know what the player's ID is, so that it can tell all of the projectiles it spawns which ID to carry with (making the projectiles traceable back to either player 1 or player 2). The Standard_SlotWeaponController reference found and stored in the variable weaponControl, then its SetOwner() function is called to set the owner ID to the ID of the player:

```
// get a ref to the weapon controller
weaponControl=myGO.GetComponent<Standard_SlotWeaponController>();

```

```
// tell weapon control who we are (so all weapon control can tell
// projectiles who sent them)
weaponControl.SetOwner(ownerID);
```