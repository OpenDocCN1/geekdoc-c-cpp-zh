```
public void GoNext()
{
    // if our index goes over the total number of levels in the
    // array, we reset it
    if(gameLevelNum >= levelNames.Length) {
        gameLevelNum = 0;
    }
}
```

```
// load the level (the array index starts at 0, but we start
// counting game levels at 1 for clarity's sake
LoadLevel( gameLevelNum);
```

```
// increase our game level index counter
gameLevelNum++;
```

```
private void LoadLevel( int indexNum)
{
    // load the game level
    LoadLevel( levelNames[indexNum] );
}
```

# 4.10.1 Script Breakdown

The Sript derives from MonoBehavior and should be attached to an empty gameObject:

```
using UnityEngine;
using System.Collections;
```

```
public class SceneManager : MonoBehaviour
{
```

The (Start) function calls DontDestroyOnLoad and passes in reference to this instance's gameObject. What does this tell the game engine not to remove the gameObject from the game when a new one is loaded. The new scene will load as expected and this gameObject will still exist in the new scene:

```
public void Start ()
{
    // keep this object alive
    DontDestroyOnLoad(this.gameObject);
}
```

LoadLevel() may be used to load a new scene directly, passing in the name of the scene as a string. Application.LoadLevel loads the specified scene:

```
public void LoadLevel( string sceneName )
{
    Application.LoadLevel( sceneName );
}
```