b) Verify that the eigenvector for λ₁ = 5 is proportional to

x₁ = 1/√6 ⎛ -1 ⎞
                ⎜ -2 ⎟
                ⎝ +1 ⎠ .  (6.39)

c) The eigenvalue −3 corresponds to a double root. This means that the corresponding eigenvectors are degenerate, which in turn means that they are not unique. Two linearly independent ones are

x₂ = 1/√5 ⎛ -2 ⎞ ,  x₃ = 1/√10 ⎛ 3 ⎞
                ⎜ +1 ⎟           ⎜ 0 ⎟
                ⎝ +0 ⎠           ⎝ 1 ⎠ .  (6.40)

In this case, it is not clear what your eigenproblem solver will give for the eigenvectors. Try to find a relationship between your computed eigenvectors with the eigenvalue −3 and these two linearly independent ones.

5. Imagine that your model of some physical system results in N = 100 coupled linear equations in N unknowns:

a₀₀ y₀ + a₀₁ y₁ + ⋯ + a₀(N−1) y_{N−1} = b₀ ,
 a₁₀ y₀ + a₁₁ y₁ + ⋯ + a₁(N−1) y_{N−1} = b₁ ,
 ⋮
 a_{(N−1)0} y₀ + a_{(N−1)1} y₁ + ⋯ + a_{(N−1)(N−1)} y_{N−1} = b_{N−1} .

In many cases, the a and b values are known, so your exercise is to solve for all the x values, taking a as the Hilbert matrix and b as its first column:

[a_{ij}] = a = [ 1/(i + j − 1) ] = ⎛ 1   1/2  1/3  1/4  …  1/100 ⎞
                                   ⎜ 1/2 1/3  1/4  1/5  …  1/101 ⎟
                                   ⎜ ⋮   ⋮    ⋮    ⋮      ⋮   ⎟
                                   ⎝ 1/100 1/101 …   …   1/199 ⎠ ,

[b_i] = b = [1/i] = ⎛ 1 ⎞
                     ⎜ 1/2 ⎟
                     ⎜ 1/3 ⎟
                     ⎜ ⋮   ⎟
                     ⎝ 1/100 ⎠ .

Compare to the analytic solution

⎛ y₁ ⎞   ⎛ 1 ⎞
⎜ y₂ ⎟ = ⎜ 0 ⎟
⎜ ⋮  ⎟   ⎜ ⋮ ⎟
⎝ y_N⎠   ⎝ 0 ⎠ .  (6.41)