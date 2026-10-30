
## 3.2 基于深度学习的文本检测与识别

随着深度学习技术的快速发展，基于深度学习的文本检测与识别方法逐渐成为主流。这类方法通常利用卷积神经网络（CNN）和循环神经网络（RNN）等模型，自动学习图像中文本的视觉特征和序列特征，从而实现端到端的文本检测与识别。

在文本检测方面，基于深度学习的方法主要分为两类：基于候选区域的方法和基于语义分割的方法。基于候选区域的方法（如 Faster R-CNN、SSD 等）先生成可能包含文本的候选区域，然后对候选区域进行分类和回归，得到最终的文本检测框。基于语义分割的方法（如 FCN、U-Net 等）则直接对图像进行像素级分类，将文本区域与背景区域进行分割，再通过后处理得到文本检测框。

在文本识别方面，基于深度学习的方法通常采用序列到序列（Seq2Seq）模型，将文本图像转换为字符序列。其中，卷积神经网络用于提取图像特征，循环神经网络（如 LSTM、GRU）用于建模字符序列的上下文依赖关系，最后通过 CTC（Connectionist Temporal Classification）或注意力机制（Attention）进行序列解码，得到最终的文本内容。

近年来，端到端的文本检测与识别方法逐渐兴起，这类方法将检测和识别任务统一在一个深度学习模型中，通过共享特征提取网络，实现检测和识别的联合优化，从而提升整体性能。例如，FOTS（Fast Oriented Text Spotting）和 Mask TextSpotter 等方法在自然场景文本检测与识别任务中取得了显著的效果。

尽管基于深度学习的文本检测与识别方法取得了很大的进展，但仍然面临一些挑战，如复杂背景下的文本检测、多方向文本的识别、手写文本的识别等。未来的研究将更加注重模型的轻量化、实时性和鲁棒性，以满足实际应用的需求。

综上所述，基于深度学习的文本检测与识别方法在自然场景文本识别领域具有广阔的应用前景，随着技术的不断进步，其性能和应用范围将进一步提升。

appropriately. Given the right conditions, this numerical method is more efficient and converges faster to an approximate optimal solution: **quadratic convergence** versus the **linear convergence** of steepest ascent.

Newton’s Method for multivariable optimization searches is based on the single-variable root-finding algorithm. Modify the procedure to look for roots of the first derivative rather than roots of the original function:

$$x_{n+1}=x_n+\frac{f(x_n)}{f'(x_n)}\ \Longrightarrow\ x_{n+1}=x_n+\frac{f'(x_n)}{f''(x_n)}$$

and iterate until $|x_{n+1}-x_n|<\epsilon$ for our chosen tolerance $\epsilon>0$.

Extend the Modified Newton’s Method to several variables by using gradients and the Hessian, the matrix of second partial derivatives.

$$x_{n+1}=x_n+\left(f''(x_n)\right)^{-1}f'(x_n)\ \Longrightarrow\ x_{n+1}=x_n+\left(H(x_n)\right)^{-1}\nabla f(x_n)$$

now iterating until $\|x_{n+1}-x_n\|<\epsilon$ for our chosen tolerance $\epsilon>0$. Applying a little bit of linear algebra gives us the method as an algorithm.

```
**Modified Newton’s Method Algorithm**

Find the unconstrained maximum of the function $f:\mathbb{R}^n\to\mathbb{R}$.

**INPUTS:**

- Function: $f$
- Starting point: $x_0$
- Tolerance and Maximum Iterations: $\epsilon, N$

**OUTPUTS:** Maximal point $x^*$ and maximum value $f(x^*)$

**Step 1.** Initialize: Set $x=x_0$

**Step 2.** Calculate the gradient $\mathbf{g}=\nabla f(x)$ and $H=$ Hessian$(x)$

**Step 3.** Compute $d=|H|$ and create new matrices

$$H_1=\text{substitute }\mathbf{g}\text{ for column 1 of }H$$
$$H_2=\text{substitute }\mathbf{g}\text{ for column 2 of }H$$

**Step 4.** Compute: $\Delta x_1=|H_1|/d$ and $\Delta x_2=|H_2|/d$.

**Step 5.** Find the new point $x_{new}=\langle x_1+\Delta x_1,x_2+\Delta x_2\rangle$

**Step 6.** If $\|\langle\Delta x_1,\Delta x_2\rangle\|<\epsilon$, then STOP and return estimates $x^*=x_{new}$ and $f(x_{new})$.

Otherwise, set $x=x_{new}$ and return to Step 2.
```

