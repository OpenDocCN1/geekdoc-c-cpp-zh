# Unity Games by Tutorials

# Chapter 18: Making A Tower Defense Game

![](bbox=[0.273, 0.089, 0.727, 0.255])

There are just two fields that need some setup: **Game Win Sound** and **Game Lose Sound**. In the **Project** view, open the **Sound FX** folder to see all the sound effects present in the project:

![](bbox=[0.376, 0.339, 0.624, 0.466])

Drag **GameWin** to the **Game Win Sound** field and drag **GameLose** to **Game Lose Sound.**

![](bbox=[0.193, 0.536, 0.807, 0.735])

Now that the **GameManager** is in place, there are a few scripts that need to be modified to use its features. Open the **WaveManager** script (**Scripts > Game > Enemy > Wave**) and add this inside the `SearchForWave()` method, right under `spawnCounter = 0;`

```
GameManager.Instance.waveNumber++;
```

raywenderlich.com

528