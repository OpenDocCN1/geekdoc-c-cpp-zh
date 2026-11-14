
![](img/b54974d0a4317ec82d7ae02126d10a6f_106_0.png)

Figure 5.1: Sine, cosine, and sinusoid signals.

Euler's equation is shown below:

```
e^{j\theta} = \cos(\theta) + j\sin(\theta)
j = \sqrt{-1}
(5.2)
```

You can see that it includes both sine and cosine functions. The j term is the imaginary number, the square root of -1 (mathematicians call it i but since that represents current in engineering, we rename it j instead). The j is known as the phase rotation operator; multiplying a function by j rotates the phase by 90 degrees.

Suppose you want to shift the phase of a waveform by 180°, thereby inverting it. Mathematically, you can do this by multiplying the waveform by -1, inverting the values of all its points. Suppose you wanted to invert the waveform again (which would bring it back to its original shape)—you could do that by multiplying by -1 again. But suppose that you only wanted to shift the phase by 90°? Is there a number (η) you could use as a multiplier to shift by 90°? In other words,

```
90-degree shifted waveform = (original waveform) (η)
```

You don't know what η is yet, but you can figure it out. Suppose you then wanted to shift the waveform by another 90 degrees, which would be the same as shifting the original waveform by 180 degrees. You would multiply it by η again. You'd then have the following:

```
180-degree shifted waveform = (original waveform) (η)(η)
= (original waveform) (η)²
= (original waveform) (-1)
```

This leads to Equation 5.3:

\(\eta^2 = -1\)
\(\eta = \sqrt{-1} = j\)
(5.3)

So, you can perform a conceptual 90-degree phase shift by multiplying a waveform by \(j\). A \(-90\)-degree phase shift is accomplished by multiplying by \(-j\). Some other useful relationships with \(j\) are

\(j^2 = -1\)
\(\frac{1}{j} = -j\)
(5.4)

Euler's equation is complex and contains a real part (cos) and imaginary part (sin), and the plus sign (+) in the equation is not a literal addition—you can't add real and imaginary numbers together. In a complex number of the format A + jB, the two parts coexist as part of one complex number.

For our purposes, we replace the \(\theta\) with \(\omega t\) instead, where \(\omega\) is the frequency in radians/second and \(t\) is the time variable. Plug in various values for \(t\) and you get the plot in Figure 5.1 when you plot the sine and cosine in the same plane. So, we will reject using the sin() and cos() functions independently and adopt the complex sinusoid as a prepackaged mixture of the two. The reason is partly mathematical—as it turns out, \(e\) is simple to deal with mathematically. You only need to learn four rules (Equation 5.5) in addition to Euler's equation.

Euler's equation: \(e^{j\omega t} = \cos(\omega t) + j\sin(\omega t)\)

The four rules:

```
e^a e^b = e^{(a+b)} or e^{ja} e^{jb} = e^{j(a+b)}
\frac{e^a}{e^b} = e^{(a-b)} or \frac{e^{ja}}{e^{jb}} = e^{j(a-b)}
\frac{d(e^{at})}{dt} = ae^{at}
\int e^{at} dt = \frac{1}{a} e^{at}
```
(5.5)

> So, what Euler's equation is really describing is a sine and cosine pair of functions, coexisting in two planes that are 90 degrees apart. The word orthogonal is the engineering term for 90 degrees apart.

The two equations in Equation 5.5 demonstrate that \(e\) behaves like a polynomial (\(x^2 * x^5 = x^7\)) even when the argument is a function of time, \(t\). Equation 5.5 also shows how simply it behaves in calculus—multiple derivatives or integrations are done by simply multiplying the argument's constant (a or 1/a) over and over. Before we leave this topic, make sure you remember how to deal with complex numbers—you'll need it to understand where the frequency and phase responses come from.

## 5.2 Complex Math Review

Because a complex number has both real and imaginary parts, it cannot be plotted on a single axis. In order to plot a complex number, you need two axes: a real and imaginary axis. The two axes are aligned at right angles, just like the x- and y-axes in two-dimensional geometry. They are orthogonal. The x-dimension is the real axis (Re), and the y-dimension is the imaginary axis (Im). So, a complex number is plotted as a point on this x-y plane, also called the complex plane. Complex numbers are usually written in the form A + jB where A is the real part and B is the imaginary part. Notice that the notation always stays in the form A + jB even when common sense might contradict it. For the point in the second quadrant, you still write -2 + j2 even though j2 - 2 might look nicer. Also notice that you write 2 - j1 instead of just 2 - j. The points are plotted the way you would plot (x, y) pairs in a plane (Figure 5.2).

This example plots points as (x + jy) pairs; this is called the Cartesian coordinate system. You can also use polar notation to identify the same complex numbers. In polar notation, you specify the radius (R) and angle (θ) for the vector that results from drawing a line from the origin of the axes out to the point in question. For example, consider the point 2 + j3 above. You could plot this point in polar form as shown in Figure 5.3.

We are leaving the Cartesian form (2 + j3) for reference. Normally, all you would see is R and θ. Most engineers prefer polar notation for dealing with complex numbers. The polar number is often written as R ∠ θ. Fortunately for us, the conversion from Cartesian to polar notation is simple. Starting with a complex number in the form A + jB, you can find the resulting radius and angle from Equations 5.6 and 5.7.

