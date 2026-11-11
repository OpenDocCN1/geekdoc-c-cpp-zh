
### 6.6.3.3 Constructing a Composite Component

A composite node is specified via the instantiation of subcomponents within a `Model3DGroup` element: the subcomponents are accumulated into the composite node’s own coordinate system.

### 6.6.3.4 Creating the Lower Leg

Here is a first draft of our camel’s lower leg:

```xml
<Model3DGroup x:Name="LowerLeg">
    <GeometryModel3D Geometry="{StaticResource RSRCMeshFoot}">
        Material... />
    <GeometryModel3D Geometry="{StaticResource RSRCMeshShin}">
        Material... />
</Model3DGroup>
```

Testing this composite by instantiating it into the viewport yields the rendering shown in Figure 6.44.

**Inline Exercise 6.11:** Back in the lab, select the model “Lower leg (shin + foot)”.

![](img/f464cd0043eb5336aa0543fe20a0561b_192_0.png)

*Figure 6.45: Rendering of the lower-leg model, now corrected via application of a modeling transformation on the shin sub-component.*

This unsatisfactory result, in which the two models co-inhabit space causing the foot’s ankle region to intersect the shin, occurs because each component is, by design, positioned at the origin of its local coordinate system. When composing parts, we must use instance transforms to properly position the subcomponents relative to one another. Our goal is for the bottom of the shin to be connected to the top (ankle) part of the foot.

Thus, we need to translate the shin in the positive y direction; an offset of 13 units is sufficient. Note that the foot is already properly positioned for its role in the lower-leg composite and thus needs no transform.

Below is our second draft of the XAML specification for this composite component (with the new lines of code highlighted). A couple of views of the result are shown in Figures 6.45 and 6.46.

```xml
<Model3DGroup x:Name="LowerLeg">

    <GeometryModel3D Geometry="{StaticResource RSRCMeshFoot}">
        Material... />

    <GeometryModel3D Geometry="{StaticResource RSRCMeshShin}">
        Material... />
        <GeometryModel3D.Transform>
            <TranslateTransform3D OffsetY="13"/>
        </GeometryModel3D.Transform>
</Model3DGroup>
```

![](img/f464cd0043eb5336aa0543fe20a0561b_192_1.png)

*Figure 6.46: Rendering of the lower-leg model from a second point of view.*

**Inline Exercise 6.12:** Return to the lab, and use the hierarchy viewer/editor to add a transform to the shin to repair the lower-leg composite.

### 6.6.3.5 Creating the Full Leg

Let’s continue our bottom-up implementation by going up to the next level. The “whole leg” is a composition of the lower leg (itself a composite) and the thigh (a primitive). Let’s first compose these two components to form a rigid locked object, and then we’ll attack the challenge of adding a knee joint.

As was the case for the lower leg, one of the subcomponents needs an instance transform (i.e., the thigh needs to be raised 43 units in the y direction) and the other is already at a suitable location. The resultant image is shown in Figure 6.47; the XAML code is as follows:

![](img/f464cd0043eb5336aa0543fe20a0561b_193_0.png)

```xml
    <Model3DGroup x:Name="Leg">

      <!-- Build the lower-leg composite (same XAML shown earlier). -->
      <Model3DGroup x:Name="LowerLeg"> . . . </Model3DGroup>

      <!-- Instantiate and transform the thigh. -->
      <GeometryModel3D Geometry="{StaticResource RSRCMeshThigh}">
        Material . . . >
          <GeometryModel3D.Transform>
            <TranslateTransform3D OffsetY="43"/>
          </GeometryModel3D.Transform>
      </GeometryModel3D>

    </Model3DGroup>
```

**Inline Exercise 6.13:** Return to the lab, and select “Thigh” from the list of models to examine that component in isolation. Then select the model “Whole leg.” The undesired merging of the two subcomponents will be obvious. Repair by adding an instance transform to the thigh to translate it on the y-axis. (If you wish, you can jump straight to our solution by choosing “Whole leg auto-composed” from the list of models.)

