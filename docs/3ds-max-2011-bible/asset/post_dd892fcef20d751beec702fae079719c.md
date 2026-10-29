
## Part VI: Advanced Modeling

The order in which the operations are applied affects the result. You can reorder the operations in the list by selecting an operation, choosing its position in the list, and clicking the Reorder Ops button.

## Cross-Ref

You also can apply Boolean operations to shapes using the Boolean operators available for Editable Meshes in the Geometry rollout. Chapter 12, “Drawing and Editing 2D Splines and Shapes,” covers these 2D Boolean operators.

## FIGURE 27.25

The Insert operation only maintains closed volumes when subtracted.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_791_0.png)

The materials that get applied to a ProBoolean result can be set to use the Operand Material or to retain the Original Material. If you use the Operand Material with the subtraction operation, then the surface that touches the picked object retains the removed object's material, and the rest of the object has the original object's material. If the Retain Original Material option is selected, then the entire result gets the original object's material.

In the Advanced Options rollout are options for updating the scene and for reducing the complexity of the object. The Decimation value is the percentage of edges to remove from the result. If you plan on smoothing the object or converting it to an Editable Poly object, then you want to enable the Make Quadrilaterals option, which causes the polygon reduction to avoid triangles in favor of quads. You also can set the Quad Size, and you can select how planar edges are handled.

## Chapter 27: Working with Compound Objects

### Note

If you plan to deform the mesh as part of a skinned object or a cloth simulation, the resulting mesh has to be clean or the deformation will have problems.

### Tutorial: Creating a keyhole

What was it that Alice saw when she looked through the keyhole? The ProBoolean feature is the perfect tool for cutting a keyhole through a doorknob plate.

To use the ProBoolean object to create a keyhole, follow these steps:

- 1. Open the Doorknob.max file from the Chap 27 directory on the DVD.
- 2. Select the doorknob plate object positioned where the keyhole is, and choose the Create → Compound → ProBoolean menu command. In the Parameters rollout, select the Subtraction option.
- 3. In the Pick Boolean rollout, click the Start Picking button and select the Box and Cylinder objects positioned where the keyhole should be.

Figure 27.26 shows the finished keyhole.

## FIGURE 27.26

A keyhole built using the ProBoolean object

![](img/ebbb4844f027f7d1c580e48108d2b6cb_792_0.png)

## Using ProCutter

The original Boolean compound object included a Cut option. This feature has been replaced with ProCutter, which offers many more features than the original option. ProCutter allows you to cut a single object (known as the Stock object) with multiple cutter objects.

You can pick both the Stock and Cutter objects using the buttons found in the Cutter Picking Parameters rollout. You have four options with each selection: Reference, Move, Copy, or Instance. The Auto Extract Mesh option automatically replaces the selected stock object with the extracted result. The Explode by Elements option works only when the Auto Extract Mesh option is enabled. It separates each cut element into an object.

Within the Cutter Parameters rollout, you can select from three Cutting Options. The Stock Outside Cutter option keeps the portion of the stock object that is on the outside of the cutter. The Stock Inside Cutter option is the opposite, keeping the stock portion inside the cutters. The Cutters Outside Stock option maintains those portions of the cutters that are outside of the stock.

All selected cutters and stock objects are added to a list in the Cutter Parameters. Using the Extract Selected button, you can restore any cutter or stock object that has been operated on as a Copy or Instance. Materials and Decimation also work the same as for ProBoolean objects.

### Tip

The ProCutter features are helpful for dividing an object that will be animated exploding into pieces.

### Tutorial: Creating a jigsaw puzzle

The ProCutter is useful for creating destructive scenes such as shattering glass to pieces and breaking down buildings, but it also can be used for constructive cutting such as creating a jigsaw puzzle.

To use the ProCutter compound object to divide an object into a jigsaw puzzle, follow these steps:

- 1. Open the ProCutter puzzle.max file from the Chap 27 directory on the DVD. This file includes a simple box mapped with a scenic image and several extruded lines that mark the jigsaw puzzle's edges.
- 2. Select one of the extruded lines that mark where the cuts should be (known as a cutter), and choose the Create > Compound > ProCutter menu command.
- 3. Then, click the Pick Cutter Objects button and select all of the remaining cutter objects. In the Cutter Parameters rollout, enable the Stock Outside Cutter along with the Stock Inside Cutter options. Select the Retain Original Material option also.
- 4. In the Cutter Picking Parameters rollout, enable the Auto Extract Mesh and Explode By Elements options, then select the Pick Stock Objects button and choose the Box object in the viewport.
- 5. Open the Material Editor and drag the image material onto each puzzle piece.

### Note

If you don't want to see the cutter lines, you can select and hide them.

Figure 27.27 shows the final puzzle with one piece moved away from the others.

## FIGURE 27.27

A puzzle cut using the ProCutter compound object

![](img/ebbb4844f027f7d1c580e48108d2b6cb_794_0.png)

## Summary

Compound objects add several additional modeling types to your bulging modeling toolkit. From morph objects to complex deformed lofts, you can use these special-purpose types to model many different objects. This chapter covered these topics:

- The various compound object types
- Morphing objects with the same number of vertices
- Creating a Conform object with differing numbers of vertices
- Using splines and mesh objects to create a ShapeMerge object
- Creating a Terrain object using splines
- The Mesher object
- Using the BlobMesh object to simulate water
- Creating a Scatter object
- Creating a Connect object to join two objects
- Creating a Loft object

## Part VI: Advanced Modeling

- How to control Loft parameters
- Using Loft deformations
- Modifying Loft subobjects
- Comparing the strengths of Loft objects versus surface tools
- Modeling with the ProBoolean and ProCutter objects

Max generally uses polygons and meshes as its default modeling type, but CAD packages generally work with solids. The Body Object is the answer for working between solids and meshes, and it is covered next.

## FIGURE 28.1

The SAT Import dialog box includes options for importing CAD objects.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_797_0.png)

The Single Body options let you import all objects together as a single object in Max. If all objects are not welded together, you can select and move them independently in Element subobject mode. If they are welded, they act as a single object. This may be desirable if you are loading in a background or some terrain data. The final option imports each trimmed surface as a separate body object.

The Viewport Body Mesh Quality setting is used to set the density of the mesh displayed in the viewport. The 3D Trimming Tolerance option lets you set how accurately the imported objects are trimmed. It is best to start with a lower tolerance and increase it as you see import problems such as missing faces.

### Caution

SAT files can be large, and selecting any of the Fine settings results in huge Max files.

Enabling the Automatic Face Flipping option causes the importer to attempt to correct any normals that are pointing the wrong way. Most CAD formats have a different coordinate system with the Z axis pointing up instead of the Y axis. Enabling the Convert SAT Y Axis to Z Axis option fixes this for the imported objects.

The Select Additional SAT Files for Import button opens a file dialog box where you can select more files to import using the current settings. Importing SAT files takes a long time, so selecting and importing several files at once is a good idea.

## Converting Max Objects to Body Objects

Objects that are imported from an SAT format appear in Max as Body Object types in the Modify panel. Max objects can be converted to the Body Object type using the Body Object button found in the Create panel by opening the Body Objects subcategory. Simply select the object to convert, and press the Body Object button.

The conversion works best when used on only the most basic primitive objects. If a more complex mesh object needs to be converted, try converting it to a NURBS object first and then to a Body Object.
