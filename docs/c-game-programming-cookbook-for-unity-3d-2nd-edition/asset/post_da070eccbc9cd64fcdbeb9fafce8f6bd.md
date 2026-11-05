
Again, as with the other implementation of PlaySoundByIndex(), we take a SoundObject instance from the soundObjectList array, using the passed in parameter anIndexNumber, and hold it in a variable named tempSoundObj. We then see whether or not theListenerTransform variable actually has anything in it – if it has, we use the position of theListenerTransform to position the sound by passing its position into PlaySound(). If there is nothing in theListenerTransform, we found no Listener in the Scene, and instead we pass Vector3.zero to PlaySound() to make the sound play at world space 0,0,0.

The audio fade functions are all similar but do different things with the volume levels. There are three functions for you to use:

StartFadeIn(AudioMixer audioMixer, string exposedParam, float duration)

This will fade the exposed parameter in exposedParam of the AudioMixer, from -80 decibels to 0, in time duration x seconds.

StartFadeOut(AudioMixer audioMixer, string exposedParam, float duration)

This will fade out the exposed parameter in exposedParam of the AudioMixer from 0 decibels to -80, in time duration x seconds.

StartFade(AudioMixer audioMixer, string exposedParam, float duration, float targetVolume)

This will transition the exposed parameter in exposedParam of the AudioMixer from its current value to targetVolume, in time duration x seconds.

```csharp
public static IEnumerator StartFadeIn(AudioMixer audioMixer, string exposedParam, float duration)
{
    float targetVolume = 1;
    float currentTime = 0;
    float currentVol = -80f;
    currentVol = Mathf.Pow(10f, currentVol / 20f);
    float targetValue = Mathf.Clamp(targetVolume, 0.0001f, 1);
    while (currentTime < duration)
    {
        currentTime += Time.deltaTime;
        float newVol = Mathf.Lerp(currentVol, targetValue, currentTime / duration);
        audioMixer.SetFloat(exposedParam, Mathf.Log10(newVol) * 20f);
        yield return null;
    }
    yield break;
}

public static IEnumerator StartFadeOut(AudioMixer audioMixer, string exposedParam, float duration)
{
    float targetVolume = -80;
    float currentTime = 0;
    float currentVol;
    audioMixer.GetFloat(exposedParam, out currentVol);
    currentVol = Mathf.Pow(10f, currentVol / 20f);
    float targetValue = Mathf.Clamp(targetVolume, 0.0001f, 1);
    while (currentTime < duration)
    {
        currentTime += Time.deltaTime;
        float newVol = Mathf.Lerp(currentVol, targetValue, currentTime / duration);
        audioMixer.SetFloat(exposedParam, Mathf.Log10(newVol) * 20f);
        yield return null;
    }
    yield break;
}

public static IEnumerator StartFade(AudioMixer audioMixer, string exposedParam, float duration, float targetVolume)
{
    float currentTime = 0;
    float currentVol;
    audioMixer.GetFloat(exposedParam, out currentVol);
    currentVol = Mathf.Pow(10f, currentVol / 20f);
    float targetValue = Mathf.Clamp(targetVolume, 0.0001f, 1);
    while (currentTime < duration)
    {
        currentTime += Time.deltaTime;
        float newVol = Mathf.Lerp(currentVol, targetValue, currentTime / duration);
        audioMixer.SetFloat(exposedParam, Mathf.Log10(newVol) * 20f);
        yield return null;
    }
    yield break;
}
}
```

### 9.3 Adding Sound to Weapons

To add a sound to weapons, the easiest method is to add an AudioSource to the projectile prefab and set its PlayOnAwake checkbox to true. Whenever a projectile is spawned, the sound will be played. By attaching the sound to the projectiles, you can easily have different sounds for different projectile types just by changing the clip on the AudioSource.

## 10 AI Manager

The AI controller in this book is a state machine. You may have heard of this before, but what do we mean when we say state machine? Our AI system stores the current state of the AI and runs code according to whichever state it is. When the state changes, it runs different code. For example, when our state is set to chase, the AI should move toward an object. When the state is set to stopped, the AI should stand still. This is state machine AI.

In this book, the AI is split into several different scripts that fit together to add functionality. You can think of our main AI class, BaseAIController, as a class containing a set of utility functions for AI rather than a single all-encompassing script.

