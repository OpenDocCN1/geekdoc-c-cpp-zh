The game controller for this game is created dynamically by the LevelSetup script component attached to the empty gameObject named LevelSetup. The actual script will be broken down later in this chapter, but the basic function of the script is to check whether a game controller exists in the scene and, if not, to instantiate one. It references two prefs, called GameController and one SceneManager.

By creating the game controller and scene manager objects dynamically, these objects can exist across different game levels. The level setup script first checks to see whether they exist, and if the game scene is a level other than the first, the objects will not be duplicated accidentally.

When the game controller prefab is instantiated, its gameObject looks like this, in the Hierarchy window of the Unity editor:

+   - GameController
  - GameCamera
    - BulletDestroyer
    - BulletDestroyer
    - Player_Parent_Object
    - StarsLayer1
      - StarsLayer1

+   - UI
  - GAMEO_GRAPHIC
  - GETREADY_GRAPHIC

It can be seen that the GameController prefab contains everything required for the game controller to function, create a player, and have a camera and UI available to use during the game. The prefabs contains the minimum amount required to run the game, the most important elements. With the exception of the LevelSetup gameObject in each game scene, everything else in the level scenes is specific to the level.

# 14.3 Prefabs

The prefabs used for this game are

+   - ENEMIES
  - EnemyShip_1
  - EnemyShip_2
  - EnemyShip_3
  - Gameboss