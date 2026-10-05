Did you notice that a GameObject was created called EventSystem in the Hierarchy after you created the first Button?

# EventSystem

This is how your UI buttons can be clicked to trigger events. The EventSystem GameObject listens for these click (or hover) events and dispatches to something that needs to know that they've happened. You don't need to worry about how it dispatches its events; all that matters is how you intercept them.

Create a C script, name it Menu and open it in the code editor. First, add this import at the top of the script:

```
using UnityEngine.SceneManagement;
```

This allows you to use the SceneManager type. This is a class that allows you to manage your scenes such as loading, unloading or even searching for a scene.

Now, add the following methods to the body of the class:

```
// 1
public void StartGame()
{
    SceneManager.LoadScene("Battle");
}

// 2
public void Quit()
{
    Application.Quit();
}
```

+   1. This method will be used when the user clicks the Begin button; it simply loads the Battle scene.
2. This method will be used to exit the app. However, note that if you are running the game in Unity (instead of within a standalone build) this won't do anything.

With these methods set up, you can now configure the buttons to actually call them. Save your work and switch back to Unity.

Select the MenuUI GameObject and drag over the Menu script to it. Now, you must hook the methods to the buttons.

Select the BeginButton GameObject and click the + in the Button component.