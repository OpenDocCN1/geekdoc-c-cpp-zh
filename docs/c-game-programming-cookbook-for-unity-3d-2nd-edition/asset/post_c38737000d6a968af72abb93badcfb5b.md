
distanceFromCameraToSpawnAt as the radius so that the Gizmo exactly represents our spawn distance. In the second instance, when distanceBasedSpawnStart is false, we pass an arbitrary value as the radius instead.

```csharp
public void Update()
{
    float aDist = Vector3.Distance(_TR.position,
        _cameraTransform.position);
    if (distanceBasedSpawnStart && !spawning &&
        aDist < distanceFromCameraToSpawnAt)
    {
        StartSpawn();
        spawning = true;
    }
}
```

The Update() function checks the distance between our Transform and the camera, by using Vector3.Distance(). This is not the most optimized thing to call every single frame, so be aware of this if you use it in a complicated project that may be impacted by this. An alternative might be to only check distance every few frames, instead, or perhaps on a timer.

Once we have the distance value in aDist we check that distanceBasedSpawnStart is true (indicating that we want to do distance-based spawning) and that we are not already spawning -- spawning is false -- then compare aDist to the distanceFromCameraToSpawnAt value. If these conditions are met, we can call StartSpawn() to spawn the prefab(s) and we set spawning to true to avoid any duplicate calls to spawn now that the process is in motion.

```csharp
void StartSpawn()
{
    StartWave(totalAmountToSpawn,
        timeBetweenSpawns);
}
```

To get the spawning process in motion, we call StartSpawn() above that will then call another function StartWave(). You will see below what StartWave() does, but note for now just that you pass in how many prefabs you want to spawn followed by the amount of time the system should wait before spawning another one.

Spawning is a process in this function, rather than a single action. StartWave() will continue to spawn as many objects as you tell it to, ultimately disabling its own GameObject once all prefabs have been added to the Scene.

```csharp
public void StartWave(int HowMany, float timeBetweenSpawns)
{
    spawnCounter = 0;
    totalAmountToSpawn = HowMany;

    // reset
    currentObjectNum = 0;
    CancelInvoke("doSpawn");
}
```

As StartWave() is the beginning of our spawn wave, we need to do a little set up first. spawnCounter is a variable we will use to keep tabs on how many prefabs this Spawner has added to the Scene. The value of spawnCounter will be compared to totalAmountToSpawn (set by the code above to the first parameter passed into this function, howMany) to know when to stop spawning.

currentObjectNum is an index number we can use to refer to the array holding all the prefabs. When there are more than one prefabs in that array (set in the Inspector) then currentObjectNum will be increased every time a new prefab is spawned so that we get the next item from the array next time.

If there are more prefabs to spawn, a function named doSpawn() will be called repeatedly – until all prefabs are made. We use Unity's Invoke() function to schedule a call to doSpawn(), so whenever we run StartWave we make sure there are no outstanding Invoke calls to doSpawn() by using the CancelInvoke() function. If there are any outstanding, CancelInvoke() will flush all of them out at once.

```csharp
// the option is there to spawn at random
// times, or at fixed intervals...
if (shouldRandomizeSpawnTime)
{
    // do a randomly timed invoke call,
    // based on the times set up in the inspector
    Invoke("doSpawn", Random.Range(minimumSpawnTimeGap, timeBetweenSpawns));
}
else
{
    // do a regularly scheduled invoke
    // call based on times set in the inspector
    InvokeRepeating("doSpawn",
        timeBetweenSpawns, timeBetweenSpawns);
}
```

Above, we look to see if shouldRandomizeSpawnTime is true. If it is, we use a random amount of time between minimumSpawnTimeGap and the value of timeBetweenSpawns (which was passed into this function as a parameter). Having a randomized spawn time can just make a game more interesting than having enemies spawning at fixed times all the time.

If shouldRandomizeSpawnTime is false, instead of using standard Invoke() to schedule the call to doSpawn(), the code here uses InvokeRepeating(). This will repeat the call to doSpawn() indefinitely – it takes two parameters, the first is the time before we do the first spawn, and the second parameter is the time between that and every other call after. We just use the value in timeBetweenSpawns for timing, passing its value in to InvokeRepeating() as both parameters.

```csharp
void doSpawn()
{
    if (spawnCounter >= totalAmountToSpawn)
    {
        if (shouldRepeatWaves)
        {
            spawnCounter = 0;
        }
        else
        {
            CancelInvoke("doSpawn");
            this.enabled = false;
            return;
        }
    }
}
```

As mentioned above earlier in the section, doSpawn() is called repeatedly until all of the prefabs we want to spawn have been added to the Scene. To accomplish that, spawnCounter counts up, and we compare it to totalAmountToSpawn to know how to proceed.

