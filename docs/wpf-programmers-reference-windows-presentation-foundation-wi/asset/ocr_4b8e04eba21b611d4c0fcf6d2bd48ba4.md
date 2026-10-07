![](bbox=[0.147, 0.101, 0.546, 0.423])

The following code shows the program's MakeRectangle routine, which builds a textured rectangle:

```
// Make a rectangle.
// If rect_mesh is null, make a new one and add it to the model.
// The points p1, p2, p3, p4 should be outwardly oriented.
// The points u1, u2, u3, u4 give the texture coordinates
// for the points p1, p2, p3, p4.
private void MakeRectangle(Model3DGroup rect_model,
    ref MeshGeometry3D rect_mesh, Material rect_material,
    Point3D p1, Point3D p2, Point3D p3, Point3D p4,
    Point u1, Point u2, Point u3, Point u4)
{
    // Make the mesh if we must.
    if (rect_mesh == null)
    {
        rect_mesh = new MeshGeometry3D();
        GeometryModel3D new_model =
            new GeometryModel3D(rect_mesh, rect_material);
        rect_model.Children.Add(new_model);
    }

    // Make the points.
    rect_mesh.Positions.Add(p1);
    rect_mesh.Positions.Add(p2);
    rect_mesh.Positions.Add(p3);
    rect_mesh.Positions.Add(p4);

    // Set the texture coordinates.
    rect_mesh.TextureCoordinates.Add(u1);
    rect_mesh.TextureCoordinates.Add(u2);
```