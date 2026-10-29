
Figure 42.10 shows the icons for each of these Space Warps. All the P-type deflectors are in the first column, the S-type deflectors are in the second column, and the U-type deflectors are in the third column.

**Tip:** When you use deflector objects, the number of polygons makes a big difference. The deflector object uses the normal to calculate the bounce direction, so if the deflector object includes lots of polygon faces, then the system slows way down. A solution to this, especially if you're using a simple plane deflector, because all its polygon normals are the same anyway, is to use a simplified proxy object as the deflector and hide it so the particles look like they are hitting the complex object.

**Figure 42.10:** The Deflector Space Warps: POmniFlect, SOmniFlect, UOmniFlect, PDynaFlect, SDynaFlect, UDynaFlect, Deflector, SDeflector, and UDeflector

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1096_0.png)

**Note:** The PDynaFlect, SDynaFlect, and UDynaFlect space warps allow the particles that strike the deflector object to exert a force on the deflector, but this force is detected only when the Dynamics utility is used to create a dynamic simulation. If a dynamic simulation is included, then the deflectors act just like the OmniFlect deflectors. Given that reactor is much more powerful and helpful than the Dynamics utility, it is recommended that the OmniFlect deflectors be used instead of these DynaFlect deflectors, as the DynaFlect deflectors require more memory and are slower to respond than their OmniFlect counterparts.

## POmniFlect, SOmniFlect, and UOmniFlect

The POmniFlect Space Warp is a planar deflector that defines how particles reflect and bounce off other objects. The SOmniFlect Space Warp is just like the POmniFlect Space Warp, except that it is spherical in shape. The UOmniFlect Space Warp is another deflector, but this one can assume the shape of another

## Deflector, SDeflector, and UDeflector

The Deflector and SDeflector Space Warps are simplified versions of the POmniFlect and SOmniFlect Space Warps. Their parameters include values for Bounce, Variation, Chaos, Friction, and Inherit Velocity. The UDeflector Space Warp is a simplified version of the UOmniFlect Space Warp. It has a Pick Object button for selecting the object to act as the deflector and all the same parameters as the SDeflector Space Warp.

## Geometric/Deformable Space Warps

You use Geometric/Deformable Space Warps to deform the geometry of an object. Space Warps in this subcategory include FFD (Box), FFD (Cyl), Wave, Ripple, Displace, Conform, and Bomb. These Space Warps can be applied to any deformable object. Figure 42.12 shows the icons for each of these Space Warps.

**Figure 42.12:** The Geometric/Deformable Space Warps: FFD (Box), FFD (Cyl), Wave, Ripple, Displace, Conform, and Bomb

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1098_0.png)

### FFD (Box) and FFD (Cyl)

The FFD (Box) and FFD (Cyl) Space Warps show up as a lattice of control points in the shape of a box and a cylinder; you can select and move the control points that make up the Space Warp to deform an object that is bound to the Space Warp. The object is deformed only if the bound object is within the volume of the Space Warp.

These Space Warps have the same parameters as the modifiers with the same name found in the Modifiers > Free Form Deformers menu. The difference is that the Space Warps act in World coordinates and aren't tied to a specific object. This allows a single FFD Space Warp to affect multiple objects.

**Cross-Ref:** To learn about the FFD (Box) and FFD (Cyl) modifiers, see Chapter 11, “Introducing Modifiers and Using the Modifier Stack.”

To move the control points, select the Space Warp object, open the Modify panel, and select the Control Points subobject, which lets you alter the control points individually.

### FFD Select modifier

The FFD Select modifier is another unique selection modifier. It enables you to select a group of control point subobjects for the FFD (Box) or the FFD (Cyl) Space Warps and apply additional modifiers to the selection. When an FFD Space Warp is applied to an object, you can select the Control Points subobjects and apply modifiers to the selection. The FFD Select modifier lets you select a different set of control points for a different modifier.

### Wave and Ripple

The Wave and Ripple Space Warps create linear and radial waves in the objects to which they are bound. Parameters in the rollout help define the shape of the wave. Amplitude 1 is the wave's height along the X-axis, and Amplitude 2 is the wave's height along its Y-axis. The Wave Length value defines how long each wave is. The Phase value determines how the wave starts at its origin. The Decay value sets how quickly the wave dies out. A Decay value of 0 maintains the same amplitude for the entire wave.

The Sides (Circles) and Segments values determine the number of segments for the X- and Y-axes. The Division value changes the icon's size without altering the wave effect. Figure 42.13 shows a Wave Space Warp applied to a simple Box primitive. Notice that the Space Warp icon is smaller than the box, yet it affects the entire object.

**Figure 42.13:** The Wave and Ripple Space Warps applied to a patch grid object

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1099_0.png)

**Note:** Be sure to include enough segments in the bound object, or the effect won't be visible.

### Tutorial: Creating pond ripples

For this tutorial, you position a patch object so it aligns with a background image and apply the Ripple Space Warp to it.

To add ripples to a pond, follow these steps:

- 1. Open the Pond ripple.max file from the Chap 42 directory on the DVD.
   This file includes a background image of a bridge matched to a patch grid where the pond is located with a reflective material assigned to it.

**Tip:** If you're having trouble locating the patch grid, press F3 to switch to Wireframe mode.

- 2. Select the Create > Space Warps > Geometric/Deformable > Ripple menu command. Drag in the Perspective view to create a Space Warp object. In the Parameters rollout, set the Amplitudes to 2 and the Wave Length to 30.

- 3. Click the Bind to Space Warp button, and drag from the patch object to the Space Warp.

Figure 42.14 shows the resulting image.

**Figure 42.14:** A ripple in a pond produced using the Ripple Space Warp

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1100_0.png)

### Conform

The Conform Space Warp pushes all object vertices until they hit another target object called the Wrap To Object, or until they've moved a preset amount. The Conform Parameters rollout includes a Pick Object button that lets you pick the Wrap To Object. The object vertices move no farther than this Wrap To Object.

You can also specify a Default Projection Distance and a Standoff Distance. The Default Projection Distance is the maximum distance that the vertices move if they don't intersect with the Wrap To Object. The Standoff Distance is the separation amount maintained between the Wrap To Object and the moved vertices. Another option, Use Selected Vertices, moves only a subobject selection.

**Cross-Ref:** The Conform Space Warp is similar in function to the Conform compound object that is covered in Chapter 27, “Working with Compound Objects.”

Figure 42.15 shows some text being deformed with the Conform Space Warp. A warped quad patch has been selected as the Wrap To object.

**Figure 42.15:** The Conform Space Warp wraps the surface of one object around another object.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_1101_0.png)

### Bomb

The Bomb Space Warp causes an object to explode from its individual faces. The Strength value is the power of the bomb and determines how far objects travel when exploded. The Spin value is the rate at which the individual pieces rotate. The Falloff value defines the boundaries of faces affected by the bomb. Object faces beyond this distance remain unaffected. You must select Falloff On for the Falloff value to work.
