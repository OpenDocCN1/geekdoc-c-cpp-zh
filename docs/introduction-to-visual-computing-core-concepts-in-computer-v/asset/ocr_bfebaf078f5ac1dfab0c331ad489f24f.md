![](bbox=[0.15, 0.18, 0.88, 0.23])

Figure 3.3. This figure illustrates the effect of cascading convolutions.

![](bbox=[0.15, 0.32, 0.88, 0.38])

Figure 3.4. This figure illustrates the effect of combination of parallel convolutions.

This means that if a function x undergoes two different convolutions in parallel with b and c which are then combined, the same effect can be obtained by designing a new kernel d by adding b and c (d = b + c) and then undergoing a single convolution with this new kernel d (Figure 3.4).

# 3.2 Linear Filters

The next question to ask is how does knowing about convolution help us in any way? In fact, convolution can help us greatly in designing systems since instead of worrying about complex signals, we need to only worry about the simple δ function. If we can design the impulse response of a system, we know that convolving the input signal with impulse response would provide us with the correct answer for any general function.

Let us take the case of designing a filter (or impulse response) that will blur any general signal. To design this, we have to first think intuitively about what a blurred delta signal would look like. In other words, what would a linear system that blurs a signal produce when a delta is provided as its input. For this consider Figure 3.5. Delta is a function that has a single sample of value 1 at 0 which is essentially a sharp spike. Therefore, intuitively, blurring a delta function can be expected to produce a spike with a broader base and a smaller height. This is represented by a function that has multiple samples centered around 0 whose values are smaller than 1. Now the next question is, how much broader should the base be and how much shorter should the spike be? In fact, there can be many answers to this question. For example, it can be three samples centered at 0, each of value 0.7. Or, it can be five samples centered around 0, each of value 0.5. So, how do we constrain this problem to find an appropriate answer to these questions?

One way to constrain the problem may be to first fix the base of the spike