### 6.6.3.6 Adding the Knee Joint

The leg is currently locked in a straight position. But, by adding a rotation transformation to the lower leg, we can provide a “hook” that animation logic can use to simulate bending at the knee.

Figure 6.48 shows the leg in its canonical location at the origin, but with a 37° rotation at the knee. (The invisible axis of rotation has been added to this rendered image for clarity.)

![](img/f464cd0043eb5336aa0543fe20a0561b_193_1.png)

The WPF element for expressing 3D rotation requires specification of the axis and the rotation amount. The axis is configured via two parameters: an arbitrary directional vector (e.g., [1 0 0]^T representing any line that is parallel to the x-axis) and a center point lying on that vector (e.g., the center of the “knee” part of the lower leg, which is (0.50, 0) in the lower leg’s coordinate system).

**Inline Exercise 6.14:** Return to the whole-leg model in the lab. Implement the simulated knee joint by adding a rotation transform to the lower-leg component. Set the rotation axis as needed, and then use the numeric spinner to change the rotation amount to produce a knee-bend animation.

The XAML for the lower leg—with the joint transformation in effect to bend the knee—now appears as follows:

```xml
<!-- Construct the lower-leg composite (same XAML shown earlier) -->
<Model3DGroup x:Name="LowerLeg">
  <Model3DGroup.Transform>
    <!-- Joint transform for the knee -->
    <RotateTransform3D CenterX="0.5" CenterY="0" CenterZ="0">
      <RotateTransform3D.Rotation>
        <AxisAngleRotation3D x:Name="KneeJointAngle" Angle="37" Axis="1 0 0"/>
      </RotateTransform3D.Rotation>
    </RotateTransform3D>
  </Model3DGroup.Transform>
  <GeometryModel3D Geometry="{StaticResource RSRCMeshFoot}" Material="..."/>
  <GeometryModel3D Geometry="{StaticResource RSRCMeshShin}" Material="...">
    <GeometryModel3D.Transform>
      <TranslateTransform3D OffsetY="14"/>
    </GeometryModel3D.Transform>
  </GeometryModel3D>
</Model3DGroup>
```

Manipulation of the joint’s rotation amount can be performed by procedural code, or by the declarative animation features introduced in Section 2.5.1.

### 6.6.4 Reuse of Components

With our leg designed, let’s move up one more level and consider how we might compose the entire camel. The leg is the first component that is going to be multiply instantiated into its parent. Reusing components is fundamental to hierarchical modeling; however, there are two types of reuse, each achieving different goals and appropriate for different scenarios.

First, consider a scenario in which we must show the camel walking or galloping in a realistic way. To achieve this, we need to be able to individually control the amount of rotation at each of the four hip joints and each of the four knee joints. To achieve hip and knee rotation, we construct the camel as a tree of nodes, with each node being used only once, as shown in Figure 6.49. Thus, there are four hip joints and four knee joints, each independently manipulable.

Is any “reuse” going on in this model? Well, you could say that we are reusing the design of the leg, since the model has four copies of the leg component hierarchy we designed above. But there is no reuse of the actual components in the constructed model. The front-left leg is a tree of components dedicated to representing only the front-left leg; there is a completely independent tree of components for each of the four legs. The advantage of this approach is that each leg is independent of the others, and the effect of manipulating one leg’s joints is limited in scope to just that leg.

It is useful to search for a model for rigid subcomponents that do not have any internal joints; they are candidates for being extracted and turned into reusable components. In the model discussed above, the lower-leg component is indeed rigid, because our design does not include an ankle joint that would allow the foot to rotate relative to the shin. Thus, we can reuse the lower-leg component hierarchy without any loss of animation flexibility, by constructing the camel using the structure shown in Figure 6.50. Here, our model is no longer a tree—it is a directed acyclic graph (DAG) now that component reuse is in effect; this topology is the reason this kind of structure is known as a “scene graph.”
