
# FIGURE 5.8

The octagon, cube, tetrahedron, icosahedron, and dodecahedron objects; Plato would be amazed.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_194_0.png)

## Exploring the Primitive Object Types

In the Create panel are actually two different subcategories of geometric primitives: Standard Primitives and Extended Primitives. These primitives include a diverse range of objects, from simple boxes and spheres to complex torus knots. You can create all these primitives from the Create panel.

## Starting with the Standard Primitives

The Standard Primitives include many of the most basic and most used objects, including boxes, spheres, and cylinders. Figure 5.9 shows all the Standard Primitives.

## Box

You can use the Box primitive to create regular cubes and boxes of any width, length, and height. Holding down the Ctrl key while dragging the box base creates a perfect square for the base. To create a cube, select the Cube option in the Creation Method rollout. A single click and drag completes the cube.

The Length, Width, and Height Segment values indicate how many polygons make up each dimension. The default is only one segment.

## Part II: Working with Objects

# FIGURE 5.9

The Standard Primitives: Box, Sphere, Cylinder, Torus, Teapot, Cone, GeoSphere, Tube, Pyramid, and Plane

![](img/ebbb4844f027f7d1c580e48108d2b6cb_195_0.png)

## Sphere

Spheres appear everywhere from sports balls to planets in space. Spheres are also among the easiest primitives to create. After clicking the Sphere button, simply click and drag in a viewport.

In the Parameters rollout, the Segments value specifies the number of polygons that make up the sphere. The higher the number of segments, the smoother the sphere is. The default value of 32 produces a smooth sphere, and a value of 4 actually produces a diamond-shaped object. The Smooth option lets you make the sphere smooth or faceted. Faceted spheres are useful for identifying faces for modifications. Figure 5.10 shows five spheres. The one on the left has 32 Segments and the Smooth option turned on. The remaining spheres have the Smooth option disabled with Segment values of 32, 16, 8, and 4.

# FIGURE 5.10

Sphere primitives of various Segment values with the Smooth option turned on and off

![](img/ebbb4844f027f7d1c580e48108d2b6cb_195_1.png)

The Parameters rollout also lets you create hemispheres. The hemisphere shape is set by the Hemisphere value, which can range from 0.0 to 1.0, with 0 being a full sphere and 1 being nothing at all. (A value of 0.5 would be a perfect hemisphere.) With the Hemisphere value specified, you now have two options with which to deal with the unused polygons that make up the originating sphere: the Chop option, which removes the unused polygons, and the Squash option, which retains the polygons but "squashes" them to fit in the hemisphere shape.

Figure 5.11 shows two hemispheres with Hemisphere values of 0.5. The Edged Faces option was enabled so you can see the polygon faces. The left hemisphere was created using the Chop option, and the right hemisphere was created with the Squash option. Notice how many extra polygons are included in the right hemisphere.

The Slice option enables you to dissect the sphere into slices (like segmenting an orange). The Slice From and Slice To fields accept values ranging from 0 to 360 degrees. Figure 5.12 shows four spheres that have been sliced. Notice that, because the Segments value hasn't changed, all slices have the same number of faces.

# FIGURE 5.11

Creating hemispheres with the Chop and Squash options

![](img/ebbb4844f027f7d1c580e48108d2b6cb_196_0.png)

## Note

You can use the Slice feature on several primitives, including the sphere, cylinder, torus, cone, tube, oiltank, spindle, chamfercyl, and capsule.

# FIGURE 5.12

Using the Slice option to create sphere slices

![](img/ebbb4844f027f7d1c580e48108d2b6cb_196_1.png)

The Base to Pivot parameter determines whether the position of the pivot point (or the point about which the object rotates) is at the bottom of the sphere or at the center. The default (with the Base to Pivot setting not enabled) sets the pivot point for the sphere at the center of the sphere.

## Cylinder

You can use a cylinder in many places—for example, as a pillar in front of a home or as a car driveshaft. To create one, first specify a base circle and then a height. The default number of sides is 18, which produces a smooth cylinder. Height and Cap Segments values define the number of polygons that make up the cylinder sides and caps. The Smooth and Slice options work the same as they do with a sphere (see the preceding section).

## Tip

If you don’t plan on modifying the ends of the cylinder, make the Cap Segments equal to 1 to keep the model complexity down.

## Torus

A torus (which is the mathematical name for a "doughnut") is a ring with a circular cross section. To create a torus, you need to specify two radii values. The first is the value from the center of the torus to the center of the ring; the second is the radius of the circular cross section. The default settings create a torus with 24 segments and 12 sides. The Rotation and Twist options cause the sides to twist a specified value as the ring is circumnavigated.

Figure 5.13 shows some sample toruses with a Smooth setting of None. The first three have Segments values of 24, 12, and 6. The last two have Twist values of 90 and 360. The higher the number of segments, the rounder the torus looks when viewed from above. The default of 24 is sufficient to create a smooth torus. The number of sides defines the circular smoothness of the cross section.

# FIGURE 5.13

Using the Segments and Twist options on a torus

![](img/ebbb4844f027f7d1c580e48108d2b6cb_197_0.png)

The Parameters rollout includes settings for four different Smooth options. The All option smoothes all edges, and the None option displays all polygons as faceted. The Sides option smoothes edges between sides, resulting in a torus with banded sides. The Segment option smoothes between segment edges, resulting in separate smooth sections around the torus.

The Slice options work with a torus the same way as they do with the sphere and cylinder objects; see the "Sphere" section earlier in this chapter.

## Teapot

Okay, let's all sing together, "I'm a little teapot, short and stout. . . ." The teapot is another object that, like the sphere, is easy to create. Within the Parameters rollout, you can specify the number of Segments, whether the surface is smooth or faceted, and which parts to display, including Body, Handle, Spout, and Lid.

## Note

You may recognize most of these primitives as standard shapes, with the exception of the teapot. The teapot has a special place in computer graphics. In early computer graphics development labs, the teapot was chosen as the test model for many early algorithms. It is still included as a valuable benchmark for computer graphics programmers.

## Cone

The Cone object, whether used to create ice cream cones or megaphones, is created exactly like the cylinder object except that the second cap can have a radius different from that of the first. You create it by clicking and dragging to specify the base circle, dragging to specify the cone's height, and then dragging again for the second cap to create a Cone.

In addition to the two cap radii and the Height, parameter options include the number of Height and Cap Segments, the number of Sides, and the Smooth and Slice options.

## GeoSphere

The GeoSphere object is a sphere created by using fewer polygon faces than the standard Sphere object. This type of sphere spreads the polygon faces, which are all roughly equal in size, around the object, instead of concentrating them on either end like the normal Sphere object. This makes the GeoSphere a better choice for surface modeling because its polygon resolution is consistent. Geospheres also render more quickly and have faster transformation times than normal spheres. One reason for this is that a GeoSphere uses triangle faces instead of square faces.
