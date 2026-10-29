
## Chapter 45: Working with Advanced Lighting, Light Tracing, and Radiosity

### FIGURE 45.5

Use the Advanced Lighting panel in the Object Properties dialog box to disable advanced lighting.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1146_0.png)

### Tutorial: Excluding Objects from Light Tracing

Using the Object Properties dialog box, you can exclude certain objects from the light tracing calculations.

To exclude objects from the Light Tracer, follow these steps:

- 1. Open the Hotplate.max file from the Chap 45 directory on the DVD.
  This file includes a simple model of a hotplate.
- 2. Open the Advanced Lighting panel by selecting Rendering ⇨ Light Tracer (or press the 9 key). In the Parameters rollout, set the Bounces value to 2.
- 3. In the Front viewport, select the plug, cord, and floor objects, and then select Edit ⇨ Object Properties to open the Properties dialog box for these objects. In the Object Properties dialog box, open the Advanced Lighting panel and enable the Exclude from Advanced Lighting Calculations option. Then click OK.
- 4. In the Render Scene dialog box, click the Render button.
  This renders the scene in the Rendered Frame Window.

Figure 45.6 shows the scene rendered with advanced lighting that excludes certain objects.

### FIGURE 45.6

Color bleeding becomes much stronger with a higher Bounce value.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1147_0.png)

### Understanding Radiosity

Imagine a scene that includes an umbrella with a light source directly overhead. If you rendered the scene, the object caught in the umbrella's shadow would be too dark for you to see clearly. To fix this situation, you would need to add some extra lights under the umbrella and set them to not cast shadows. Although this workaround provides the solution you want, it is interesting to note that this isn't the case in real life.

The difference between the workaround and real life has to do with the effect of light energy being reflected (or bounced) off the lit objects. It is this phenomenon that allows me to look down the hall and see whether my children's light is still on past bedtime. Even though I can't see the light directly, I know it is on because of the light that reflects off the other walls.

Radiosity is a lighting algorithm that is based on how heat or energy transfers across surfaces. Every time a bit of light energy, called a photon, strikes a surface, the light energy is reduced, but the light energy is bounced onto the surrounding faces. The greater the number of bounces that are computed, the more realistic the lighting solution, but the longer it takes to compute. So, using radiosity, the objects under the umbrella are visible even if they are in the shadows. Because of the way the light is computed, radiosity solutions are not capable of generating direct specular highlights.

Radiosity is mostly used to light indoor scenes because that is where the effect of light bouncing is most evident. Radiosity, along with light tracing, is another method for computing global illumination. Figure 45.7 shows the dinosaur exhibit in a museum with and without radiosity. Notice how dark the shadows are in the normal lighting image.

### FIGURE 45.7

This scene is lighted using normal lighting (left) and radiosity lighting (right).

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1148_0.png)

### Lighting for radiosity

The Advanced Lighting panel in Max includes Light Tracing and Radiosity options. You can choose either option from the Advanced Lighting panel in the Render Scene dialog box. You can open this panel with the Radiosity option selected using the Rendering > Radiosity menu command. Pressing the 9 key opens the Render Scene dialog box with the Advanced Lighting panel open.

Radiosity lighting is not displayed until you have Max compute it by clicking the Start button in the Radiosity Processing Parameters rollout. After a radiosity solution is calculated, the results are saved as light maps. These maps are easy to apply to a scene and can be viewed within the viewports. However, when the geometry or lights of the scene change, you need to recalculate the lighting solution.

The Radiosity Processing Parameters rollout, shown in Figure 45.8, lets you set the quality of the radiosity solution. You also can specify the number of iterations to use for the scene and for the selected objects. These are different steps in the radiosity computation. The Initial Quality defines the accuracy of the rays that are bounced around the scene. This stage sets the brightness for the scene. The Refine Iterations improves the general quality of the lighting solution for each iteration. You can refine iterations only for the selected object. This lets you target the iterations instead of computing them for the entire scene.

