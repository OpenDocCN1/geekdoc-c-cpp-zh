# 8.3.2 Estimating Fundamental Matrix

The next obvious question is, how do we estimate the fundamental matrix? In this section, we will explore estimation of fundamental matrix for different camera pair setups.

Calibrated Camera If we have a calibrated pair of stereo cameras, finding the fundamental matrix is relatively easy. Let the 3 × 4 calibration matrix of camera C₁ and C₂ be given by A₁ and A₂ respectively. Therefore,

p₁ = A₁ P

(8.22)

Since A₁ is not a square matrix, it is not invertible. But we can find its pseudo-inverse A₁⁺ which is a 4 × 3 matrix such that A₁ A₁⁺ = I where I is the 3 × 3 identity matrix. It can be shown that A₁⁺ = (A₁ᵀ A₁)⁻¹ A₁ᵀ. Using this pseudo inverse A₁⁺, we can write Equation 8.22 as

P = A₁⁺ p₁

(8.23)

Now, the image p₂ of P in the second camera can be expressed as

p₂ = A₂ P

(8.24)

= A₂ A₁⁺ p₁

(8.25)

The line l₂ can be defined by its endpoints e₂ and p₂ and also by Equation 8.18 giving

l₂ = e₂ × p₂ = [e₂]ₓ A₂ A₁⁺ p₁ = F p₁

(8.26)

Therefore, F can be derived from the above equation as

F = [e₂]ₓ A₂ A₁⁺.

(8.27)

In fact, it can be shown that A₂ A₁⁺ is a full rank 3 × 3 matrix and is the homography A defined in Equation 8.14.

First Camera Aligned with World Coordinate Next, we will simplify the camera setup even more. Let us consider C₁ to be located at the origin aligned with the coordinate axes. Let the intrinsic matrix for C₁ be K₁. Therefore, A₁ is given by

A₁ = K₁ (I | O)

(8.28)

where I is the 3 × 3 identity matrix and O is (0,0,0)ᵀ. Further A₁⁺ is given by

A₁⁺ = ( K₁⁻¹ )

O

(8.29)