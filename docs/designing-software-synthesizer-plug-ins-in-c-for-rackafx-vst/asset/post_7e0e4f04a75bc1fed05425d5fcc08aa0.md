
MIDI Manufacturers Association. 2006. Downloadable Sounds Level 2. Amendment 2.

MIDI Manufacturers Association. "Tutorial: History of MIDI." Accessed June 2014, http://www.midi.org/aboutmidi/tut_history.php

Smith, Dave and Wood, Chet. 1981. The 'USI' or Universal Synthesizer Interface. 70th Audio Engineering Society Convention, Preprint 1845.

Since we are designing synthesizers, an obvious place to start working on the modules would be the analog world since the original modules were analog. We would like to make analog equivalents in the digital domain. In this chapter we discuss two ways to do this, with the majority of time spent on the latter named Virtual Analog. Chapter 7, we will be implementing the synth filters from Chapter 1 (lowpass, highpass, bandstop), and we need to get the signal processing theory out of the way. In Analog Chapter 5, a few of our oscillator designs will also use some signal processing blocks from this chapter.

## 4.1 Analog and Digital Building Blocks

Analog and digital signal processing algorithms either process an input x into an output y, such as a lowpass filter, or render an output, such as an oscillator. Analog signal processing, the input and output signals are usually labeled x(t) and y(t) where t is the continuous time variable. Analog algorithms can be described in a block diagram format rather than a circuit. In doing so, the details of the circuit are removed so that you can focus on the details of the algorithm to understand it and figure out different ways of implementing or improving it. The block diagrams use analog building blocks that consist of three components:

- scalar coefficient multipliers
- summers
- integrators

A scalar coefficient multiplier simply multiplies the signal by a value called a coefficient, while a summer adds or subtracts two signals. An integrator performs the mathematical operation of time integration on the signal. Integration is required because analog circuits that include capacitors and inductors can be described mathematically using a differential equation (or set of them). Solving these equations often requires one or more integrations.

In digital signal processing, the input and output signals are labeled x(n) and y(n) or x[n] and y[n] where n is the discrete time variable. Some engineers specifically reserve the bracketed version as x[n] for digital signals and the other x(t) for analog signals, we do not apply this paradigm. Digital algorithms can be described in a block diagram format rather than a flowchart. The block diagrams use digital building blocks that consist of three components:

- scalar coefficient multipliers
- summers
- delay elements

The scalar coefficient multipliers and summers behave the same way as their analog counterparts. A delay element performs the mathematical operation of time delay. Time delay is used to create the digital equivalent of a phase shift in the signal. Digital algorithms often produce block diagrams that add or subtract feed-forward and feedback sub-branches of delayed signals. Figure 4.1 shows the analog and digital building blocks. The input/output relationships are shown. The z⁻¹ represents one delay. The delay is indicated with the (–) sign, the number of samples by. The output is y(n) = x(n−1) where the delay is indicated with the (–) sign and the number of samples by the value after it. As you see in Chapter 1, multiplying a signal by z⁻¹ effectively delays it by one sample interval.

## 4.2 Analog and Digital Transfer Functions

It is convenient to describe the input/output relationship of the signals in analog and digital algorithms in frequency rather rather than the time domain. The resulting equations explain how the algorithm affects the frequency components of the signal rather than the time domain. For analog algorithms, this is done with the Laplace transform, while digital algorithms use the z-Transform. Calling Chapter 1, the Laplace transform converts a signal or function whose dependent variable is t into a function whose dependent variable is s. The s is a complex frequency, which means that it can be described with real and imaginary components indicated as s = σ + ju where ω is in radians/second. The need for a complex number arises from the fact that the Laplace transform's kernel is s¹, which represents a complex sum that may be a steady state signal, an exponentially decaying signal or an exponentially increasing signal, depending on the value of σ in the s-term. The input and output signals x(t) are transformed into X(s) and Y(s), the Laplace spectra of the input and output. The transfer function of an algorithm is its output divided by its input and denoted as H. The time domain of H is h and the impulse response of the system. The impulse response of the system when a impulse is applied at the input. For analog signals, the impulse is infinitely narrow and called the Dirac function. The Laplace transform might look daunting, but you can learn a few rules and use the Laplace transform without doing any calculus. In fact, for this book's projects, you can analyze block diagrams and apply the transform essentially by inspection. The first Laplace transform relationships are to learn easily.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_218_0.png)

Figure 4.1: Analog and digital building blocks.

```
x(t) → X(s)
ax(t) → ax(s)
y(t) → Y(s)
by(t) → bY(s) (4.1)
```

These first rules state that instances of x(t) will become instances of X(s), and likewise y(t) becomes Y(s). The scalar property also translates through the transform so that multiplying by a scalar a or b in time turns into multiplication in the Laplace spectrum. Figure 4.2 shows a simple example block diagram of an amplifier that amplifies the input by a factor of K.

