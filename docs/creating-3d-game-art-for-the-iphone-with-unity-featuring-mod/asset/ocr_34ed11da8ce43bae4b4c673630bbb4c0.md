Ultimately, it’s best practice to think of Unity’s scale in terms of the arbitrary game unit you set for your projects. For instance, I set my game projects to have a scale of 1 game unit equal to 1 m. So in Unity iOS, 1 grid square is equal to 1 unit. In modo, I create my objects, as 1 grid square is equal to 1 unit to match my projects game unit scale. However, this means when working with modo and Unity iOS, your modo meshes will need to be scaled by 0.01 in Unity’s Importing Assets Settings via the Mesh Scale Factor due to the differences in which the Unity iOS and modo internally work with scale as shown in Fig. 2.6.

![](bbox=[0.106, 0.302, 0.94, 0.694])

FIG 2.6 Notice that the Mesh Scale Factor Defaults to 0.01, and the Imported 1 × 1 × 1 Modo Cube Matches a Default 1 × 1 × 1 Unity iOS Cube.

You can either choose to scale the mesh in modo before export, thus not having to scale it in the import settings within Unity iOS, or simply scale the mesh by 0.01 in the import settings within Unity iOS. I prefer to scale the modo mesh in Unity’s import settings, which allows me to work in meters within modo. By doing this, I don’t have to worry about freezing scale in modo before export and sending my mesh over to Blender works better as we’ll discuss in Chapter 5.

In modo’s Preferences, under Accuracy and Units, I set the Unit System to Game Units and then set the Meters per Game Unit to 1.0. This means that every grid square in modo will be 1 game unit and will represent 1 m, which is what I am considering my Unity iOS units to be equal to as shown in Fig. 2.7.