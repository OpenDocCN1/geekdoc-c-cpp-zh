
![](img/d3e3fa4010906e98ec76be003a6e31c2_257_0.png)

**FIG A.3** Here you can see early concepts that Warner worked upon from my original sketch, this was in the “Bob” stage.

![](img/d3e3fa4010906e98ec76be003a6e31c2_257_1.png)

**FIG A.4** Here is a concept sketch I gave to Warner with a rough idea of Thumper.

![](img/d3e3fa4010906e98ec76be003a6e31c2_257_2.png)

**FIG A.5** At this point, Bob has transformed into Tater. Here are some character sketches that Warner produced. You can really see that Tater is beginning to take shape.

**FIG A.6** Here is a color scheme for Tater that I gave to Warner. The “77” on the jersey is my birth year.

![](img/d3e3fa4010906e98ec76be003a6e31c2_258_0.png)

**FIG A.7** Warner sent me the character turns that I could use as backdrop items in modo for modeling.

### Tater

![](img/d3e3fa4010906e98ec76be003a6e31c2_258_1.png)

Tater Character Turns

**FIG A.8** Here, we began to work on the cover. Since I am not an illustrator, it was easier for me to take some photos of myself in the poses I was wanting for Tater. You can see here that the middle photo is what we used.

![](img/d3e3fa4010906e98ec76be003a6e31c2_258_2.png)

![](img/d3e3fa4010906e98ec76be003a6e31c2_259_0.png)

**FIG A.9** Here is a preliminary sketch for the key pose. You can see that we were still working on designing Thumper.

![](img/d3e3fa4010906e98ec76be003a6e31c2_259_1.png)

**FIG A.10** This image shows some Thumper refinements.

**FIG A.11** This image shows the key pose and the refined Thumper design.

![](img/d3e3fa4010906e98ec76be003a6e31c2_260_0.png)

**FIG A.12** Here is the final illustration that Warner created.

![](img/d3e3fa4010906e98ec76be003a6e31c2_260_1.png)

### Developing the Menu

In this section, you can see the menu screens that were developed for the game. Tater is a character from my personal game project called "Dead Bang." The Dead Bang world is grungy, so I wanted to bring this style into the look of the book's companion app. To create the actual in-game menu system, I used EZ GUI from Above and Beyond Software, which can be found at http://www.anbsoft.com/middleware/ezgui/. EZ GUI is a great system for developing GUI elements and menus for your game, as it allows you to lower the draw calls for your GUI elements by utilizing texture atlases and shared materials. I also heavily relied on iTween, which was created by Bob Berkebile. The iTween library is a rich animation system that can be used to create various animation effects ranging anywhere from the simple to complex. It is a great time saver, and it was used to animate the buttons in my menu. You can find more info on iTween at http://itween.pixelplacement.com/index.php.

![](img/d3e3fa4010906e98ec76be003a6e31c2_261_0.png)

**FIG A.13** This is an early version of the menu system. Most of the elements are there, but at this point, I was still exploring the overall style.

![](img/d3e3fa4010906e98ec76be003a6e31c2_261_1.png)

**FIG A.14** This is the final background for the menu system. It is important to always explore your concepts and designs thoroughly.

![](img/d3e3fa4010906e98ec76be003a6e31c2_262_0.png)

**FIG A.15** This image shows the menu system scene that utilizes EZ GUI. Here you can see the panels that were created for each menu option as well as the game rendered in the Game View.

![](img/d3e3fa4010906e98ec76be003a6e31c2_263_0.png)

**FIG A.16** Here are the menu buttons. By using EZ GUI, these meshes share a texture atlas and material and thus are only 1 draw call.

![](img/d3e3fa4010906e98ec76be003a6e31c2_263_1.png)

**FIG A.17** This image shows the loading screen menu that is called before the actual game play screen is called. This image contains only 1 sprite and loads either the iPhone 4 or iPhone scene depending on the value that is held in a Global Variable called eHD.

### The Game Play Scene

