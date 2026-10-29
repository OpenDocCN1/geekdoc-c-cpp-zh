
## Accessing Subobjects and Using Modeling Helpers

Modeling is the process of pure creation. Whether it is sculpting, building with blocks, construction work, carving, architecture, or advanced injection molding, many different ways exist for creating objects. Max includes many different model types and even more ways to work with them.

This chapter introduces the various modeling methods in Max. It also explains the common modeling components, including normals and subobjects. The chapter also covers many utilities and helpers that, well, help as you begin to model objects. The purpose of this chapter is to whet your whistle for modeling and to cover some of the general concepts that apply to all models. More specific details on the various modeling types are presented in the subsequent chapters, so onward into the realm of creation.

**IN THIS CHAPTER**

- Understanding the modeling types
- Using normals
- Working with subobjects
- Using Soft Selection
- Using helper objects and utilities

## Exploring the Model Types

You can climb a mountain in many ways, and you can model one in many ways. You can make a mountain model out of primitive objects like blocks, cubes, and spheres, or you can create one as a polygon mesh. As your experience grows, you’ll discover that some objects are easier to model using one method and some are easier using another. Max offers several different modeling types to handle various modeling situations.

### Parametric objects versus editable objects

All geometric objects in Max can be divided into two general categories — parametric objects and editable objects. Parametric means that the geometry of the object is controlled by variables called parameters. Modifying these parameters modifies the geometry of the object. This powerful concept gives parametric objects lots of flexibility. For example, the sphere object has a parameter called Radius. Changing this parameter changes the size of the sphere. Parametric objects in Max include all the objects found in the Create menu.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_308_0.png)

## Chapter 10: Accessing Subobjects and Using Modeling Helpers

- **Compound objects:** A miscellaneous group of model types, including Booleans, loft objects, and scatter objects. Other compound objects are good at modeling one specialized type of object such as Terrain or BlobMesh objects. All the Compound objects are covered in Chapter 27, “Working with Compound Objects.”
- **Body objects:** Solid objects that are imported from a SAT file produced by a solid modeling application like Revit that have the concept of volume. Max mesh objects typically only deal with surfaces but can be converted to a Body object. All the information on Body objects is covered in Chapter 28, “Working with Solids and Body Objects.”
- **Particle systems:** Systems of small objects that work together as a single group. They are useful for creating effects such as rain, snow, and sparks. Particles are covered along with the Particle Flow interface in Chapter 41, “Creating Particles and Particle Flow.”
- **Hair and fur:** Modeling hundreds of thousands of cylinder objects to create believable hair would quickly bog down any system, so hair is modeled using a separate system that represents each hair as a spline. The Hair and Fur modifiers are covered in Chapter 29, “Adding and Styling Hair and Fur, and Using Cloth.”
- **Cloth systems:** Cloth—with its waving, free-flowing nature—behaves like water in some cases and like a solid in others. Max includes a specialized set of modifiers for handling cloth systems. Creating and using a cloth system is discussed in Chapter 29, “Adding and Styling Hair and Fur, and Using Cloth.”

> **Note**
> 
> Hair, fur, and cloth are often considered effects or dynamic simulations instead of modeling constructs, so their inclusion on this list should be considered a stretch.

With all these options, modeling in Max can be intimidating, but you learn how to use each of these types the more you work with Max. For starters, begin with primitive or imported objects and then branch out by converting to editable objects. A single Max scene can include multiple object types.

## Converting to editable objects

Of all the commands found in the Create menu and in the Create panel, you won’t find any menus or sub-categories for creating editable objects.

To create an editable object, you need to import it or convert it from another object type. You can convert objects by right-clicking on the object in the viewport and selecting the Convert To submenu from the pop-up menu, or by right-clicking on the base object in the Modifier Stack and selecting the object type to convert to in the pop-up menu.

Once converted, all the editing features of the selected type are available in the Modify panel, but the object is no longer parametric and loses access to its common parameters such as Radius and Segments. However, Max also includes specialized modifiers such as the Edit Poly modifier that maintain the parametric nature of primitive objects while giving you access to the editing features of the Editable object. More on these modifiers is presented in the later modeling chapters.

> **Caution**
> 
> If a modifier has been applied to an object, the Convert To menu option in the Modifier Stack pop-up menu is not available until you use the Collapse All command.

## Part III: Modeling Basics

The pop-up menu includes options to convert to editable mesh, editable poly, editable patch, and NURBS. If a shape or spline object is selected, then the object can also be converted to an editable spline. Using any of the Convert To menu options collapses the Modifier Stack.

> **Note**
> 
> **Objects can be converted between the different types several times, but each conversion may subdivide the object. Therefore, multiple conversions are not recommended.**

Converting between object types is done automatically using Max’s best guess, but if you apply one of the Conversion modifiers to an object, several parameters are displayed that let you define how the object is converted. For example, the Turn to Mesh modifier includes an option to Use Invisible Edges, which divides polygons using invisible edges. If this option is disabled, then the entire object is triangulated. The Turn to Patch modifier includes an option to make quads into quad patches. If this option is disabled, all quads are triangulated.

The Turn to Poly modifier includes options to Keep Polygons Convex, Limit Polygon Size, Require Planar Polygons, and Remove Mid-Edge Vertices. The Keep Polygons Convex option adds any polygons that are concave, if enabled. The Limit Polygon Size option lets you specify the maximum allowable polygon size. This can be used to eliminate any pentagons and hexagons from the mesh. The Require Planar Polygons option keeps adjacent polygons as triangles if the angle between them is greater than the specified threshold value. The Remove Mid-Edge Vertices option removes any vertices caused by intersections with invisible edges.

All Conversion modifiers also include options to preserve the current subobject selection (including any soft selection) and to specify the Selection Level. The From Pipeline option uses the current subobject selection that is selected on the given object. After a Conversion modifier is applied to an object, you must collapse the Modifier Stack in order to complete the conversion.

## Understanding Normals

Before moving on to the various subobjects, you need to understand what a normal is and how it is used to tell which way the surface is facing. Normals are vectors that extend outward perpendicular to the surface of an object. These vectors aren’t rendered and are used only to tell which way the surface face is pointing. If the normal vector points toward the camera, then the polygon is visible, but if it points away from the camera, then you are looking at its backside, which is visible only if the Backface Cull option in the Object Properties dialog box is disabled.

Several other properties also use the normal vector to determine how the polygon face is shaded, smoothed, and lighted. Normals are also used in dynamic simulations to determine collisions between objects.

## Viewing normals

In all mesh subobject modes except for Edge, you can select the Show Normals option to see any object’s normals and set a Scale value. Figure 10.1 shows a Plane, a Box, and a Sphere object. Each object has been converted to an Editable Mesh with all faces selected in Face subobject mode with the Show Normals option selected.
