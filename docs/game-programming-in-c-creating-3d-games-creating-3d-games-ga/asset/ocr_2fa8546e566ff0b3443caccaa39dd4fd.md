# Combining Rotations

Another common operation is applying an additional rotation to an existing quaternion. Given two quaternions, p and q, the Grassmann product is the rotation of q followed by p:

```
$(pq)_v = p_v.q_v + q_v.p_v + p_v \times q_v$
$(pq)_s = p_s.q_s - p_v \cdot q_v$
```

```
$(pq)_v = p_s.q_v + q_s.p_v + p_v \times q_v$
$(pq)_s = p_s.q_s - p_v \cdot q_v$
```

Note that even though the multiplication has p to the left of q, the rotation applies in a right-to-left order. Also, because the Grassmann product uses a cross product, it isn't commutative. So, swapping p and q will reverse the order of rotation.

Much like a matrix, a quaternion has an inverse. For unit quaternions, the inverse of a quaternion is the negation of its vector component:

```
$q^{-1} = [-q_v, q_s]$
$q^{-1} = [-q_v, q_s]$
```

Because there's an inverse, there is also an identity quaternion, defined as follows:

```
$i_v = \langle 0, 0, 0 \rangle$
$i_s = 1$
```

```
$i_v = \langle 0, 0, 0 \rangle$
$i_s = 1$
```