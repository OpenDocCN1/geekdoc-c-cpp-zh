![](bbox=[0.18, 0.06, 0.82, 0.52])

Figure 4.1 The Player GameObject has physics and collision Components attached to it, as well as Components to deal with data, sound, movement, and input.

# 4.1 A Player Controller

Things can be a little complicated when we look at the character controller class and its inherited scripts. As an example, a player might use a class name BlasterPlayerController that inherits a string of other classes:

```
ExtendedMonoBehaviour<BasePlayerStats<BaseCharacterController<ShootingPlayerCharacter<BlasterPlayerController
```

We are essentially layering classes on top of one another to provide the functionality we need for the specific game we are building. For example, if we wanted to change the character above to a player that could run around but did not need to use weapons, all it would take would be to remove one of the classes in the chain (changing the class declaration of BlasterPlayerController to derive from BaseCharacterController rather than ShootingPlayerCharacter) so that it looks like:

```
MonoBehaviour
<ExtendedMonoBehaviour<BasePlayerStats<BaseCharacterController
<BlasterPlayerController
```

Let's say, this time, that we now want to replace the person with a vehicle. The new chain might look like this:

```
MonoBehaviour
<ExtendedMonoBehaviour<BasePlayerStats<BaseVehicleController
<ShootingVehicleController<BlasterPlayerController
```