
Figure 4.33: A piece of more complex filter to examine.

In Chapter 7, we will implement a filter that has a PFB delay-loop with filters in both feed-forward and feedback paths shown in Figure 4.33. The gain $K2$ is 1.0. There is a LPF in the forward band and a HPF in the reverse band. Both filters are first order. Initially, the LPF and HPF have the same cutoff frequency $f_c$ therefore they have the same $G$ value, based solely on cutoff frequency. In the equations, they will share the same $G$ but each will have their own values, $S3$ for LPF2 and $S2$ for HPF1. The reason for indexing them will become evident in Chapter 7, where there are other filtering blocks in the complete structure.

Let's derive the equation for $u$, the input to LPF2. You can see that the final output of the filter $y$:

First, define the filter equations for each component:

Now form $u$:

Figure 4.34: The realization of the filter in Figure 4.33 with delay-less respect loops.

Let $\alpha$ be a scaling factor:

By using these $\beta$ coefficients we can alter the structure of the VA filter to incorporate a feedback output port that will simplify processing in the filter. This is covered in Chapter 7. The final structure is shown in Figure 4.34. Once again, verify that the value of the input $u$ is correct by tracing through the filter. Use the Modified Härmärt method and Equation 4.39 to verify the results.

```
$u_{in} = \frac{x+K_1K_2G_1+K_2S_2}{1+K_1K_2G_1}, \quad u_{out} = \frac{x-K_1K_2G_1-K_2S_2}{1+K_1K_2G_1} \quad (4.59)$
```

## 4.15 Analog Signal Flow Graphs

We examine examples of analog signal flow diagrams in the beginning of the chapter. Another kind of signal diagram exists a signal flow graph. It graphically describes filters in feed-forward and feedback paths connected together

![](img/b42d0dca53f4a889d8162d55f7c8c05d_243_0.png) with nodes. The transfer functions of each filter component labeled $T_{NM}$, where $N$ is the input node and $M$ is the output, so $T_{13}$ would be the transmission from node 1 to node 3. In our example shown in Figure 4.33, we had a LPF in the feed-forward path and an HPF in the feedback path. The signal flow graph for this is shown in Figure 4.35. Notice the way the nodes are numbered; the input is always node 1, the output is node 2 and the rest of nodes are serialized in the loop starting with node 3.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_244_0.png)

$y = Ky_3$

$HPF1$
$LPF2$
$y_2 = y-(Gy+S2)$
$y_3 = Gu+S3$
$= y-Gy-S2$
$S3 = \frac{s_1}{1+g}$

$S2 = \frac{s_2}{1+g}$
$y = K(Gu+S3)$
$y_2 = y-Gy-S2$
$u = x+y_1$
$= x+y-Gy-S2$
$= x+KGu+KS3-G(KU+S3)-S2$
$= x-S2+S3(K-KG)$
$= 1-KG+KG'$

(4.60)

(4.61)

Typically, the labels LPF1 and HPF1 (which stand for first order LPF and HPF) are left out of the diagram; it is up to the reader to recognize the $T$ values; after some practice this is relatively easy. Mason's gain equation lets you write the analog transfer function of the system graph off the graph.

For this simple graph:

For this kind of simple block diagram/signal flow, Mason's gain equation rules are:

- the numerator is the product of all feed-forward transmissions (a.k.a. feed-forward gains)
- the denominator is [1 - (sum of all loop transmissions (a.k.a. loop gains))] taken one at a time], which is done by tracing each loop and multiplying the transmissions. This is similar but not identical to step three of the Modified Härmäd method.

Notice that the loop include any forward transmission in the loop, the loop gain of the simple feedback loop in Figure 4.35 is $T_{34}$ (forward) times $T_{33}$ (reverse). In more complex Signal Graphs, both numerator and denominator are augmented with more factors. A complete analysis is beyond the scope of this but may be found in any good analog filtering book such as (Lindquist, 1977). We will use this Signal Graph as a visual aid when discussing block diagrams in Chapter 7, but you won't need to solve any of these equations; they are here only to show that analog filters may be described and solved in this manner rather than using the analog block diagrams. In fact, you can convert analog signal graph directly into a virtual analog filter. As an example, let's analyze another simple flow graph from the analog state filter shown in Figure 4.36(a). The signal flow graph is shown in Figure 4.36(b). For simplicity, we will let $\omega_c = 1$ and get the transfer function.