![](img/b54974d0a4317ec82d7ae02126d10a6f_108_0.png)

Figure 5.2: Several points plotted in the complex plane using the Cartesian (x, y) coordinate system.

![](img/b54974d0a4317ec82d7ae02126d10a6f_108_1.png)

Figure 5.3: Plotting 2 + j3 in polar form.

```
R = \sqrt{A^2 + B^2} (5.6)
\theta = \tan^{-1} \left[ \frac{B}{A} \right] (5.7)
```

The radius (\(R\)) is sometimes called the *magnitude* and the angle \(\theta\) is called the *argument*. You sometimes only care about the square of the magnitude (called the “magnitude-squared” or \(|R|^2\)) (Equation 5.8).

```
|R|^2 = A^2 + B^2 (5.8)
```

Equation 5.9 shows how to extract the magnitude and phase from a transfer function.

```
H = \frac{\text{num}}{\text{denom}}
```

then

```
|H| = \frac{|\text{num}|}{|\text{denom}|} (5.9)
```

and

```
Arg(H) = Arg(num) - Arg(denom)
```

> The frequency response plots of filters are actually magnitude responses of a complex function called the *transfer function* of the filter. The phase response plots are actually argument responses of this function. The transfer function is complex because it contains complex numbers; many transfer functions are actually quite simple. We use the letter H to denote a transfer function.

## 5.3 Time Delay as a Math Operator

The next piece of DSP theory you need to understand is the concept of time delay as a mathematical operator. This will be pretty easy since we are going to exploit the simple mathematical behavior of the \(e^{j\omega t}\) function. First, consider a complex sinusoid and a delayed complex sinusoid (Figure 5.4).

How does the delay of \(n\) seconds change the complex sinusoid equation? Since positive time goes in the positive \(x\) direction, a delay of \(n\) seconds is a shifting of \(-n\) seconds. In the complex sinusoid equation, you would then replace \(t\) with \(t-n\). In other words, any point on the delayed curve is the same as the nondelayed curve minus \(n\) seconds. Therefore, the delayed sinusoid is

```
Delayed sinusoid = e^{j\omega(t-n)} (5.10)
```

But, by using the polynomial behavior of \(e\) and running Equation 5.5 in reverse, you can rewrite it as shown in Equation 5.11:

```
e^{j\omega(t-n)} = e^{j\omega t} e^{-j\omega n} (5.11)
```

It’s a subtle mathematical equation but it says a lot: if you want to delay a complex sinusoid by \(n\) seconds, multiply it by \(e^{-j\omega n}\)—this allows us to express time delay as a mathematical operator.

In the last two sections you've learned that phase rotation and time delay can both be expressed as mathematical operators.

> Time delay can be expressed as a mathematical operator by multiplying the signal to be delayed \(n\) seconds by \(e^{-j\omega n}\). This is useful because \(e^{-j\omega n}\) is not dependent on the time variable. In discrete-time systems, the \(n\) refers to samples rather than seconds.

![](img/b54974d0a4317ec82d7ae02126d10a6f_110_0.png)

Figure 5.4: A complex sinusoid \(e^{j\omega t}\) and another one delayed by \(n\) seconds.

## 5.4 First-Order Feed-Forward Filter Revisited

Being able to express delay as the mathematical operation of multiplication by \(e^{-j\omega n}\) means you can take the block diagram and difference equation for a DSP filter and apply a sinusoid to the input in the form of \(e^{j\omega t}\) rather than having to plug in sequences of samples as you did in Chapter 4. Then, you can see what comes out of the filter as a mathematical expression and evaluate it for different values of \(\omega\) (where \(\omega = 2\pi f\) with \(f\) in Hz) to find the frequency and phase responses directly rather than having to wait and see what comes out then try to guesstimate the amplitude and phase offsets. Consider the first-order feed-forward filter from the last chapter but with \(e^{j\omega t}\) applied as the input signal, shown in a block diagram in Figure 5.5.

The difference equation is as follows:

```
$$y(t) = a_0 e^{j\omega t} + a_1 [e^{j\omega t} e^{-j\omega 1}]$$ (5.12)
```

Figure 5.5 shows the familiar block diagram but this time with the input \(x(t)\) and output \(y(t)\) instead of \(x(n)\) and \(y(n)\). Notice the delay element has been replaced by \(e^{-j\omega 1}\) since there is a one-sample delay.

When you apply the complex sinusoid \(e^{j\omega t}\) to the input, the difference equation uses the delay-as-multiplication operation to produce the output. With a little math you can arrive at Equation 5.13.

```
$$y(t) = a_0 e^{j\omega t} + a_1 [e^{j\omega t} e^{-j\omega 1}]$$
$$= e^{j\omega t} (a_0 + a_1 e^{-j\omega 1})$$ and the input $x(t) = e^{j\omega t}$ so
$$y(t) = x(t) (a_0 + a_1 e^{-j\omega 1})$$ (5.13)
```

The transfer function is defined as the ratio of output to input, therefore
