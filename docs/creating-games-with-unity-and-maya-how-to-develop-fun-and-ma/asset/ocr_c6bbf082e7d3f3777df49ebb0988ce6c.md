component Emit is turned off (a script activates it). This script is called SteamEmitters and it simply turns the emitters on and off based upon the distance the emitters are from the player:

```
private var fpcAegis : GameObject;

function Start () {
    fpcAegis = GameObject.Find("FPC_AegisChurch");
}

function Update () {
    var dist = Vector3.Distance (fpcAegis.transform
    .position, transform.position);
    if (dist <25) {
        particleEmitter.emit = true;
    } else {
        particleEmitter.emit = false;
    }
}
```

This is so that when walking through the dark version of the model, the steam for the entire level isn't visible (the shaders for particles are light independent). So as the player gets closer, the emitter emits.

The version of steam included in the Steam Unity package also includes an Audio Source component (Component>Audio>Audio Source) with a looping steam sound. Importantly, it contains a Box Collider component (Component>Physics>Box Collider) that is set to be a trigger. Finally, the Steam GameObject has attached to it the DamagePlayerScript with a Damage Amount set to 2 (Figure 17.9).

![](bbox=[0.2059, 0.6389, 0.9393, 0.9232])

Figure 17.9 Steam prefab.