Figure 4.35: (a) The filter in Figure 4.33 with nodes renumbered and (b) the resulting flow graph.

Figure 4.36: (a) The state variable filter with nodes renumbered and (b) the resulting Graph.

From the state variable filter, you can read directly that the normalized transmissions (or transfer functions) between nodes are: Then using Mason's Equation we can derive the transfer function as:

## 4.16 Wave

```
$$\alpha_0 = \frac{1}{1-KG+KG^2}$$
then: $u = \alpha_0(x-S_2+S_3(K-KG))$$
define: $S_2=\beta_2, S_3=\beta_3, \beta_2=\frac{-1}{1+g}, \beta_3=\frac{K-KG}{1+g}$
then: $u=\alpha_0(x+\beta_2+\beta_3)$
```

```
$H(s) = \frac{KT_{10}}{1-KT_{10}}$
```

## Shaping

Wave shaping uses a non-linear function to process and deliberately distort an input signal. We will use in Chapter 5 to change the shape of an oscillator's output. All of the filters in Chapter 7 have a Nonlinear Processing (NLP) block that may be enabled. This saturates the signal with soft clipping. In several of the filter models, the clipping comes from diodes in the original circuits. In others it is built into the analog circuit specifically as the hyperbolic tangent function, tanh(). There are many wave shaping to choose from. From more harmonic distortion we will be specifically focusing on soft-wave shapers, which produce less distortion and attempt to limit the signal in a way that is still pleasing to the ear. Figure 4.37(a) shows a perfectly linear amplitude transfer function (ATF) and the ATF of the hyperbolic tangent function. In others, the x-axis represents the input signal and the y-axis is output signal. The range of values we use is -1 to +1 on both axes. In the perfectly linear function, the output equals input from -1 and is clamped at these extremes. The tanh(x) function in Figure 4.37(b) saturates the signal, clipping it at +/-0.8 for an input signal from -1 to +1.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_245_0.png)
![](img/b42d0dca53f4a889d8162d55f7c8c05d_245_1.png)

```
$T_{34} = T_{40} = \frac{1}{s}, T_{45} = -2\zeta, T_{51} = -1$
```

```
$H(s) = \frac{T_{10}T_{20}}{1-(T_{20}T_{30}+T_{34}T_{45}T_{51})}=\frac{1-\frac{2\zeta}{s}+\frac{1}{s^2}}}{1-\frac{1}{s^2+2\zeta s+1}}$
```

![](img/b42d0dca53f4a889d8162d55f7c8c05d_246_0.png)
![](img/b42d0dca53f4a889d8162d55f7c8c05d_246_1.png) and (c) tanh(kx) with k = 1, 2.5 and 5.

The limiting of the signal to about +/-0.8 roughly corresponds to the way diode works. They saturate (or limit) the signal to a smaller than the actual total operating range of the circuit, but the shape of the transfer function depends on the device construction. In Figure 4.38(c) you can see that amplifying the input x to the tanh function can produce outputs that are out of range of -1 to +1 and also thus more harmonic distortion. In the projects that use NLP, we refer to amplifying as the saturation control. You can experiment with a more efficient numerical approximation to tanh() called fasttanh(), available in synthfunctions.h.

The problem with nonlinear wave shaping is that it will always cause aliasing in the signal. If the nonlinearity is small, this not be a problem. However if the saturation variable is increased, or a more nonlinear function is used, the aliasing effects will begin to stand out. How to mitigate this is oversampling techniques. Figure 4.38 shows more wave shaping functions you can experiment with. Figure 4.38(a) is an algorithm that Yamaha and Suyama put in 1996 for the purposes of generating tube-like distortions. In the range of -1 to +1 it produces a very soft clip. Figure 4.38(b) shows a normalized arctan(x) wave shape.