Again, remember that $\|y\|=\|\langle y_1,y_2\rangle\|=\sqrt{y_1^2+y_2^2}$. Let’s repeat our examples for the steepest ascent method using Newton’s method. We’ll use the function $ModifiedNewtonMethod$ which is in the book’s PSMv2 package. Load the package via `with(PSMv2)`. The syntax of the `ModifiedNewtonMethod` function is

ModifiedNewtonMethod(f, (x₀, y₀), ε, N)

where *f* is the function, (x₀, y₀) is the starting vector, ε is the tolerance, and *N* is the maximum number of iterations allowed. The output of `ModifiedNewtonMethod` is a `DataFrame` containing the generated points, function values, Hessians, and the definiteness of the Hessian.

### Example 4.16. Modified Newton’s Method Example, I.

Maximize *f*(x) = 2x₁x₂ + 2x₂ − x₁² − 2x₂² to within ε = 0.01 starting at x₀ = ⟨0, 0⟩.

Limit the number of iterations to *N* = 20.

```
> f := x → 2x₁x₂ + 2x₂ − x₁² − 2x₂²:
> MNf := ModifiedNewtonMethod(f, ⟨0, 0⟩, 0.01, 20);
```

| SAf | k | xₖ | F(xₖ) | Hessian | definiteness |
|---:|---:|---|---:|---|---|
|  | 1 | [0, 0]ᵀ | 0. | [−2, 2; 2, 4] | negative_definite |
|  | 2 | [1, 1]ᵀ | 0. | [−2, 2; 2, 4] | negative_definite |
|  | 3 | [1, 1]ᵀ | 0. | [−2, 2; 2, 4] | negative_definite |

We have a maximum of *f* of 1 at (1, 1) since the Hessian is negative definite there.

On to the second example.

### Example 4.17. Modified Newton’s Method Example, II.

Maximize *g*(x) = 55x₁ − 4x₁² + 135x₂ − 15x₂² − 100 starting at the point (1, 1) to within a tolerance of ε = 0.01 limiting iterations to *N* = 20.

```
> g := x → 55x₁ − 4x₁² + 135x₂ − 15x₂² − 100:
> MNg := ModifiedNewtonMethod(g, ⟨1, 1⟩, 0.01, 20);
```

| SAg | k | xₖ | F(xₖ) | Hessian | definiteness |
|---:|---:|---|---:|---|---|
|  | 1 | [1, 1]ᵀ | 71. | [−8, 0; 0, −30] | negative_definite |
|  | 2 | [6.875, 4.500]ᵀ | 392.9 | [−8, 0; 0, −30] | negative_definite |
|  | 3 | [6.875, 4.500]ᵀ | 392.9 | [−8, 0; 0, −30] | negative_definite |

We have a maximum of \(g\) of 392.9 at \((6.875, 4.500)\) since the Hessian is negative definite there.

Now, for the third example.

### Example 4.18. Modified Newton’s Method Example, III.

Maximize \(h(x)=2x_1x_2+2x_2-e^{x_1}-e^{x_2}+10\) starting at the point \((0.8,0.8)\) to within a tolerance of \(\epsilon=0.01\) with no more than \(N=20\) iterations.

```
h := x -> 2x1x2 + 2x2 - e^x1 - e^x2 + 10:
MNg := ModifiedNewtonMethod(h, (0.8, 0.8), 0.01, 20);
```

| SA_g | \(x_k\) | \(F(x_k)\) | Hessian | definiteness |
|---:|---|---:|---|---|
| 1 | [0.8, 0.8] | 8.428 | [-2.226, 2; 2, -2.226] | negative_definite |
| 2 | [2.224, 2.697] | 3.306 | [-9.241, 2; 2, -14.83] | negative_definite |
| 3 | [1.669, 2.057] | 7.851 | [-5.306, 2; 2, -7.820] | negative_definite |
| 4 | [1.288, 1.642] | 8.723 | [-3.264, 2; 2, -5.164] | negative_definite |
| 5 | [1.088, 1.450] | 8.825 | [-2.968, 2; 2, -4.265] | negative_definite |
| 6 | [1.034, 1.404] | 8.829 | [-2.813, 2; 2, -4.073] | negative_definite |
| 7 | [1.031, 1.402] | 8.827 | [-2.803, 2; 2, -4.061] | negative_definite |

