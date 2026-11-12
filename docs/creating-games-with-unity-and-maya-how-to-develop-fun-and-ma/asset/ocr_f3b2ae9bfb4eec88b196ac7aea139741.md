Step 10: Apply HealthEngineScript to FPC_AegisChung. Go ahead and break the Prefab connection when prompted, then reattach to prefab via the Prefab Apply button. Test and play. The HealthLevel that should be displayed at the top of the screen should swap from 0 to 100.

# Why?

We'll want this health system in all the places we're showing the GUIElements. Make it once here, reap the benefits everywhere.

# Back to Script

+   1. Step 11: Reopen HealthEngineScript.
+   2. Step 12: Create the function that deducts from the health level when damage is done.

```
var health : int;
private var healthLevel : GameObject;

function Awake () {
    healthLevel = GameObject.Find("HealthLevel");
}

function Start() {
    health = 100;
    healthLevel.guiText.text = health.ToString();
}

function ApplyDamage (damage : int){
    health -= damage;
    healthLevel.guiText.text = health.ToString();
    if (health <= 0){
        KillPlayer ();
    }
}
```

# Why?

The first line is defining the name of the function (applyDamage declares a local variable “damage” that is an integer). This local variable declared here will mean we can easily pass values to the function.

Then, the first command is a bit of programming shorthand. health -= damage means, “subtract damage from health, and that's the new health value.” It's a little unintuitive at first glance, but saves loads of time when doing counting sorts of things.

The next command just says (as before), write the string version of the health value to the text of the guiText component attached to healthLevel.

Finally, it checks to see if the health level is equal to or has dropped beneath 0, and if it has, fire the function KillPlayer (which we haven't written yet).