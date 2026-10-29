from a certain selection of a mesh, such as a dragon's mouth or the end of a fire hose. The other options in the PArray system's Basic Parameters rollout are the same as in the other systems.

The Particle Generation rollout includes a Divergence value. This value is the angular variation of the velocity of each particle from the emitter's normal.

# Splitting an object into fragments

The Particle Type rollout for the PArray system contains a unique particle type: Object Fragments. This type breaks the selected object into several fragments. Object Fragment settings include a Thickness value. This value gives each fragment a depth. If the value is set to 0, the fragments are all single-sided polygons.

Also in the Particle Type rollout, the All Faces option separates each individual triangular face into a separate fragment. An alternative to this option is to use the Number of Chunks option, which enables you to divide the object into chunks and define how many chunks to use. A third option splits up an object based on the smoothing angle, which can be specified.

In the Material section of the Particle Type rollout, you can select material IDs to use for the fragment's inside, outside, and backside.

The Load/Save Presets rollout includes a host of interesting presets, including the likes of Blast, Disintegrate, Geyser, and Comet.

# Tutorial: Creating rising steam

In this tutorial, you create the effect of steam rising from a street vent. Using the PArray particle system, you can control the precise location of the steam.

To create the effect of steam rising from a vent, follow these steps:

+   1. Open the Street vent.max file from the Chap 41 directory on the DVD. This file includes a street scene with a vent. The car model was created by Viewpoint Datalabs.
+   2. Select the Create > Particles > PArray menu command, and drag in the Front viewport to create the system.
+   3. In the Basic Parameters rollout, click the Pick Object button and select the Quadpatch object that is positioned directly beneath the vent object. Set the Particle Formation option to Over Entire Surface.
+   Because the Plane object only has a single face, the particles travel in the direction of the Plane's normal.
+   4. In the Particle Generation rollout, set the Emit Stop value to 100 and the Life value to 60 with a Variation of 50. Set the Particle Size value to 5.0 with a Variation of 30.
+   5. In the Particle Type rollout, select the Standard Particles and the Constant Particles options.
+   6. Open the Material Editor (by selecting the M key), and name the selected sample slot steam. Click the map button to the right of the Opacity value, and double-click the Mask map type from the Material/Map Browser. In the Mask Parameters rollout, click the map button and select the Noise map type. Then click the Go to Parent button to return to the Mask map, click the Mask button, and select the Gradient map type. For the Gradient material, drag the black color swatch to the white color swatch, select Swap in the dialog box that appears, and enable the Radial option. Finally, drag the steam material to the PArray icon.

Figure 41.16 shows the steam vent at frame 60.