In this section, you can see various elements from the game play scene. In the video walk-through for the app, I will explain exactly how the app was created, which will also cover the coding of the game as well. I created two scenes to support the different resolution of the iPhone 4 and older iDevice generation. The device the user is running the app on determines the appropriate scene to load. It captures this device information in a Static Class and is used throughout the game.

**FIG A.18:** This is the full scene for the standard definition version.

![](img/d3e3fa4010906e98ec76be003a6e31c2_264_0.png)

**FIG A.19:** In this image, you can see the usage of Beast lightmapping in the scene. Here, you can see that I am checking the resolution of the light-map as it is denoted by the overlaid checker pattern.

![](img/d3e3fa4010906e98ec76be003a6e31c2_264_1.png)

![](img/d3e3fa4010906e98ec76be003a6e31c2_265_0.png)

**FIG A.20:** Here is the Prefab for my scene props. This Prefab is distributed randomly around the trash yard by simply copying and pasting elements. Each copy is batched.

![](img/d3e3fa4010906e98ec76be003a6e31c2_265_1.png)

**FIG A.21:** Tater's weapon is not part of the Tater mesh. Instead it is parented at run-time using a script. This gives me the flexibility to add new weapons in game i.e., the user picks up a new weapon.

![](img/d3e3fa4010906e98ec76be003a6e31c2_266_0.png)

**FIG A.22** This is the actual script that is used to parent the gun to Tater's hand bone.

![](img/d3e3fa4010906e98ec76be003a6e31c2_266_1.png)

**FIG A.23** To create a shadow for Tater, I did not use a Projector. Instead I created a simple transparent sprite that was parented to the Tater.

![](img/d3e3fa4010906e98ec76be003a6e31c2_267_0.png)

**FIG A.24** The target was also made into a Prefab. It consists of several small mesh items, a baked animation and Colliders. There is also a script on the target, which when hit, dispatches a message to play the attached animation for the FBX fake file and instantiate a particle prefab for the explosion at the position of that target.

![](img/d3e3fa4010906e98ec76be003a6e31c2_267_1.png)

**FIG A.25** This image shows the explosion that is created by the instantiated particle emitter.

![](img/d3e3fa4010906e98ec76be003a6e31c2_268_0.png)

**FIG A.26** This image shows the actual particle emitter that was used to create the explosion effect.

![](img/d3e3fa4010906e98ec76be003a6e31c2_268_1.png)

**FIG A.27** To create the muzzle flash, I parented a GameObject, which consisted of three transparent sprites to the tip of Thunder. By default, the Mesh Renderer is disabled. When the user hits the fire button, a script toggles the Mesh Renderer for the muzzle flash to on. A coroutine is used to turn the muzzle flash Mesh Renderer off.

![](img/d3e3fa4010906e98ec76be003a6e31c2_269_0.png)

**FIG A.28** Here, you can see the gate Prefab. This Prefab uses a transparent lightmapped shader that uses alpha testing.

### Game Play Controls

A vital aspect of any game is the controls. Programming a control system can be a very complex task, which, depending on your system, can take lots of time to correctly implement. Instead of trying this venture on my own, I turned to the Tornado Twins and UnityPrefabs.com at http://www.unityprefabs.com/. I, Efraim Meulenberg, founder of UnityPrefabs.com graciously provided me with the 3rd Person Camera Kit Prefab for the book. UnityPrefabs.com Prefabs are not only amazing quality assets, but easily integrate into your own projects. By utilizing their 3rd Person Camera Kit Prefab, I was able to concentrate on the control’s graphic elements and bypass the coding altogether, not to mention save tons of valuable time on the project.

![](img/d3e3fa4010906e98ec76be003a6e31c2_269_1.png)

**FIG A.29** This image shows the control scheme from the UnityPrefabs.com 3rd Person Camera Kit Prefab that I re-skinned to match my game style. It was extremely easy to configure the Prefab as well as replace the graphics.

## Index

Page numbers followed by f indicate a figure and t indicates a table.