The Interactive Tools section lets you specify a Filtering value. A greater Filtering value eliminates noise between adjacent surfaces by averaging the lighting coming from all surrounding surfaces. The Setup button offers access to the Exposure Control rollout in the Environment panel. You also can turn off radiosity in the viewports.

### Cross-Ref

Chapter 23, “Rendering a Scene and Enabling Quicksilver,” includes coverage of the Exposure Control rollout.

### Subdividing a mesh for radiosity

As you begin to play with radiosity, you’ll quickly find that to get accurate results, you need to have good, clean models. If any models have long, thin faces, then the results are unpredictable.

The Radiosity Meshing Parameters rollout includes an option to enable meshing and a Meshing Size value. This setting is the same as the Size value parameter for the Subdivide modifier, except that it is applied globally.

## Part XI: Advanced Lighting and Rendering

### FIGURE 45.8

The Radiosity Processing Parameters rollout includes buttons for computing a solution.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1149_0.png)

### Tip

If you're creating an indoor room using the Box object, be aware that Box objects have only one external face surface with normals, so the interior of a Box object will not have the correct lighting. You can easily fix this by applying the Shell modifier to the Box object. This adds an interior set of faces to the Box object.

### Using the Subdivide modifier

The Modifiers menu includes a submenu for Radiosity modifiers. This submenu includes only the Subdivide modifier and a World-Space version of the Subdivide modifier. This modifier accomplishes a simple task—creating a mesh that has regular, equally shaped triangular faces that work well when computing a radiosity solution.

### Tip

Although this modifier was created to help with radiosity solutions, it also helps with other commands that require regular mesh faces, such as the Boolean and Terrain compound objects.

The Parameters rollout includes a Size value that determines the density of the mesh. The lower the value, the denser the mesh and the better the resulting radiosity solution, but the longer the solution takes.

## Chapter 45: Working with Advanced Lighting, Light Tracing, and Radiosity

same Subdivision Size setting also can be found (and set globally) in the Radiosity Meshing Parameters rollout of the Advanced Lighting panel. It is also found in the Advanced Lighting panel of the Object Properties dialog box. Figure 45.9 shows a simple cube with the Subdivide modifier applied and the Size value set to (from left to right) 50, 30, 25, 20, and 12.

### Tip

If you drag the Size value, you'll probably want to set the Update option to Manual or you'll find yourself waiting while Max computes some seriously dense mesh, or you can just disable the Display Subdivision option.

### FIGURE 45.9

The Subdivide modifier changes all mesh faces into regularly shaped triangular faces.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1150_0.png)

### Tutorial: Preparing a mesh for radiosity

When it comes to meshes that have long, thin, and irregular faces, you don't have to look any further than Boolean compound objects. These objects typically are divided along strange angles, producing ugly meshes. The good news is that these meshes are easy to subdivide.

To subdivide an irregular mesh in preparation for a radiosity solution, follow these steps:

- 1. Open the Boolean object.max file from the Chap 45 directory on the DVD.
  This file includes two copies of a Box object with an arch shape Boolean subtracted from it.
- 2. Select the top object, and choose the Modifiers→ Radiosity Modifiers→ Subdivide menu command.
  This applies the Subdivide modifier to the object.
- 3. In the Parameters rollout, select the Manual update option, set the Size value to 5.0, and click Update Now.
  If the Display Subdivision option is enabled, then the changes are visible in the viewport.
- 4. Open the Advanced Lighting panel with the Rendering→ Radiosity menu command (or press the 9 key). Select Radiosity from the drop-down menu.

Figure 45.10 shows the two objects with and without the Subdivide modifier applied. The top object is ready for a radiosity solution.

### Painting with light

The Light Painting rollout (found in the Advanced Lighting panel of the Render Scene dialog box), shown in Figure 45.11, includes buttons for Adding Illumination, Subtracting Illumination, and Picking an Illumination value from the scene. Using these tools, you can paint lighting on the objects in the scene. The Clear button removes all the changes you've made using the Light Painting tool.
