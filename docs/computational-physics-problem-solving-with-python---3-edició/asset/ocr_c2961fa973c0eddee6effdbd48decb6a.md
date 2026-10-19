# 24.4

# Including Dispersion

We have just seen that Burgers’ equation can turn an initially smooth wave into a square-edged shock wave. An inverse wave phenomenon is dispersion, in which a waveform disperses or broadens as it travels through a medium. Dispersion does not cause waves to lose energy and attenuate, but rather to lose information with time. Physically, dispersion may arise when the propagating medium has structures with a spatial regularity equal to some fraction of a wavelength. Mathematically, dispersion may arise from terms in the wave equation that contain higher order space derivatives. For example, consider the waveform

u(x, t) = e^{±i(kx - ωt)}  (24.17)

corresponding to a plane wave traveling to the right (“traveling” because the phase kx − ωt remains unchanged if you increase x with time). When this u(x, t) is substituted into the advection equation (24.3), we obtain

ω = c k .  (24.18)

This equation is an example of a dispersion relation, that is, a relation between frequency ω and wave vector k. Because the group velocity of a wave

v_g = ∂ω/∂k ,  (24.19)

the linear dispersion relation (24.18) leads to all frequencies having the same group velocity c and thus dispersionless propagation.

Let us now imagine that a wave is propagating with a small amount of dispersion, that is, with a frequency that has somewhat less than a linear increase with the wave number k:

ω ≈ c k − β k³ .  (24.20)

Note that we skip the even powers in (24.20), so that the group velocity,

v_g = dω/dk ≈ c − 3β k² ,  (24.21)

is the same for waves traveling to the left the or the right. Now we work backward. If plane-wave solutions like (24.17) were to arise from a wave equation, then (as verified by substitution) the ω term of the dispersion relation (24.20) would arise from a first-order time derivative, the c k term from a first-order space derivative, and the k³ term from a third-order space derivative:

∂u(x, t)/∂t + c ∂u(x, t)/∂x + β ∂³u(x, t)/∂x³ = 0 .  (24.22)

We leave it as an exercise to show that solutions to this equation do indeed have waveforms that disperse in time.