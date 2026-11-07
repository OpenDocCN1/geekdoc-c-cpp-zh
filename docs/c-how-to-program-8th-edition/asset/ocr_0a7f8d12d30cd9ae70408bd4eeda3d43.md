+   - We must have the preprocessor directive to include the `OgreAL.h` header.
+   - Sound is the OgreAL object that contains the sound data. Use the `createSound` function of class `SoundManager` to create sounds. There can be only one `SoundManager`.
+   - The `createSound` function takes three parameters. The first is an `Ogre::String` that will be the name of the Sound within the OgreAL system. The second is the name of the sound file associated with the sound. The third is a bool that determines whether the Sound should be looped to continue playing. Passing false will play the Sound through once, then stop. Passing true will continuously loop the sound until you stop it.
+   - Attach the Sound to a node with the `attachObject` function.
+   - Each Sound must have a unique name.
+   - A Sound must finish playing before it can be played again.

# Section 27.4.8 Resources

+   - All of the resources must be loaded before we can use them.
+   - Use a `ResourceGroupManager` to manage the game’s resources.
+   - The `addResourceLocation` function takes three `Ogre::String` arguments. The first is the location of the resources. The second is the type of file the resources are in. The third is the resource group these files belong to.

# Section 27.4.9 Pong Driver

+   - Ogre supports various platforms, so you should try not to write platform-specific code when you can avoid it.

# Terminology

| Terminology | Reference | Terminology | Reference |
|---|---|---|---|
| 3D graphics engine | CLIX | KeyListener class | CLXXXVII |
| 3D model | CLX | levels of detail (LoD) | CLXI |
| 3D modeling tool | CLX | Light class | CLXXIII |
| 3D sound | CLXII | local space | CLXXXVI |
| alpha channel | CLX | material | CLIX |
| ambient light | CLXI | mesh | CLXXIV |
| Camera class | CLXXIII | metrics model | CLXXXIII |
| collision detection | CLXI | normal | CLXXIX |
| color | CLX | Object Oriented Input System (OIS) | CLXXXVI |
| color depth | CLXXI | Ogre (Object-oriented Graphics Rendering Engine) | CLIX |
| culling | CLXXII | OgreAL | CLXIII |
| diffuse light | CLXI | OpenAL audio library | CXCIII |
| Direct3D | CLX | OpenGL | CLX |
| Directional lights | CLXXIII | Overlay class | CLXXXIII |
| emissive light | CLXI | OverlayContainer class | CLXXXIII |
| Entity class | CLXXIV | PanelOverlayElement class | CLXXXIII |
| export 3D models | CLX | parent space | CLXXXVI |
| frame | CLXII | pixel mode | CLXXXIII |
| FrameEvent class | CLXXXVI | Point light | CLXIII |
| FrameListener class | CLXXXVI | relative mode | CLXXXIII |
| Keyboard class | CLXXXVII |  |  |
| KeyEvent class | CLXXXVII |  |  |