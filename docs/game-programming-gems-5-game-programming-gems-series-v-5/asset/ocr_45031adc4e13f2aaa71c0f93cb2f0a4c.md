called spherical linear interpolation or slerp for short. The goal of the slerp function is to interpolate smoothly between two quaternions a and b, sweeping a constant angle per unit time and maintaining a constant unit length.

So why can't we just use linear interpolation? The answer is that we need to maintain the unit length of the interpolated quaternion to avoid introducing a scaling factor. Even if we renormalize the result of linear interpolation, the angular velocity of the resulting animation will not be constant, resulting in jerky movement.

An example of a slerp in real life is the great circle taken by a passenger jet over the surface of the Earth. The jet keeps a constant distance from the center of the Earth and moves with a constant speed over the shortest arc. Thus, if we want to fly from Amsterdam to Berlin, we apply the function:

Slerp(Amsterdam, Berlin) (2.4.12)

How do we achieve this?

![](bbox=[0.38, 0.42, 0.68, 0.7])

In Figure 2.4.1, Amsterdam is represented by the vector a and Berlin by b. The position p of the jet sweeps out an arc of θ radians during the journey, taking one hour. At time t, we have moved θt radians.

This position can be represented as a linear combination of the vectors a and b:

p(θ,t) = α(θ,t)a + β(θ,t)b. (2.4.13)

We can calculate a and b by using the triangle drawn on the diagram. Using the sine formula for triangle area in three different ways for the triangle opc, with op = 1, oc = α, cp = β,