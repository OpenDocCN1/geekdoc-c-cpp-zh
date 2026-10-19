vertical directions must equal zero (Figure 6.2):

T₁ sin θ₁ − T₂ sin θ₂ − W₁ = 0 ,  (6.6)

T₁ cos θ₁ − T₂ cos θ₂ = 0 ,  (6.7)

T₂ sin θ₂ + T₃ sin θ₃ − W₂ = 0 ,  (6.8)

T₂ cos θ₂ − T₃ cos θ₃ = 0 .  (6.9)

Here Wᵢ is the weight of mass i and Tᵢ is the tension in string i. Note that because we do not have a rigid structure, we cannot assume the equilibrium of torques.

# 6.1.2

# Algorithm: Multidimensional Searching

Equations (6.1)–(6.9) are nine simultaneous nonlinear equations. While linear equations can be solved directly, nonlinear equations cannot (Press et al., 1994). You can use the computer to search for a solution by guessing, but there is no guarantee of finding one.

Unfortunately, not everything in life is logical, as we need to use a search technique now that will not be covered until Chapter 7. While what we do next is self-explanatory, you may want to look at Chapter 7 now if you are not at all familiar with searching.

We apply to our set the same Newton–Raphson algorithm as used to solve a single equation by renaming the nine unknown angles and tensions as the subscripted variable yᵢ and placing the variables together as a vector:

y = [x₁ x₂ x₃ x₄ x₅ x₆ x₇ x₈ x₉]ᵀ = [sin θ₁ sin θ₂ sin θ₃ cos θ₁ cos θ₂ cos θ₃ T₁ T₂ T₃]ᵀ .  (6.10)

The nine equations to be solved are written in a general form with zeros on the right-hand sides and placed in a vector:

fᵢ(x₁, x₂, …, x_N) = 0 ,   i = 1, N ,  (6.11)