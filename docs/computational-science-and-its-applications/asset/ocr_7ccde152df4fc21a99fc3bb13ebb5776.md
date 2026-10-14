**b** = bₓ x̂ + bᵧ ŷ + b_z ẑ

with respect to the body fixed axes xyz. Here, (x̂, ŷ, ẑ) is the unit vector in the rotating frame xyz. Moreover, the vector b can also be decomposed as

**b** = b_X X̂ + b_Y Ŷ + b_Z Ẑ

with respect to the non-rotating axes XYZ. Here, (X̂, Ŷ, Ẑ) is the unit vector in the inertial frame XYZ. We now differentiate b (defined in fixed frame) with respect to time t to get

d**b**/dt = [ dbₓ/dt x̂ + dbᵧ/dt ŷ + db_z/dt ẑ ] + [ bₓ d x̂/dt + bᵧ d ŷ/dt + b_z d ẑ/dt ]   (10.2)

The first part on the right hand side of Equation (10.2) can be interpreted as the instantaneous change of b observed from the body fixed frame xyz since the unit vectors (x̂, ŷ, ẑ) are fixed (do not change) in the body fixed frame. The second part on the right hand side of Equation (10.2) refers to the rate of change of the unit vectors as observed from the inertial frame (non-rotating frame) XYZ. Since the origin of the inertial frame has the same instantaneous velocity as the body-fixed frame, the only way that these unit vectors change with respect to time is by a rotation about some axis passing through the common origin. We denote this rotational velocity as ω and we have

d x̂/dt = ω × x̂,   d ŷ/dt = ω × ŷ,   d ẑ/dt = ω × ẑ.

Hence, the second part in Equation (10.2) becomes (ω × b) and Equation (10.2) reduces to

d**b**/dt = (d**b**/dt)_b + ω × **b**   (10.3)

Equation (10.3) relates the rate of change of the vector b between the translating axis (XYZ) and body fixed rotating axis (xyz). The subscript b indicates that the derivative is with respect to body fixed rotating frame xyz. The LHS is the rate of change of b in the non rotating frame XYZ, which is equal to the rate of change of b with respect to body fixed frame xyz plus omega cross b. Physically, it means that the vector b can increase in magnitude while keeping its direction fixed, and in addition it can change its direction.

Let us now consider the angular momentum L (also called as rotational momentum). The angular momentum is defined as the product of moment of inertia tensor I_m and the angular velocity ω, that is,

**L** = I_m ω,   I_m = [ I_xx  -I_xy  -I_xz ; -I_yx  I_yy  -I_yz ; -I_zx  -I_zy  I_zz ]

Here, I_xx is the moment of inertia of the body about the x-axis defined as

I_xx = ∫_{Ω_S(t)} ρ_s (y² + z²) dx dy dz,