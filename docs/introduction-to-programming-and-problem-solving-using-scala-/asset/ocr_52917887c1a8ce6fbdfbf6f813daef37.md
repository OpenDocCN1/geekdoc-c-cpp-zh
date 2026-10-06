# Graphics and Advanced ScalaFX

![](bbox=[0.214, 0.073, 0.785, 0.335])

This is some text.

This text is in bold.

This text is underlined.

Now a list:

+   * One
* Two
* Three

The text can have even colors.

FIGURE 12.17: The window that is produced by running HTMLEEditor.scala.

There are four different 3D shapes in the scalafx.scene.shape type that are provided. These are Box, Cylinder, MeshView, and Sphere. With the exception of MeshView, these should be fairly self-explanatory as all basic 3D shapes. The MeshView covers everything that is not those three shapes by you to make complex geometries of triangles. Proper coverage of the MeshView is outside of the scope of our discussion.

For 2D shapes, you need to specify the field that was used for drawing them. When you go to 3D, this changes to a material. ScalaFX provides the scalafx.scene.paint.PhongMaterial type for this purpose. You can instantiate this type with new PhongMaterial(diffuseColor: Color, diffuseMap: Image, specularMap: Image, bumpMap: Image, selfIllumination: Map) or new PhongMaterial(diffuseColor: Color). The first option gives significant control over how the material appears. For example, the diffuseMap allows you to apply a texture to the surface of the shape.

In addition to having shapes, when you move to 3D with cameras and lighting, both of which are defined in the scalafx.scene package. There are two types of cameras provided. By default you use a ParallelCamera. When you use the ParallelCamera, object do not get smaller as you move away from the camera. In this view, parallel lines leading away from the viewer remain parallel. This is not what happens in real life, but it is sufficient for some application. The PerspectiveCamera more closely resembles the way we actually see, with objects shrinking as they get further away and everything converging to a point at distance. You make a ParallelCamera with new ParallelCamera. To make a PerspectiveCamera you new PerspectiveCamera(fixedEyeAt:Boolean). The Stage has a member called camera that you can assign to your desired camera type.

There are two types of light in ScalaFX. They are the AmbientLight and

> 15 The ability to have only one camera for the full stage can be a bit limiting. The scalafx.scene package