Figure 4.2: The Laplace transform of a simple block diagram.

You can see that the input and output x(t) and y(t) have been transformed into X(s) and Y(s) by inspection. Let's look at how we form the transfer function H(s):

![](img/b42d0dca53f4a889d8162d55f7c8c05d_219_0.png)

Multiplying the input by H(s) yields Y(s). So in the block diagram in Figure 4.2, when an input is applied to a transfer block H(s), the output is simply the input multiplied by the transfer function.

Figure 4.3: The z-Transform of a simple block diagram.

Referring back to Chapter 1, the z-Transform is the discrete version of the Laplace transform, and it converts a signal or function whose dependent variable is t into a function whose dependent variable is s. The s is a complex frequency, which means that it can be described with real and imaginary components indicated as s = σ + ju where ω is in radians/second. The need for a complex number arises from the fact that the Laplace transform's kernel is s¹, which represents a complex sum that may be a steady state signal, an exponentially decaying signal or an exponentially increasing signal, depending on the value of σ in the s-term. The input and output signals x(t) are transformed into X(s) and Y(s), the Laplace spectra of the input and output. The transfer function of an algorithm is its output divided by its input and denoted as H. The time domain of H is h and the impulse response of the system. The impulse response of the system when a impulse is applied at the input. For analog signals, the impulse is infinitely narrow and called the Dirac function. The Laplace transform might look daunting, but you can learn a few rules and use the Laplace transform without doing any calculus. In fact, for this book's projects, you can analyze block diagrams and apply the transform essentially by inspection. The first Laplace transform relationships are to learn easily.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_218_0.png)

Figure 4.1: Analog and digital building blocks.

```
x(t) → X(s)
ax(t) → ax(s)
y(t) → Y(s)
by(t) → bY(s) (4.1)
```

These first rules state that instances of x(t) will become instances of X(s), and likewise y(t) becomes Y(s). The scalar property also translates through the transform so that multiplying by a scalar a or b in time turns into multiplication in the Laplace spectrum. Figure 4.2 shows a simple example block diagram of an amplifier that amplifies the input by a factor of K.

Figure 4.2: The Laplace transform of a simple block diagram.

You can see that the input and output x(t) and y(t) have been transformed into X(s) and Y(s) by inspection. Let's look at how we form the transfer function H(s):

![](img/b42d0dca53f4a889d8162d55f7c8c05d_219_0.png)

Multiplying the input by H(s) yields Y(s). So in the block diagram in Figure 4.2, when an input is applied to a transfer block H(s), the output is simply the input multiplied by the transfer function.

Figure 4.3: The z-Transform of a simple block diagram.

Referring back to Chapter 1, the z-Transform is the discrete version of the Laplace transform, and it converts a signal or function whose dependent variable is t into a function whose dependent variable is s. The s is a complex frequency, which means that it can be described with real and imaginary components indicated as s = σ + ju where ω is in radians/second. The need for a complex number arises from the fact that the Laplace transform's kernel is s¹, which represents a complex sum that may be a steady state signal, an exponentially decaying signal or an exponentially increasing signal, depending on the value of σ in the s-term. The input and output signals x(t) are transformed into X(s) and Y(s), the Laplace spectra of the input and output. The transfer function of an algorithm is its output divided by its input and denoted as H. The time domain of H is h and the impulse response of the system. The impulse response of the system when a impulse is applied at the input. For analog signals, the impulse is infinitely narrow and called the Dirac function. The Laplace transform might look daunting, but you can learn a few rules and use the Laplace transform without doing any calculus. In fact, for this book's projects, you can analyze block diagrams and apply the transform essentially by inspection. The first Laplace transform relationships are to learn easily.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_218_0.png)

Figure 4.1: Analog and digital building blocks.

```
x(t) → X(s)
ax(t) → ax(s)
y(t) → Y(s)
by(t) → bY(s) (4.1)
```

These first rules state that instances of x(t) will become instances of X(s), and likewise y(t) becomes Y(s). The scalar property also translates through the transform so that multiplying by a scalar a or b in time turns into multiplication in the Laplace spectrum. Figure 4.2 shows a simple example block diagram of an amplifier that amplifies the input by a factor of K.

Figure 4.2: The Laplace transform of a simple block diagram.

You can see that the input and output x(t) and y(t) have been transformed into X(s) and Y(s) by inspection. Let's look at how we form the transfer function H(s):

![](img/b42d0dca53f4a889d8162d55f7c8c05d_219_0.png)

Multiplying the input by H(s) yields Y(s). So in the block diagram in Figure 4.2, when an input is applied to a transfer block H(s), the output is simply the input multiplied by the transfer function.

Figure 4.3: The z-Transform of a simple block diagram.