- **A**
  - Animating Tater, 139-152
    - in Blender, 143-152
      - cyclic animation, 145-149
      - exporting FBX, 149-152
      - using actions, 144, 144f
  - Unity's animation data works, 142-143
    - keyframe compression and reduction, 143f
    - reuse animations on different characters, 143, 144f
    - using FBX, 140-142
      - multiple clips versus one clip per file, 140-142
  - Animation Clips, 141
  - ARM central processing unit (CPU), 2-7

- **B**
  - Batching, 5-7
    - dynamic batching, 5-6
    - Static batching, 6-7
  - Beast, 189
  - Beast Lightmapping, 189-209, 189f
    - adjusting lightmaps, 203-209
    - adding grime to maps, 206-209
    - color grading maps, 204-206
    - autogenerate UVs, 192
  - Beast and HDR, 190
  - Beast settings, 200-203
    - custom settings, 201-203
    - lightmap UVs, 190-191
    - process of lightmapping, 192-198
    - using dual lightmaps, 198
  - Blender
    - platforms, 91
    - rotation order for objects in, 142f
    - timeline with different animations, 140f
  - Blender 2.5, 91, 98
  - Blender animation
    - IK animation, 119-139
    - arm setup, 131-135
    - bones used for twisting body, 125f
    - controls for feet, 121f
    - controls for rig, 120f
    - creating master control, 136
    - elbow bone, 123f
    - fixing rotations, 135-136
    - foot bone used to raise heel, 122f
    - knee controls, 123f
    - leg setup, 124-131
    - pelvis bone used to control hips, 125f
    - shoulder shrugging, 124f
    - toe bone used to articulate toes, 122f
    - tweaking weight maps, 137-139
    - using bone layers, 137
    - matching object size, 92-94
    - skinned meshes in Unity, 96-99
    - VP-optimized skinning, 96-98
  - Unity Blender support and FBX workflow, 94-95
    - using FBX, 94-95
  - Budget rendering
    - texture budget, 17
    - vertex budget, 17
  - Building on grid, 77

- **C**
  - Clean Weight tool, 101, 102f, 115, 116f
  - CNTRL_Foot, 124, 126f
  - Col Game Property, 178, 179f
  - Creating game level, 74-86
  - CrossFade("shoot"), 167
  - Cyclic animation, 145-149
    - first and last keyframes, 146f
  - FPS Calculate, 147, 147f
  - frame rate in Blender, 145f
  - hold keyframes, 147, 148f, 149f
  - keyframing location and rotation, 147f
  - run cycle for Tater, 148f

- **D**
  - Dead Bang game, 15, 67
  - Degenerate triangles, 30, 30f
    - triangle strip, 30, 30f. See also Zero-angle triangles
  - Diffuse map, 57-64
    - faking light and shadow, 57-58
    - Unity 3 OpenGL ES 2.0 Shaders, 58
    - texturing Tater, 58-64
    - adding wear and tear, 62-64
    - building up volume through shading, 61-62
    - creating hair, 62
    - reference images, 59-60
    - skin textures, 60-61
  - Discontinuous UVs, 31
  - Dynamic batching, 5-6
  - Dynamics in Blender to animate objects, 169-185
    - setting up Rigid Body Dynamics, 170-184
    - baking simulation, 179-183
    - editing animation with NLA Editor, 183-184
    - importing into Blender, 171-178
    - setting up logic, 178-179

- **F**
  - FBX
    - exporting, 149-152
    - baking keys, 150-151
    - disabling optimize keyframes and selected objects, 152
    - setting Frame Range, 150
    - using, 140-142
      - multiple clips versus one clip per file, 140-142

- **G**
  - Game textures, fundamentals of, 50-57
    - multiple resolutions, 55
    - texture budget, 55-57
    - texture compression:
      - PVRTC, 53-55
      - using Texture Importer Dialog, 54, 54f
    - texture formats, 50
      - format in importing assets dialog within Unity, 50, 50f
