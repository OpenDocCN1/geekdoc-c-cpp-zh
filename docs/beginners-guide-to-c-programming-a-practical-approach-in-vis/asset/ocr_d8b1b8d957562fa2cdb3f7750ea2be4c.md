![](bbox=[0.07, 0.11, 0.9, 0.49])

Figure 16.73. The score decreases as the RobotBoy touches monsters

We can now increase and decrease the score, great. Now, let’s implement the code that will restart the level when the RobotBoy falls of the platform, in other words when the RobotBoy touches the ground. Firstly, add the required namespace by the code line using UnityEngine.SceneManagement. Then add the following code inside the OnCollisionEnter2D method which checks if the touched object is the ground:

```
if (objectTag == "ground")
{
SceneManager.LoadScene(SceneManager.GetActiveScene().name);
}
```

Code 16.6

The code line inside the condition statement reloads the scene resetting the score.

We displayed the score in the Console window using the print() method until now. However, when we distribute this game as a .exe file, the player will not play it inside the Unity but as a standalone program which won’t have a Console. Therefore, it is important to show the score on the scene. The values can be displayed in a UI Text on the scene.