Above, if spawnCounter is greater than or equal to totalAmountToSpawn then we need to end this wave of spawning and either start another wave by resetting spawnCounter to 0, or to cancel further calls to doSpawn() entirely with CancelInvoke(). If we are dropping out entirely and ending all spawning, the `this.enabled = false` line will disable the GameObject so that it no longer receives any calls to its functions from the engine (no more FixedUpdate(), Update(), or LateUpdate() calls and so on). We also know that enough spawns have been made, so we drop out of the function.

```csharp
// create an object
Spawn(_spawnObjectPrefabs[currentObjectNum].transform,
    _TR.position, Quaternion.identity);
```

Above, we call out to a function named Spawn() - a custom function from the ExtendedCustomMonoBehaviour class - to instantiate the prefab into the Scene. The parameters that Spawn() takes is a Transform for the prefab to spawn, a position, and a rotation.

```csharp
spawnCounter++;
currentObjectNum++;
// check to see if we've reached the end of the spawn objects array
if (currentObjectNum > _spawnObjectPrefabs.Length - 1)
    currentObjectNum = 0;
if (shouldRandomizeSpawnTime)
{
    // cancel invoke for safety
    CancelInvoke("doSpawn");
    // schedule the next random spawn
    Invoke("doSpawn", Random.Range(minimumSpawnTimeGap,
        timeBetweenSpawns));
}
```

With the new prefab added to the Scene, our counters, spawnCounter and currentObjectNum, are incremented. After that, we check currentObjectNum to see if it has been incremented too far - past the end of the _spawnObjectPrefabs array. If we tried to use this as an index number to access the prefabs array, Unity would throw an error, so at this point if we find that currentObjectNum is too high it gets reset to 0.

Earlier in the class, we used the shouldRandomizeSpawnTime flag to decide whether to call this function with Invoke() or call it with InvokeRepeating(). Above, if we are using a randomized spawn time, we need to schedule the next call to doSpawn at a different, randomized period of time. For this, first any outstanding calls to doSpawn() are cancelled with CancelInvoke() - this is just a safety measure, as in the current state there should never be any duplicate calls. Again, we use Invoke() and Random.Range() to choose a random period of time. Random.Range() takes the minimum value of minimumSpawnTimeGap and the maximum value of timeBetweenSpawns.

### 5.8.2 Trigger Spawning

The TriggerSpawner class instantiates an object when another object enters the trigger that this script Component is attached to.

The easiest way to use this Component is to add a cube primitive to a Scene and set its Box Collider's IsTrigger property to true. Add this TriggerSpawner Component to your cube and then whenever your player enters the area outlined by the cube, it will trigger this script to spawn a prefab. Once you have the area worked out correctly, disable the cube's Mesh Renderer Component and you have a trigger spawn area.

One such use for this script would be to spawn an enemy when the player reaches an area in a level.

```csharp
using UnityEngine;

namespace GPC
{
    [AddComponentMenu("CSharpBookCode/Utility/Trigger Spawner")]
    public class TriggerSpawner : Spawner
    {
        public GameObject ObjectToSpawnOnTrigger;
        public Vector3 offsetPosition;
        public bool onlySpawnOnce;
        public LayerMask triggerLayerMask;
```

We add this script as a menu item first, using Unity's AddComponentMenu tag. This class derives from the Spawner class from Section 5.8.1 of this chapter, so we can use its Spawn() function, have it draw a Gizmo so we can see where we will be spawning, and to get access to its base class, ExtendedCustomMonoBehaviour.

```csharp
void OnTriggerEnter(Collider other)
{
    if (IsInLayerMask(other.gameObject.layer, triggerLayerMask))
        return;
    Spawn(ObjectToSpawnOnTrigger.transform, _TR.position + offsetPosition, Quaternion.identity);
    if (onlySpawnOnce)
        Destroy(gameObject);
}
```

When an object with a Rigidbody and a Collider enters this GameObject's Collider (which MUST have its IsTrigger property checked in the Inspector), the prefab in objectToSpawnOnTrigger will be spawned at this GameObject's position.

### 5.8.3 Timed Spawning

This TimedSpawner Component will spawn a prefab in a set amount of time. In an arena blaster game, this might be used to delay the spawning of an enemy from the start of a level, using a random delay to make the start of the level more dynamic.

```csharp
using UnityEngine;

namespace GPC
{
    public class TimedSpawner : Spawner
    {
        public float initialSpawnDelay;
        public bool shouldRandomizeSpawnTime = true;
        public float randomDelayMax = 0.5f;
```
