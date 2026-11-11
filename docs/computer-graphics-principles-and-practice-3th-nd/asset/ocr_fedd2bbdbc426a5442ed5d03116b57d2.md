+   1. Find a vector v ∈ S^3 that's in the q1–q2 plane and is perpendicular to q1.
+      We subtract the projection (q2 · q1)q1 of q2 onto q1 from q2 to get a vector perpendicular to q1, and normalize:
+      v = (q2 − (q2 · q1)q1) / ||q2 − (q2 · q1)q1||. (11.41)
+   2. Find a unit-speed path along the great circle from q1 through v. That's just γ(t) = cos(t)q1 + sin(t)v. This path reaches q2 at t = θ, where θ = cos⁻¹(q1 · q2) is the angle between the two vectors.
+   3. Adjust the path so that it reaches q2 at time 1 rather than at time θ, by multiplying t by θ.

The resultant code is shown in Listing 11.4.

Listing 11.4: Code for spherical linear interpolation between two quaternions.

```
~~~cpp
1  double[4] slerp(double[4] q1, double[4] q2, double t)
2  {
3      assert(dot(q1, q1) == 1);
4      assert(dot(q2, q2) == 1);
5      // build a vector in q1-q2 plane that's perp. to q1
6      double[4] u = q2 - dot(q1, q2) * q1;
7      u = u / length(u); // ...and make it a unit vector.
8      double angle = acos(dot(q1, q2));
9      return cos(t * angle) * q1 + sin(t * angle) * u;
10 }
~~~
```

As the argument to the cosine ranges from 0 to angle, the result varies from q1 to q2.

# 11.2.6.2 Interpolating between Rotations

We now have all the tools we need to interpolate between rotations. Suppose that M1 and M2 are rotation matrices, with M1 corresponding to the quaternions ±q1, and M2 corresponding to the quaternions ±q2, as indicated schematically in Figure 11.8. Starting with q1, we determine which of q2 and −q2 is closer, and then interpolate along an arc between q1 and this point; to find interpolating rotations, we project to SO(3) via K.

Listing 11.5 shows the pseudocode.

Listing 11.5: Code to interpolate between two rotations expressed as matrices.

```
~~~cpp
1  Mat33 RotInterp(Mat33 m1, Mat33 m2, double t)
2  // find a rotation that's t of the way from m1 to m2 in SO(3).
3  // m1 and m2 must be rotation matrices.
4  {
5      if ( m1 m2^T = -I ) {
6          report error; can't interpolate between opposite rotations.
7      }
8      Quaternion q1, q1p, q2, q2p;
9      RotationToQuaternion(m1, q1, q1p);
10     RotationToQuaternion(m2, q2, q2p);
11     if (Dot(q1, q2) < 0) q2 = q2p;
12     Quaternion qi = Quaternion.slerp(q1, q2, t);
13     return R(qi); // R is the projection from S3 to SO(3)
14 }
~~~
```