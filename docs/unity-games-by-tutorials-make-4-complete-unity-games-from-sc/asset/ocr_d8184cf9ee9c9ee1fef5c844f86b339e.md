# Unity Games by Tutorials

Your UI will look as follows:

![](bbox=[0.273, 0.126, 0.722, 0.366])

With the layout complete, just need to hook it up in code.

Open the Game script, and add the class declaration, as the following:

```
using UnityStandardAssets.Characters.FirstPerson;
using UnityEngine.SceneManagement;
```

You'll need these resources in just a moment. Add the following variable at the top of the script before the opening brace of the class:

```
public GameObject gameOverPanel;
```

Now, add these methods to the body of the class:

```
// 1
public void OnGUI()
{
    if (isGameOver && Cursor.visible == false)
    {
        Cursor.visible = true;
        Cursor.lockState = CursorLockMode.None;
    }
}

// 2
public void GameOver()
{
    isGameOver = true;
    Time.timeScale = 0;
    player.GetComponent<FirstPersonController>().enabled = false;
    player.GetComponent<CharacterController>().enabled = false;
    gameOverPanel.SetActive(true);
}

// 3
```