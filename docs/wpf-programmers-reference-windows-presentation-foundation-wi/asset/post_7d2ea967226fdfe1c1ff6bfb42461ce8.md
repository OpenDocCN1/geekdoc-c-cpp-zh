
To understand why this makes sense, suppose a triangle is part of a 3D object such as a tetrahedron. If the triangle is oriented properly, then its outward normal points out of the tetrahedron. If normal points toward the camera, then the camera can see the triangle (if nothing else blocks the view).

However, if the outward normal points away from the camera, then the triangle is on the far side of the tetrahedron, so the camera cannot see it. Direct3D doesn't even bother to draw the triangle because it cannot be visible.

## BACKFACE REMOVAL

Removing triangles that are oriented away from the camera is called backface removal. Sometimes it's also called *culling*, although that can also mean any method for quickly removing triangles from consideration. For example, if you can identify the triangles behind the camera, they also can be called.

Note that this only works for closed solids, and open surfaces won't appear properly from both sides. For example, suppose the camera views a shoebox without a lid from top. In this position, the camera is looking at the inner sides of the triangles, so, if they are outwardly oriented, Direct3D won't draw them. To fix this problem, you can include each triangle in the program's geometry twice, once with each orientation.

## Normals

As you'll see in the section "Lighting" later in this chapter, a triangle's normal not determines whether it's visible, but it also helps determine the triangle's color. That means more accurate normals give more accurate colors.

Left to its own devices, Direct3D finds a triangle's normal by performing some calculations using the points that define the triangle (It lines up its virtual fingers to the right-hand rule.) The resulting points perpendicularly away from the triangle.

For objects defined by flat surfaces such as cubes, octahedrons, and other polyhedra, that works. For smooth surfaces like spheres, cylinders, and tori (donuts), it doesn't work as well because the normal at one point of a triangle on the object's surface in a slightly different direction from the normals at other points. If you make the triangles small enough, the difference isn't noticeable, but if they are larger, using the same normal across the entire surface of a triangle makes the result appear faceted instead.

The MeshGeometry3D's *Normals* property tells you what geometry normal to use for the points defined by the *Positions*. The engine still uses the calculated normal to decide whether to draw a triangle, but it uses the normals you supply to color the triangle.

For example, suppose you are building a sphere. In each case, the points of the MeshGeometry3D object is on the surface of the sphere. The surface's normal at the point (x, y, z) on the sphere points from the sphere's center to the point. If the sphere is centered at the origin, the normal vector is simply <x, y, z>. If you set the normal for each point to the corresponding value, then Direct3D can use

## IS THERE A POINT?

Standard notation surrounds a vector's components with pointy brackets. A vector indicates a direction and not a position. For example, the vector <1, 0> indicates a direction pointing parallel to the X axis.

The SpheresWithNormals example program shown in Figure 23-3 demonstrates this technique. All the spheres were drawn using a separate MeshGeometry3D object for each triangle. The spheres on the right are the same as those on the left they specify normals for each MeshGeometry3D object. You can see that the results are much smoother.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_429_0.png)

Earlier in this section, I said Direct3D creates its normals for a triangle if you don't supply them. Actually, this is a bit of a simplification. If a point is used by more than one triangle in a MeshGeometry3D object, Direct3D sets the normal at that point to an average of the normals at that in the adjoining triangles. The result is somewhere between the individual triangles' normals, so the result is generally smoother.

For a sphere, adjoining triangles meet metrically around each point, so the averaged normal points away from the center of the sphere as it should, and the result is nicely smooth.

The SingleMesh example program draws spheres where every triangle in a sphere is contained in the same MeshGeometry3D object. The result is very smooth despite the fact that the program does not explicitly specify normals.

This program is much faster than SpheresWithNormals example. It takes Direct3D a lot to draw many triangles than it takes to draw one MeshGeometry3D object containing many triangles. (Try running the two programs and rapidly dragging their sliders back and forth. You'll find that SingleMesh can keep up better.)

## SHARING NORMALS

The Normals property specifies the normal at a point, not for a particular triangle. This means that if two triangles share the same point, they use the same normal at that point so they meet smoothly. This also means that two triangles cannot share the same points if they should join join. For example, suppose you draw a cube in a single MeshGeometry3D object. If two triangles on different sides of the cube share corners, then Direct3D will smooth out the edge between them you won't see a nice, crisp edge. Instead, you'll see something similar to the left in Figure 23-4 with the middle blurred.

## TextureCoordinates

The TextureCoordinates property is a collection that defines how points are mapped to positions on a material's surface. You specify a point's position on the surface by giving the coordinates of the point on the brush used to draw the surface.(The section “Materials” later in chapter says more about materials.)

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_430.png)

The coordinates on the brush begin with (0, 0) in the upper left with the first coordinate extending to the right and the second extending downwards. This is similar to the way you use X and Y coordinates in bitmap (although to avoid confusion with 3D space, many programmers call the axes U and V rather than X and Y).

FIGURE 23-4

Figure 23-5 shows the idea graphically. The material could come from any brush as a solid color, gradient, or image (although textures are often easy to visualize when shown in Figure 23-5).

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_430_1.png)

The picture on the left shows the texture material with its corners labeled in the U-V coordinate system. The picture on the right shows a MeshGeometry3D object that defines points (labeled A, B, C, and D) and two triangles (outlined in red and green).

FIGURE 23-5

The following code shows the MeshGeometry3D's definition. The corresponding Positions and TextureCoordinates map the points A, B, C, and D to the U-V coordinates (0, 0), (0, 1), (1, 0), and (1, 1), respectively. You can also see in Figure 23-5 how the program maps the hole from the texture's lower-right corner to the 3D rectangle's lower right corner.

## THREE-DIMENSIONAL DRAWING

```
<MeshGeometry3D
  Positions="-1,1,-1 -1,1,1 1,1,1 1,-1,1"
  TriangleIndices="0,1,2 2,1,3"
  TextureCoordinates="0,0 0,1 1,1 1,0"
/>
```

Available for download on Wrox.com

The TexturedBlock program shown in Figure 23-1 uses similar code to map textures to points for all of its surfaces.

## CAMERAS

The camera determines the location and direction from which a 3D scene is viewed. You can think of the camera as if it were a motion picture camera at a scene. The camera is in some position (possibly on a boom, a crane, or in cameraman's hand) pointed toward some part of the scene.

The following camera properties let you specify the camera's location and orientation:

- Position — Gives the camera's coordinates in 3D space.
- LookDirection — Gives the direction in which the camera should be pointed relative to its current position. For example, if the camera's Position is "1, 1, 1" and LookDirection is "1, 2, 3", then the camera is pointed at the point (1+1, 1+2, 1+3)=(2, 3, 4).
- UpDirection — Determines the camera's roll or tilt. For example, you might tilt the camera sideways or at an angle.

## COMMON DIRECTIONS

Often the camera LookDirection is the negative of its Position so the camera is looking back toward the origin. For example, if Position = "-1, -2, 3", then LookDirection = "-1, -2, 3" looks back toward the origin.

It's also common to set UpDirection to a vector pointing upward such as <0, 1, 0> so the camera is "right-side up."

The two most useful cameras in WPF are perspective and orthographic.

In a perspective view, parallel lines seem to merge toward a vanishing point and objects farther away appear smaller. This is similar to the way you see things in real life, the result of a perspective camera is more realistic.

In an orthographic view, parallel lines remain parallel and objects that have the same size appear to have the same size even if one is farther from the camera than another.
