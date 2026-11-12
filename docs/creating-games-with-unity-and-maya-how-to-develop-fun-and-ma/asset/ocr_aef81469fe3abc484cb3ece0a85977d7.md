that it's lower than the dock (of course) since it should register a collision only when the player steps off the dock. Name it Trigger-WaterKiller.

![](bbox=[0.1, 0.17, 0.59, 0.4])

FIGURE 17.7 Our water collider

**Step 15:** Create a new JavaScript. Name it DamagePlayerScript and open it.

**Step 16:** Create two variables—one to store the amount of damage the trigger will do, and a second to keep track of whether the player is still in the trigger or not:

```
var damageAmount : int;
private var inTrigger : boolean;
```

**Why?**

By leaving damageAmount as a public variable, we can reuse this script again and again. So for the water, the script can be set to do a little bit of damage (and then repeat the damage if the player remains in the water), but if the player jumps off a cliff, it can do 100 damage and kill them right away.

**Step 17:** Create the mechanism that checks to see if something has entered the trigger. Have it check to see if the object's tag is "Player" and if it is, set the Boolean inTrigger to true, and fire a function that does damage:

```
var damageAmount : int;
private var inTrigger : boolean;

function OnTriggerEnter (other:Collider){
    if (other.gameObject.tag == "Player"){
        inTrigger = true;
        DoDamage (other.gameObject);
    }
}
```