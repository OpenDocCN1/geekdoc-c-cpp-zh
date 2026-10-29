
## Part VI: Advanced Modeling

## FIGURE 29.6

Hair can be styled by changing the position and orientation of the guide hairs.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_813_0.png)

## Using hair presets

If you have a specific set of parameters that create a unique hair look that you're happy with, you can save it using the Save presets button in the Tools rollout. Hair preset files are rendered on the spot and added to the Hair and Fur Presets dialog box, shown in Figure 29.7. To add a preset configuration to the current object, simply double-click it.

In addition to presets, hairdos—created by styling the hair—also can be copied and pasted onto other hair selections.

### Tip

If you ever get into trouble styling hair, you can click the Regrow Hair button in the Tools rollout to reset all the styling to its original state.

## Using hair instances

Although the default hair looks great, if you ever wanted to replace the hair splines with an instanced geometry, you can do so by using the Pick Instance Node in the Tools rollout. The X button to the right of the Instance Node Pick button is used to remove the instance. Figure 29.8 shows a funny head created using a matchstick for a hair instance.

## Chapter 29: Adding and Styling Hair and Fur, and Using Cloth

## FIGURE 29.7

The Hair and Fur presets dialog box shows rendered thumbnails of the available presets.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_814_0.png)

### Tip

Be sure to adjust the Hair Count value before selecting an instanced object. Complex instanced objects should be used only with manageable numbers.

## FIGURE 29.8

Mr. Matchstick head has all his hair replaced with matchsticks, an instance.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_814_1.png)

## Part VI: Advanced Modeling

## Rendering Hair

You can change the hair render settings by opening the Effects panel using the Rendering → Effects menu. The Render Settings button in the Tools rollout provides quick access to the Effects panel. The Hair and Fur rollout includes settings for the Hairs and Lighting rendering methods.

Hairs can be rendered using three options. The Buffer method renders each hair individually and combines the effect. It uses minimal memory requirements. When the buffer method is selected, you can choose the Raytrace Reflections/Refractions option for better quality. The Geometry method converts each hair into a geometry object that is rendered. The mr Prim method renders hair using the mental ray renderer. For this option, you can set the Voxel Resolution used to render hairs.

### Cross-Ref

> More on mental ray is covered in Chapter 47, “Rendering with mental ray.”

Motion Blur can be enabled to make hairs that are moving fast appear blurred. The Oversampling setting adds an anti-aliasing pass to the rendering. The options include Draft, Low, Medium, High, and Maximum. The Composite Method option depends on the rendering method that is selected. A list of occlusion objects and a setting for Shadow Density also are available.

By default, all lights (except for direct lights and daylight systems) are used to light hair, but if a spotlight is added to the scene, you can select the spotlight and click the Add Hair Properties button at the bottom of the Hair and Fur rollout. This adds a Hair Light Attributes rollout to the Modify panel for the selected spotlight where you can set the Resolution and Fuzz of the shadow map for the hair object cast by the light.

## Understanding Cloth

If you drop a shirt over a chair, how does it land? It folds and bunches as it drapes over the solid object. Also notice how different types of cloth drape differently. Compare how silk reacts verses a terry cloth towel. Being able to accurately simulate how cloth reacts to scene objects and forces is yet another critical element that can really make a difference in your final scenes.

Cloth in Max is created using a modifier. This modifier can be applied to any object to make it a cloth object, or you can specifically create a set of clothes using the Garment Maker modifier. During the process of making an object into a cloth object, the object is divided into multiple faces using one of several subdivision methods. This provides the mesh with enough resolution to be deformed accurately.

Cloth objects are endowed with characteristics that let them respond to external forces within the scene including gravity, wind, and collisions with other scene objects. After all the scene objects, forces, and cloth objects are added to the scene, you can start a simulation that defines how the cloth moves within the scene under the effect of the other scene objects and forces.

### Cross-Ref

> This chapter focuses on creating and defining cloth objects. The dynamic nature of cloth is covered in Chapter 44, “Animating Hair and Cloth.”

## Creating Cloth

When you start to model a cloth object, keep in mind that the model must have enough resolution so that it can accurately fold over itself several times. If the resolution isn't defined enough, then the bending of the cloth is not believable.

### Note

Although dynamic cloth can be deformed under the effect of forces applied to it, cloth cannot apply a force back against the deforming object. This is a scenario that reactor can handle because it deals with all objects in the scene. A trampoline, for example, is a good example of a deformable cloth surface that can apply a force back on the deforming object using reactor.

You can increase the resolution of a model in several ways. The Garment Maker modifier includes parameters that can increase the resolution of a mesh, or you can use the HSDS (for Hierarchical SubDivision Surfaces) modifier to increase an object's resolution.

### Tip

When making cloth objects, use a single-sided Plane object instead of a Box object. Using a Box object needlessly doubles the number of polygons to be included in the simulation.

## Using Garment Maker to define cloth

Clothes can be added to models using a method that is similar to the way real clothes are made. Each section of cloth, called a panel, is outlined using lines and splines in the Top viewport. Clothes patterns also can be imported and used. Include a break at each corner of the panel or the modifier will round the corner. After you have all the various panels created, convert one of the panels to an Editable Spline object and attach all the panels into a single object. You can apply the Modifiers ▸ Cloth ▸ Garment Maker to the set of panels.

### Tip

The easiest way to create cloth panels is to draw the entire cloth panel and then use the Break Vertex command in Vertex subobject mode to break each corner.

When the Garment Maker modifier is first applied, the panel outlines are made into mesh objects and subdivided using the Delaunay algorithm, as shown in Figure 29.9. This algorithm uses random triangulation and divides the triangles into roughly equal shapes. This helps keep the cloth from folding along common lines caused by regular patterns. You can alter the number of polygons in the subdivided mesh using the Density value. If the Auto Mesh option is disabled, then you can update the density change using the Mesh It button. The Preserve option maintains the 3D shape of the object. If Preserve is disabled, then the panel is made flat.

## FIGURE 29.9

The Garment Maker modifier uses the Delaunay algorithm for subdividing cloth meshes.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_817_0.png)

The next step is to position the panels so they surround the model that they will be draped over. The subject that is to receive the clothes can be selected by clicking the Figure button in the Main Parameters rollout. After an object is selected, clicking the Mark Points on Figure button makes a small figure outline appear in the upper-left corner of the viewport. This figure outline has markers corresponding to the chest, neck, pelvis, shoulder, and wrists. Dragging over the body of the character lets you mark corresponding locations on the character.

After body parts are marked, you can select a cloth panel and use the Panel Position buttons in the Panel rollout to position the various cloth panels around the body. The Panel Position buttons include Front Center, Front Right, Back Center, Right Arm, and so on. You also can position the panels manually.

The Garment Maker modifier has three subobjects: Curves, Panels, and Seams. With the panels in place, you can stitch seams between the panels using the Curves subobject mode for flat drawn panels or with the Seams subobject mode for panels that are positioned about a model. Each seam edge should be relatively the same length. The Seam Tolerance value sets how far apart the two edges can deviate. For each seam, you can set a Crease Angle and Strength. The Sewing Stiffness value determines the strength that the seams are pulled together.

After the seams are defined, you can apply the Modifiers ▸ Cloth ▸ Cloth modifier to pull the panels together and simulate the cloth’s motion.
