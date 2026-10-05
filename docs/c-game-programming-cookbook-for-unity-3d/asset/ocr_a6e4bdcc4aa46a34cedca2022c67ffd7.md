+   - Player_Startpoints
  - StartPoint_1 (1–10)

+   - Players

+   - SoundController

+   - UI

+   - Game Over Graphic

+   - Get Ready Graphic

Note that the game controller dynamically creates players and enemies, when the game starts. References to several prefabs and gameObjects are set in the Unity Inspector window:

+   - The game controller references these prefabs and objects:

+   - Explosion prefab (a particle effect for explosions)

+   - StartPoints array containing a reference to the Startpoint_X gameObjects in the scene

+   - Player Prefab List array containing a reference to the Top_Down_Player prefab

+   - The BaseSoundController.cs script attached to the Sound Controller gameObject has an array called Game Sounds, containing references to

+   - shoot1

+   - explode2

+   - player_explode

+   - spawner 1

+   - The Spawn Controller gameObject has an instance of WaveSpawner.cs attached to it, with the following references in its Spawn Object Prefabs array:

+   - Spawn_Structure1

+   - Spawn_Structure2

+   - Spawn_Structure3