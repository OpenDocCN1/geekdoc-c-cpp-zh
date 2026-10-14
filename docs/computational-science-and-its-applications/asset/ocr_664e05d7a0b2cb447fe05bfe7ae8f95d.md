+   10. There are many good arguments why one should use Gabor windows (or Gabor atoms) from S₀(ℝᵈ) only (described as modulation space M¹(ℝᵈ) in [39]), among others, because this guarantees the Bessel property for Gabor systems with such windows for general lattices. This is also the basis for the discussion with respect to jitter errors and in particular a variation of lattices ([54, 55]);

+   11. Larsen’s book on the multiplier [56] provides a description of convolution operators (and also) of the corresponding transfer functions from Lᵖ(ℝᵈ) to Lᵠ(ℝᵈ) (1 ≤ p, q < ∞) using quasi-measures, as introduced by Gaudry [57, 58, 59]. But the (unlimited) global structure of quasi-measures (one could view this space equivalently as ℱLₗₒc^∞(ℝᵈ)). The introduction of the space S₀(ℝᵈ) helps us to come back to the expected statement: The transfer function is the Fourier transform of the impulse response (and vice versa);

+   12. There was a theory of transformable measures put forward by L. Argabright and J. Gil de Lamadrid, e.g. in their papers [60, 61, 62]. This can be also treated well in our context.

+   13. Another generalization of measures on multi-dimensional spaces are the so-called bimeasures, which appear in the following papers [63, 64, 65, 66, 67, 68, 69, 70, 71]. They also find a natural interpretation in our context;

+   14. In addition to the deterministic world of functions and signals questions arising in stochastic signal processing can be well treated in the context of the Banach Gelfand triple. While generalized functions allow average values over time to be described, stochastic processes define the change of statistical properties over time. Thus generalized stochastic processes combine these two features in a unified way. The following table captures the essence of this view-point.

| Toward Generalized Stochastic Processes |
|---|---|
| Ordinary Functions on ℝᵈ | Stochastic Processes on ℝᵈ |
| ℝᵈ ↦ ℂ | ℝᵈ ↦ 𝔛 |
| t ↦ f(t) | t ↦ X(t, ω) ∈ L²(Ω, Σ, P) |
| Generalized Functions | Generalized Stochastic Processes |
| C_c(ℝᵈ) ↦ ℂ | ρ : S₀(ℝᵈ) ↦ 𝔛 : f ↦ ρ(f) |
| k ↦ σ(f) := ∫_{ℝᵈ} k(x)f(x)dx | e.g., f ↦ ∫_{ℝᵈ} X(t, ω)k(t)dt |

Let us give a few references in that direction: [72], [73], with a recent summary in [74], or [75], [76], and in particular the papers by P. Wahlberg: [77], [78, 79, 80] and [81].

# 1.13 Summary

We are convinced that the theory of distributions is a central part of any mathematical foundation for signal processing. After all, for almost all the concrete situations signals are things that can be measured. Physical processes are not so much pointwise (almost everywhere) defined functions in the mathematical sense, even if the modelling using