- 1. BaseAIController：This contains base code for AI such as chase/follow behavior.
- 2. WaypointsController：The code for dealing with waypoints: this is optional, depending on whether you want waypoint following.
- 3. AIBotController：Using BaseAIController, this class can move a bot around, chase, and attack a target and stand on guard to look for a target to chase and attack. This is used by the Blaster game example in this book to move the bots around.
- 4. AISteeringController：This uses the BaseAIController and WaypointsController to provide steering inputs that will follow a waypoint path (used in the example racing game in this book to drive the AI cars around the track).

We will be looking at the above scripts and breaking them down in this chapter, as well as a method for getting the weapon system firing with AI.

Note that this AI system is only intended for 3D games.

### 10.1 AI States

Before getting to the main BaseAIController.cs script, take a look at AIStates.cs below. It contains all of the AIStates from the previous section stored in an enumerator list similar to the one used by the character controller from Chapter 5 of this book. This list will be used by the AI to determine its current required behavior. The list is in its own file (the AIStates.cs file) and in a namespace called AIStates so that we can easily make it accessible from any script used by the game:

```csharp
using UnityEngine;
namespace AIStates
{
    public enum AIState
    {
        moving_looking_for_target,
        chasing_target,
        backing_up_looking_for_target,
        stopped_turning_left,
        stopped_turning_right,
        paused_looking_for_target,
        translate_along_waypoint_path,
        paused_no_target,
        steer_to_waypoint,
        steer_to_target,
    }
}
```

### 10.2 The BaseAIController Class – Base AI Control

BaseAIController starts with the UnityEngine namespace as well as adding AIStates, as seen in the previous Section 10.1. By including AIStates as a namespace, it can be accessed as though it were part of the same script. We wrap the class in the GPC namespace, and it derives from ExtendedCustomMonoBehaviour:

```csharp
using UnityEngine;
using AIStates;
namespace GPC
{
    [AddComponentMenu("CSharpBookCode/Base/AI Controller")]
    public class BaseAIController : ExtendedCustomMonoBehaviour
    {
        public bool AIControlled;

        [Header("AI States")]
        public AIState currentAIState;
        public AIState targetAIState;

        [Header("Enemy input")]
        public float horz;
        public float vert;

        [Header("Enemy AI movement values")]
        public float obstacleAvoidDistance = 40f;
        public float modelRotateSpeed = 15f;
        public int _followTargetMaxTurnAngle = 120;
        public float minChaseDistance = 1f;
        public float maxChaseDistance = 10f;
        public float visionHeightOffset = 1f;

        [Header("Waypoints")]
        // waypoint following related variables
        public WaypointsController _waypointsController;
        public Transform _currentWaypointTransform;
        public Transform _shouldFollowTarget;
        public Transform _rotateTransform;

        [System.NonSerialized]
        public bool reachedLastWaypoint;
        public float waypointDistance = 5f;
        public float pathSmoothing = 2f;
        public bool pathShouldReversePathFollowing;
        public bool loopPath;
        public bool destroyAtEndOfWaypoints;
        public bool startAtFirstWaypoint;

        [Header("Layer masks and raycasting")]
        public LayerMask obstacleAvoidLayers;
        public string potentialTargetTag = "Player";
        public LayerMask targetLayer;
        public int obstacleFinderResult;

        private int totalWaypoints;
        private int currentWaypointNum;
        private RaycastHit hit;
        private Vector3 tempDirVec;
        private Vector3 relativeTarget;
        private float obstacleAngle;
        private int obstacleHitType;
        public int lookAheadWaypoints = 0;
```

There are a lot of variables to declare, so don't worry about those. We will see how they are used later in the breakdown. Other than ExtendedCustomMonoBehaviour, this script only uses one more script from the framework in this book – the WaypointsController class for using waypoints. Everything else is standalone and ready to be used in your projects regardless of whether you use the framework.

Once we get past the class declaration, we kick things off with a Start() function:

```csharp
public virtual void Start()
{
    Init();
}
```

The Init() function takes care of making cached references to the GameObject, the Transform and its Rigidbody (this script assumes that there will always be a Rigidbody attached to the same GameObject it is attached to as a Component):

```csharp
public virtual void Init ()
{
    // cache ref to gameObject
    _GO = GetComponent<GameObject>();
    // cache ref to transform
    _TR = GetComponent<Transform>();
    // cache a ref to our rigidbody
    _RB = _TR.GetComponent<Rigidbody>();
}
```

Above, Init() grabs references to other objects we will be needing further in the script.

```csharp
if (_rotateTransform == null)
    _rotateTransform = _TR;
```
