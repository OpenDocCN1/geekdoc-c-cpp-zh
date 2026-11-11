efficient in both space and time and much simpler to implement. Except at joints, the representation automatically preserves volume.

The limitation of an articulated rigid body is that motion necessarily appears mechanical because the individual pieces remain rigid. Were we to animate a character in this way, the character would appear robotic instead of humanoid. A more general solution is the **articulated body**. This maintains a scene graph of reference frames, but performs some other kind of animation, such as keyframe vertex interpolation, on the data within those reference frames. The particular combination of rigid frames with vertex-interpolated key frames was very popular for real-time applications like games until fairly recently, when it was overtaken by the more general scheme of skeletal animation.

# 35.5.4  Skeletal Animation

The shape of the surface of a living creature under motion is dictated by the dynamic position of its skeleton and the constraints of its musculature and other internals. It is sensible to consider parameterizing virtual objects that model such creatures in a similar way. (This is an example of the Wise Modeling principle that says that you should decide what phenomena you want to model, and then be sure your model is rich enough to represent those phenomena.) This is known as a **skeletal animation** (a.k.a. **matrix skinning**) model.

A skeletal animation model defines a set of reference frames called **bones**. That is evocative but something of a misnomer, because reference frames correspond most closely to the *joints* of the character, not the bones between those joints. The bones may be in a common object space or arranged hierarchically into a tree with parent-child relationships.

We are used to expressing a point as a weighted combination of axis vectors in some reference frame. A single vertex in a skeletal animation mesh is a weighted combination of points in multiple reference frames. For example, a point near a human’s elbow may be defined as halfway between a point defined in the shoulder/upper arm’s reference frame and a point defined in the elbow/forearm’s reference frame. This joint parameterization allows that vertex and its similarly defined neighbors to define a smoothly deforming mesh near the elbow as it bends. That is in contrast to the sharp intersection of surfaces defined in different reference frames observed under articulated rigid body animation.

We can think of a point **x** represented as a linear combination of specific points *P*<sub>b</sub> transformed by corresponding bone transformation matrices *B*<sub>b</sub> at given times under various scalar weights *w*<sub>b</sub>:

$$\mathbf{x}(t) = \sum_{b \in \mathrm{bones}} (\mathbf{B}_b(t)(\mathbf{P}_b))w_b,$$ (35.15)

where $\sum w_b = 1$. However, since $P_b$ and $w_b$ are both part of the parameterization that we will compute from an artist’s input and all relevant operators are linear, in practice we need only store 3-vectors $P'_b = P_bw_b$.

One typically constructs the representation by having an artist place a skeleton inside a mesh that is in some standard pose. The artist then assigns bone weights to each vertex and the system computes $P'_b$ for each vertex from them. A first approximation might be that each vertex has a single nonzero weight, which is for its position in the standard pose relative to the closest reference frame. The artist then manipulates the skeleton to create a different pose and the vertices transform