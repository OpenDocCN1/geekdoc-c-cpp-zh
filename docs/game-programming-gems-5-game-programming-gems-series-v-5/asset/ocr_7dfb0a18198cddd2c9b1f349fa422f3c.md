which shows to reflect a vector x through a vector a, by the transform x → axa⁻¹. This is a useful formula, since it works in any dimension, and is the basis for rotation formulas that are dimension-independent.

![](bbox=[0.312, 0.19, 0.75, 0.38])

FIGURE 2.1.5 Reflection has a simple GA notation.

By reflecting twice over vectors a and b with an angle θ/2 between them, we can rotate the objects encoded in multivectors by an angle θ. The object R = ab is called a rotor, and performs rotation on any multivector X in any dimension, by the transformation X → RXR⁻¹. They are more efficient to compose than matrices and are numerically more stable. And they rotate multivectors, not just vectors (see the examples that follow). In 3D, expanding a rotor in terms of basis elements shows it is just a quaternion, as we would expect.

There are several equivalent ways to construct a rotor. It is useful to take a and b to be unit vectors, since R⁻¹ = ba is easy to compute. In 3D, a way to construct a rotor that rotates by θ around an axis c is to take R = cos(θ/2) - sin(θ/2)Ic. With these different and concise formulas to construct rotations, GA provides a simpler way to work out computations. And in any dimension, composition of rotors is computed with the geometric product. It's even possible to do calculus on rotors to give velocities, accelerations, interpolations, minimizing paths, camera orientation, etc., but this will require more gems. As in all mathematics, this goes much deeper than there is space to present completely. Another advantage is that the rotor also keeps track of the direction of rotation, unlike a scalar-valued angle or rotation matrix, allowing subdivision and interpolation of rotations. In three dimensions, rotor interpolation is the usual SLERP, as shown in Equation 2.1.13

```
R(λ) = \frac{\sin((1-λ)θ)R_1 + \sin(λθ)R_2}{\sin θ}.
(2.1.13)
```