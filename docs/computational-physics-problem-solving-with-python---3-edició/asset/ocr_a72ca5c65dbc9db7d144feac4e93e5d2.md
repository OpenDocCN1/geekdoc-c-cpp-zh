```
ax.set_ylabel('y')
ax.set_zlabel('u(x,y)')
p.show()
```

# 21.7

# Numerical Solution for 2D Waves

The development of an algorithm for the solution of the 2D wave equation (21.51) follows that of the 1D equation in Section 21.2.2. We start by expressing the second derivatives in terms of central differences:

∂²u(x, y, t)/∂t² = [u(x, y, t + Δt) + u(x, y, t − Δt) − 2u(x, y, t)] / (Δt)² , (21.69)
∂²u(x, y, t)/∂x² = [u(x + Δx, y, t) + u(x − Δx, y, t) − 2u(x, y, t)] / (Δx)² , (21.70)
∂²u(x, y, t)/∂y² = [u(x, y + Δy, t) + u(x, y − Δy, t) − 2u(x, y, t)] / (Δy)² . (21.71)

After discretizing the variables, u(x = iΔx, y = iΔy, t = kΔt) ≡ uᵏᵢ,ⱼ, we obtain our time-stepping algorithm by solving for the future solution in terms of the present and past ones:

uᵏ⁺¹ᵢ,ⱼ = 2uᵏᵢ,ⱼ − uᵏ⁻¹ᵢ,ⱼ (c'² / c'²) [uᵏᵢ₊₁,ⱼ + uᵏᵢ₋₁,ⱼ − 4uᵏᵢ,ⱼ + uᵏᵢ,ⱼ₊₁ + uᵏᵢ,ⱼ₋₁] , (21.72)

where as before c' ≡ Δx/Δt. Whereas the present (k) and past (k−1) solutions are known after the first step, to initiate the algorithm we need to know the solution at t = −Δt, that is, before the initial time. To find that, we use the fact that the membrane is released from rest:

0 = ∂u(t = 0)/∂t ≈ (u¹ᵢ,ⱼ − u⁻¹ᵢ,ⱼ)/(2Δt) ⇒ u⁻¹ᵢ,ⱼ = u¹ᵢ,ⱼ . (21.73)

![](bbox=[0.15, 0.65, 0.8, 0.85])

Figure 21.7 The standing wave pattern on a square box top at three different times.