
To form the transfer function H(z), take the z-Transform of Equation 4.5 by inspection:

```
y(n) = x(n - M)
apply z-Transform
y(n) \rightarrow Y(z)
x(n - M) \rightarrow X(z)z^{-M}
so
Y(z) = X(z)z^{-M}
H(z) = \frac{Y(z)}{X(z)} = z^{-M}  (4.7)
```

## 4.4 Digital Differentiation

We will see few oscillators with digital differentiators in them. The differentiator takes the time derivative of the signal. Since the derivative represents the rate of change, the differentiator's output is the current (or instantaneous) slope of the signal. This is easy to find the slope mi is:

```
\frac{\Delta y}{\Delta x}  (4.8)
```

For our digitized signal, the change in x is constant between points, so the digital differentiator will be providing:

```
\frac{\Delta y}{sample}  (4.9)
```

Since the change in y is the difference between the current and last input values, we can fashion the differentiator easily as shown in Figure 4.5.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_221_0.png)

Figure 4.5: A simple digital differentiator outputs the slope between the current and last inputs.

## 4.5 Analog and Digital Integration

Analog integrators integrate over continuous time; they calculate the area under the signal's curve. The traditional analog integrator circuit consists of an op-amp with a capacitor in the feedback path (if you don't know what that means, don't worry—worry that you're not analyzing it). You can think of the charge on a capacitor as the integrating component. The transfer function of an analog integrator shown in the block diagram in Figure 4.6 is found by applying x(t) as a complex sinusoid to form an output y(t) when taking the Laplace transform.

Figure 4.6: An analog integrator and its Laplace transform block diagram.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_222_0.png)
![](img/b42d0dca53f4a889d8162d55f7c8c05d_222_1.png)
![](img/b42d0dca53f4a889d8162d55f7c8c05d_222_2.png)
![](img/b42d0dca53f4a889d8162d55f7c8c05d_222_3.png)

Figure 4.7: Three simple digital integrators (Lindquist, 1989) showing the vintegration approximation over one sample interval.

To find the transfer function, let the input to the analog system be $e^{st}$, integrate, and apply Laplace by inspection:

analog equation: $y(t) = \int x(t)dt$ let $x(t) = e^{at}$ $y(t) = \int e^{at}dt$ $y(t) = \frac{1}{a}e^{at}$ applying Laplace: $y(t) \rightarrow Y(s)$ $x(t) \rightarrow X(s)$ $Y(s) = \frac{X(s)}{s}$ $Y(s) = \frac{Y(s)}{s}$ (4.10)

The integrator's transfer function is H(s) = 1/s, and it is evaluated by $s=ju$. As $\omega$ increases, $H(s)$ decreases. When $\omega=0$, $H(s)$ is infinite. A digital integrator seeks to perform this function, calculating the area under a discrete "curve" (step-stairs). The closer the integrator's output is to the actual area, the better it performs. Digital integrators must approximate this area since they only have discrete points to deal with.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_223_0.png)

**Figure 4.8:** The output of the forward Euler integrator (solid dark line) over several samples; the positive (grey) blocks add to the running total while the negative (white) blocks subtract from it.

There are three common digital integrators: the forward Euler, backwards or reverse Euler, bilinear integrators. The forward and backwards Euler integrators are simple to implement but do a poor job of approximating the area under the curve, as they are zero-order hold functions. This is shown in Figure 4.7. T is the signal period. For simplicity, we normalize the equations so that T = 1.

**Figure 4.8** shows a demonstration of an analog curve and a step-by-step visual demonstration of the forward Euler integrator; these rectangles produce the area under the curve, or the integration of the signal. In Figure 4.8, the positive rectangles are shaded grey and the negative ones are white. The positive chunks add together the running sum. On the first sample $n=0$, we let $x(n-1)=0$. Each successive output is the sum of the previous outputs (plus or minus) the current input.

**Figure 4.8** is revealing: some people think an integrator is a smoother, but this is only only the case when it is 0. In a combined kind of block diagram we will discuss shortly. If you look at the complete plot, you see that it covers two of "cycles" of the input signal. At the point we stop, the instantaneous integration value is 0.0, which makes sense, since those cycles were constructed with two sinusoids with the second cycle in amplitude. Since sinusoids have the same positive area as negative area, we expect the total area to be 0.0 over the period of one cycle. This happens twice in the pulse, at the end of each cycles where the instantaneous area is 0.0.

In Figure 4.7 the bilinear integrator approximates the area under the curve using trapezoid and produces the most accurate result of the three. It will be our digital integrator of choice. We will then find the reverse Euler integrator in a few algorithms. The bilinear integrator is also known as the Tustin integrator or the trapezoidal integrator. It is called bilinear because it was composed of linear equations.

## 4.6 The Bilinear Z-Transform

There are two approaches to converting analog filters into digital. The first approach (classical) makes use of bilinear transform. The second approach (Virtual Analog) makes use of the bilinear integrator. Both methods result in filters that identical frequency responses, but the benefits of using the virtual analog will become apparent.

To find the transfer function of bilinear integrator, use the rules you have amassed and apply them to the difference equation in Figure 4.7.

```
y(n) = y(n-1) + \frac{T}{2}[x(n) + x(n-1)]\rightarrow Y(z) = y(z)z^{-1} + \frac{T}{2}[X(z) + X(z)z^{-1}]

Y(z)[1-z^{-1}] = \frac{T}{2}X(z)[1+z^{-1}]
H(z) = \frac{Y(z)}{X(z)} \frac{T}{2-z^{-1}}  (4.11)
```

The idea behind the Bilinear Z-Transform is that if digital integrator H(z) is approximating analog H(s) = 1/s, then we have a solid relationship between z and s.

```
H(s) = \frac{1}{s}
H(z) = \frac{1}{T} \frac{z-1}{z+1}  (4.12)
```

Means could take an analog transfer function H(s) and replace it with 2/T(z-1)/(z+1). This should produce a transfer function H(z) in the digital domain that corresponds to H(s) in the analog domain.

It would appear that such a deal is not perfect, and we do not firstly. At low frequencies, the mapping is very close, but as the frequency increases, an error in the mapping increases with the tangent or tan(1) function. Secondly, it is to map an infinite number of analog frequencies to a finite number of digits, and this does in this fractal manner, smashing and fading of all the analog frequencies to a tiny area near Nyquist. Moreover, it maps frequencies at infinity directly to Nyquist. See Designing Audio Effects Plug-Ins in C++ for a detailed discussion.

The consequence of this first issue is to pre-warp the analog frequency domain so that after the transformation, the digital frequency response is obtained. The mapping equation is:

```
\omega_s = \tan \frac{\omega_a T}{2}}
\omega_a = the prewarped analog frequency
\omega_s = the desired digital frequency
T = the sample period  (4.13)
```
