so

(1 − B)(1 − B^s) y_t = (1 − θ₁ B − θ₂ B² − θ₃ B^{s+1}) a_t

with

θ₁ = 1 − α, θ₂ = δ(1 − α), and θ₃ = (1 − α)(δ − 1).

The moving average form of the model is

y_t = a_t + Σ_{j=1}^{∞} ψ_j a_{t−j} where ψ = { α for j mod s ≠ 0 ; α + δ(1 − α) for j mod s = 0 }

# Winters Method (Additive)

The model for the additive version of Winter's method is y_t = μ_t + β_t t + s(t) + a_t.

The smoothing equations in terms of weights α, γ, and δ are

L_t = α(y_t − S_{t−s}) + (1 − α)(L_{t−1} + T_{t−1}) , T_t = γ(L_t − L_{t−1}) + (1 − γ)T_{t−1} , and S_t = δ(y_t − L_t) + (1 − δ)S_{t−s}.

This model is equivalent to a seasonal ARIMA(0, 1, s+1)(0, 1, 0)s model

(1 − B)(1 − B²) y_t = (1 − Σ_{i=1}^{s+1} θ_i B^i) a_t

The moving average form of the model is

y_t = a_t + Σ_{j=1}^{∞} Ψ_j a_{t−j}

where

Ψ = { α + j α γ for j mod s ≠ 0 ; α + j α γ + δ(1 − α) for j mod s = 0 }