Referring back to Chapter 1, the z-Transform is the discrete version of the Laplace transform, and it converts a signal or function whose dependent variable is t into a function whose dependent variable is s. The s is a complex frequency, which means that it can be described with real and imaginary components indicated as s = σ + ju where ω is in radians/second. The need for a complex number arises from the fact that the Laplace transform's kernel is s¹, which represents a complex sum that may be a steady state signal, an exponentially decaying signal or an exponentially increasing signal, depending on the value of σ in the s-term. The input and output signals x(t) are transformed into X(s) and Y(s), the Laplace spectra of the input and output. The transfer function of an algorithm is its output divided by its input and denoted as H. The time domain of H is h and the impulse response of the system. The impulse response of the system when a impulse is applied at the input. For analog signals, the impulse is infinitely narrow and called the Dirac function. The Laplace transform might look daunting, but you can learn a few rules and use the Laplace transform without doing any calculus. In fact, for this book's projects, you can analyze block diagrams and apply the transform essentially by inspection. The first Laplace transform relationships are to learn easily.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_218_0.png)

Figure 4.1: Analog and digital building blocks.

```
x(t) → X(s)
ax(t) → ax(s)
y(t) → Y(s)
by(t) → bY(s) (4.1)
```

These first rules state that instances of x(t) will become instances of X(s), and likewise y(t) becomes Y(s). The scalar property also translates through the transform so that multiplying by a scalar a or b in time turns into multiplication in the Laplace spectrum. Figure 4.2 shows a simple example block diagram of an amplifier that amplifies the input by a factor of K.

Figure 4.2: The Laplace transform of a simple block diagram.

You can see that the input and output x(t) and y(t) have been transformed into X(s) and Y(s) by inspection. Let's look at how we form the transfer function H(s):

![](img/b42d0dca53f4a889d8162d55f7c8c05d_219_0.png)

Multiplying the input by H(s) yields Y(s). So in the block diagram in Figure 4.2, when an input is applied to a transfer block H(s), the output is simply the input multiplied by the transfer function.

Figure 4.3: The z-Transform of a simple block diagram.

Referring back to Chapter 1, the z-Transform is the discrete version of the Laplace transform, and it converts a signal or function whose dependent variable is t into a function whose dependent variable is s. The s is a complex frequency, which means that it can be described with real and imaginary components indicated as s = σ + ju where ω is in radians/second. The need for a complex number arises from the fact that the Laplace transform's kernel is s¹, which represents a complex sum that may be a steady state signal, an exponentially decaying signal or an exponentially increasing signal, depending on the value of σ in the s-term. The input and output signals x(t) are transformed into X(s) and Y(s), the Laplace spectra of the input and output. The transfer function of an algorithm is its output divided by its input and denoted as H. The time domain of H is h and the impulse response of the system. The impulse response of the system when a impulse is applied at the input. For analog signals, the impulse is infinitely narrow and called the Dirac function. The Laplace transform might look daunting, but you can learn a few rules and use the Laplace transform without doing any calculus. In fact, for this book's projects, you can analyze block diagrams and apply the transform essentially by inspection. The first Laplace transform relationships are to learn easily.

## 4.3 Digital Delay

The scalar multiplication and addition operations are simple operations. Consider the M-sample delay line in Figure 4.4(a). Applying a discrete complex sinusoid $e^{juT}$ (where n is the sample number, and T is the sampling period) produces a M-sample delayed version at the output, $e^{ju(n-M)T}$. Using the polynomial property of $e^{a+b}=e^ae^b$, we can split the output term as:

$e^{junT} = e^{junT}e^{-juMT} \quad (4.4)$

This means we can treat time delay as a mathematical operation of multiplying by $e^{-ju\omegaM}$ where M is the number of samples.

| $e^{junT}$ | Sample Delay |
| :--- | :--- |
| $x(n)$ | $e^{ju(nT-M)}$ |
| $x(n)$ | $z^{-M}-y(n)=x(n-M)$ |

(a) (b)

Figure 4.4: (a) An M-sample delay line with complex sinusoid applied and (b) the digital block diagram. Now we let $z=e^{j\omega}$ and rename the M-sample delay $z^{-M}$ giving the following equation:

$x(n-M) \rightarrow X(z)z^{-M}$
so
$x(n-1) \rightarrow X(z)z^{-1}$
$x(n-2) \rightarrow X(z)z^{-2}$
$Y(n-1) \rightarrow Y(z)z^{-1}$
$\etc... \quad (4.6)$

The last $z$-Transform rule you need to learn (there are only three) has to do with delaying the signal by number of samples M. We already know that this results in multiplication by $z^{-M}$ or $e^{-ju\omegaM}$. In this case:

$y(n)=x(n-M)$
apply $\rightarrow Transform$
$Y(n) \rightarrow Y(z)$
$x(n-M) \rightarrow X(z)z^{-M}$
so
$Y(z)=\frac{Y(z)}{X(z)}$
$H(z)=\frac{Y(z)}{X(z)}=z^{-M} \quad (4.7)$
