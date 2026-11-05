GetTime() just returns the value of the variable currentTime so that you can take care of formatting or processing in another script.

# 5.10.7.1 Modifying the Timer to Update Automatically

If you want to use this and have the timer to update automatically, you could change the class declaration:

```
public class TimerClass
```

So that the class inherits from MonoBehaviour:

```
public class TimerClass : MonoBehaviour
```

Then, change the name of the UpdateTimer() function to Update(), which will be automatically called by the engine each frame.

# 5.10.8 WaypointsController

This script is so big and important that it gets its own chapter! Check out Chapter 8 to see how this script fits together and how it should be used in your own games.

# 5.11 Weapons

In the Weapons folder are four scripts: AutoShooter.cs, ProjectileController.cs, StandardSlotWeaponController.cs and ThreeWayShooter.cs. These scripts and how the weapons system can be used will be covered in full, in Chapter 7 of this book.