We have a maximum of \(h\) of 8.827 at \((1.031, 1.402)\) since the Hessian is negative definite there.

Even though Newton’s method is faster and more direct, we must be cautious. The method requires a relatively good starting point. Try searching for a maximum for \(h\) starting at \((0.5,0.5)\) and looking at just the last entry in the *DataFrame* report.

```
MNh2 := ModifiedNewtonMethod(h, (0.5, 0.5), 0.01, 20):
MNh2[-1, ..];
```

|  |  |
|---|---|
| \(x_k\) | [-0.2667, 0.3829] |
| \(F(x_k)\) | 8.329 |
| Hessian | [-0.7659, 2; 2, -1.467] |
| definiteness | indefinite |

We started at \((0.5, 0.5)\), not far from our original \((0.8, 0.8)\). But the Hessian being indefinite tells us that we’ve found an approximate saddle point, not a maximum. Modified Newton’s method is very sensitive to the initial value chosen.

## Comparisons of Methods

We compared these two routines finding that Modified Newton’s Method converges faster than the gradient method. Table 4.4 shows the comparison.

**TABLE 4.4: Comparison of the Steepest Ascent and Modified Newton’s Methods**

|   | Initial Value | Iterations | Solution | max $f(x)$ |
|---|---|---:|---|---:|
| Steepest Ascent | $(0,0)$ | 16 | $(0.9922, 0.9961)$ | 1.0 |
| Modified Newton | $(0,0)$ | 2 | $(1.0, 1.0)$ | 1.0 |

|   | Initial Value | Iterations | Solution | max $g(x)$ |
|---|---|---:|---|---:|
| Steepest Ascent | $(0,0)$ | 4 | $(-0.266, 0.385)$ | 8.3291 |
| Modified Newton | $(0,0)$ | 2 | $(-0.269, 0.381)$ | 8.3291 |

|   | Initial Value | Iterations | Solution | max $h(x)$ |
|---|---|---:|---|---:|
| Steepest Ascent | $(0.5, 0.5)$ | 6 | $(1.025, 1.397)$ | 8.828 |
| Modified Newton | $(0.8, 0.8)$ | 7 | $(1.031, 1.402)$ | 8.827 |

As a final comparison, add the modified Newton’s method points to the contour map showing the steepest ascent points for $g$ or Figure 4.12 to obtain Figure 4.13 below.

![](img/0f04050177d82aebd17d3383d7334896_174_0.png)

When given a good starting value, a Modified Newton’s method search is much faster and more direct than a steepest ascent gradient method.

## Exercises

- 1. Maximize $f(x)=2x_1x_2-2x_1^2-2x_2^2$ to within a tolerance of 0.1.
  - a. Start at the point $x=\langle1,1\rangle$. Perform 2 complete iterations of the steepest ascent gradient search. For each iteration clearly show $x_n$, $x_{n+1}$, $\nabla f(x_n)$, and $t^*$. Justify that the process will eventually find the approximate maximum.
  - b. Use Newton’s method to find the maximum. Starting at $x=\langle1,1\rangle$. Clearly show $x_n$, $x_{n+1}$, $\nabla f(x_n)$, and the Hessian for each iteration. Indicate when the stopping criterion is achieved.

- 2. Maximize $f(x)=3x_1x_2-4x_1^2-4x_2^2$ to within a tolerance of 0.1.
  - a. Start at the point $x=\langle1,1\rangle$. Perform 2 complete iterations of the steepest ascent gradient search. For each iteration clearly show $x_n$, $x_{n+1}$, $\nabla f(x_n)$, and $t^*$. Justify that the process will eventually find the approximate maximum.
  - b. Use Newton’s method to find the maximum. Starting at $x=\langle1,1\rangle$. Clearly show $x_n$, $x_{n+1}$, $\nabla f(x_n)$, and the Hessian for each iteration. Indicate when the stopping criterion is achieved.
