Start() begins by getting a reference to the AI controller component. It does this with Unity's GetComponent() function, employed here as a key, meaning that it will look for the component on the gameObject this script is attached to:

```
void Start () {
    // first, let's try to get the AI control script
    // automatically
    AIControllerComponent = GetComponent<BaseAIController>();
}
```

Next, the regular gameObject and transform references are cached, and a quick check is made to make sure that we have an AI controller:

```
myGO = gameObject;
tmyTransform = transform;

// quick null check, to warn us if something goes wrong
if (AIControllerComponent == null) {
    Debug.LogWarning("SetAIChaseTargetBasedOnTag cannot findBaseAIController");
}
```

The main part of this script is within LookForChaseTarget(), but it is not something we need to do every step or frame of the game running. Instead, InvokeRepeating uses a repeated call to do it every 1.5 seconds:

```
InvokeRepeating("LookForChaseTarget", 1.5f, 1.5f);
```

This script will not work if it has not been able to find an AI controller script (BaseAIController.cs) attached to the same gameObject. LookForChaseTarget() does a quick null check to get started:

```
void LookForChaseTarget () {
    // null check
    if(AIControllerComponent == null)
        return;
}
```

To find another target, references to all of the potential gameObjects need to be retrieved and put into an array. array of all gameObjects in the scene whose tag matches the one passed as a parameter. The defaultTagFilter variable is actually just string containing the word "enemy," which corresponds to the tag with the same name in the Unity editor:

```
GameObject[] gos = GameObject.FindGameObjectsWithTag(
    defaultTagFilter);
```

A foreach loop steps through each gameObject in the array named gos, which holds all of the tagged objects returned by the call to FindGameObjectsWithTag():