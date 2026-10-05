The SceneManager variable contains a reference to the SceneManager component that will be responsible for figuring out which level to load in next. First, GetSceneManager() is called to make sure we have a working reference to it:

```
 // make sure we have a scene manager to talk to
GetSceneManager();
```

As long as SceneManager exists (and is not null), the call to GoNextLevel() will have the scene manager load the next game scene and increment its current level counter:

```
 // tell scene manager to load the next level
if(sceneManager != null)
{
    sceneManager.GoNextLevel();
} else {
    Debug.LogError("SCENE MANAGER DOES NOT EXIST. CAN'T
    MOVE TO NEXT LEVEL!");
}
```

To find the SceneManager.cs script component, the GetSceneManager() function first needs to find its gameObject. The gameObject has been named SceneManager in the Unity editor, so a call to GameObject.Find() should return it without any trouble:

```
void GetSceneManager ()
{
    // find level loader object
    GameObject sceneManagerGO =
    GameObject.Find("SceneManager");
}
```

Assuming the gameObject has been found and a reference stored in ManagerGO, which we do a quick check on here, we can go ahead and grab another reference, this time to the SceneManager component itself. GameObject.GetComponent() finds the SceneManager:

```
 // check to see if we managed to find a manager
// before trying to get at its script
if(sceneManagerGO!=null)
    sceneManager=
    sceneManagerGO.GetComponent<SceneManager>();

```

EnemyDestroyed() is an overridden version of the function, which can be found in the original base class (BaseGameController.cs). We need to add some extra functionality to it:

```
 override void EnemyDestroyed ( Vector3 aPosition,
 int pointsValue, int hitByID)
{}
```

When an enemy is destroyed, the scene would not be complete without a sound effect. BaseSoundController provides a explosion sound:

```
 // tell our sound controller to play an explosion sound
BaseSoundController.Instance.PlaySoundByIndex( 1, aPosition);
```