your abstraction within the bounds of your resources, and finally, *test* to verify that your abstraction was appropriate.

**Visual System Impact principle:** Consider the impact of the human visual system on your problem and its models.

**Coordinate-System/Basis principle:** Always choose a coordinate system or basis in which your work is most convenient, and use transformations to relate different coordinate systems or bases.

**First Pixel principle:** The first pixel is the hardest.

**Visual Debugging principle:** Use visual displays to help you debug and understand your graphics programs.

**Hierarchical Modeling principle:** Whenever possible, construct models hierarchically. Try to make the modeling hierarchy correspond to a functional hierarchy for ease of animation.

**Implementation principle:** If you understand a mathematical process well enough, you can write a program that executes it.

**Parametric/Implicit Duality principle:** There's a duality between parametric and implicit forms for shapes: In general, it's easy to find an intersection between shapes where one's described implicitly and the other parametrically, and harder when either both are implicit or both parametric.

**Tiling principle:** If T′ is an oriented triangle in plane P′ with normal n′, and T is its projection to plane P, the projection being along the unit normal n to P, then the signed area of T is n′ · n times the signed area of T′.

**Division of Modeling principle:** Separate the mathematical and/or physical model of a phenomenon from the numerical model used to represent it.

**Meaning principle:** For every number that appears in a graphics program, you need to know the semantics, the **meaning**, of that number.

**Transformation Uniqueness principle:** For each class of transformations—linear, affine, projective—and any corresponding coordinate frame, and any set of corresponding target elements, there's a unique transformation mapping the frame elements to the corresponding elements in the target frame. If the target elements themselves constitute a frame, then the transformation is invertible.

**High-Level Design principle:** Start from the broadest possible view. Elements of a graphics system don't separate as cleanly as we might like: you can't design the ideal representation for an emitter without considering its impact on light transport. Investing time at the high level lets us avoid the drawbacks of committing, even if it defers gratification.

**Noncommutativity principle:** The order of operations often matters in graphics. Swapping the order of operations can introduce both efficiencies in computations and errors in results. You should be sure that you know when you're doing so.

**API principle:** Design APIs from the perspective of the programmer who will use them, not that of the programmer who will implement them or from the mathematical notation used in their derivation. For example, a single BSDF f(ωo, ωi) mapped to a function `API.Color3 bsdf(Vector3 wi, Vector3 wo)` is easy to implement but hard to use in a real renderer.