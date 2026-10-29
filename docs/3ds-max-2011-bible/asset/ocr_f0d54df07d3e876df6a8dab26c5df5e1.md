# Display and Advanced settings

The Display rollout controls which features are visible within the viewports. Options include Show Colored Vertices, Show Colored Faces, Color All Weights, Show All Envelopes, Show All Vertices, Show All Gizmos, Show No Envelopes, Show Hidden Vertices, Draw On Top Cross Sections, and Draw On Top Envelopes.

With these display options, you can turn on and off the weight color shading on vertices and faces. You can also select to show all envelopes, vertices, and gizmos The Color All Weights option is unique. It assigns every bone a different color and shows how the weights blend together between bones.

The Advanced Parameters rollout includes an option to Back Transform Vertices. This option avoids applying transform keys to the skin because the bones control the motion. The Rigid Vertices and Rigid Patch Handles options set the vertices so that they are controlled by only one bone. This rollout also includes buttons to Reset Selected Vertices, Reset Selected Bones, and Reset All Bones. This is handy if you really mess up a skinning job, because it gives you a chance to start over. It also includes buttons for saving and loading envelopes. The envelopes are saved as files with the .env extension.

The Animatable Envelopes option lets you create keys for envelopes. Weight All Vertices is a useful option that automatically applies a weight to the nearest bone of all vertices that have no weight. The Remove Zero Weights button removes the vertex weight of any vertex that has a value lower than the Zero Limit. This can be used to remove lots of unnecessary data from your model if you need to put it on a diet.

# Using deformers

Below the Advanced Parameters rollout is the Gizmos rollout. You use this rollout to apply deformers to selected skin object vertices. Three deformers are available in the Gizmos rollout: a Joint Angle Deformer, a Bulge Angle Deformer, and a Morph Angle Deformer.

Each of these deformers is unique. They include the following features:

+   - Joint Angle Deformer: Deforms the vertices around the joint between two bones where the skin can bunch up and cause problems. This deformer moves vertices on both the parent and child bones.

+   - Bulge Angle Deformer: Moves vertices away from the bone to simulate a bulging muscle. This deformer works only on the parent bone.

+   - Morph Angle Deformer: Can be used on vertices for both the parent and child bones to move the vertices to a morph position.

All deformers added to a skin object are listed in the Gizmo rollout. You can add deformers to and remove deformers from this list using the Add and Remove Gizmo buttons. You can also Copy and Paste the deformers to other sets of vertices. Before a deformer gizmo can be applied, you need to select vertices within the skin object. To select vertices, enable the Vertices check box of the Parameters rollout and drag over the vertices in the viewport to select the vertices.

The parameters for the deformer selected in the Gizmo rollout's list appear when the deformer is selected in the Deformer Parameters rollout. This rollout lists the Parent and Child bones for the selected vertices and the Angle between them. This rollout changes depending on the type of deformer selected.

For the Joint and Bulge Angle Deformers, a new rollout labeled Gizmo Parameters or Deformer Parameters appears. The Gizmo Parameters rollout includes buttons to edit the control Lattice and to edit the deformer Key Curves. The Edit Lattice button lets you move the lattice control points in the viewports. The Edit Angle Keys Curves opens a Graph window that displays the transformation curves for the deformation.