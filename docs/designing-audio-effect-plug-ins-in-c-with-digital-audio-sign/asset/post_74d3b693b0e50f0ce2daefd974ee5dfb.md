
![](img/b54974d0a4317ec82d7ae02126d10a6f_250_0.png)

Figure 8.10: The frequency response for the resonant LPF test filter.

![](img/b54974d0a4317ec82d7ae02126d10a6f_250_1.png)

Figure 8.11: The ringing IR of the resonant LPF.

## 8.2.3 The IR File Format

The IR file actually contains C++ code and you can quickly understand how it works by using the clipboard functions. In the analyzer window that you still have pulled up, click on the button h(n) → Clipboard and after the success message, open a text editor or a C++ compiler. Then, use the operating system (OS) paste function to paste the clipboard data into your editor. You will see something like this at the top:

```
// h(n) Impulse Response
// Length= 1024
m_nIRLength= 1024;
m_h_Left[0] = 0.00000000;
m_h_Left[1] = 0.00503618;
m_h_Left[2] = 0.01998402;
m_h_Left[3] = 0.03938961;
m_h_Left[4] = 0.05777339;
m_h_Left[5] = 0.07477701;
m_h_Left[6] = 0.09007415;
m_h_Left[7] = 0.10337673;
etc...
```

This is the IR data starting with the length (1024) and then the left and right channels respectively. If you scroll to the bottom, you will see the last few samples of the IR:

```
m_h_Right[1016] = -0.00000850;
m_h_Right[1017] = 0.00004104;
m_h_Right[1018] = 0.00008918;
m_h_Right[1019] = 0.00013495;
m_h_Right[1020] = 0.00017745;
m_h_Right[1021] = 0.00021589;
m_h_Right[1022] = 0.00024953;
m_h_Right[1023] = 0.00027775;
```

This was my resonant LPF and you can see that it is still ringing, even after 1024 samples. If you listen to a wave file through a filter like this, you can hear pinging sounds at the peak resonant frequency. These pinging noises are the ringing of the filter. If you look at the C++ code you can tell that the IR data appears to be some kind of member variable information for a C++ object because of the “m_” Hungarian notation used to describe the data.

> All RackAFX plug-ins already have two default IR arrays declared as m_h_Left[1024] and m_h_Right[1024] and another variable m_nIRLength that defines how much of the 1024 point IR buffer is being used. The FIR designer will let you create IRs with variable sizes–in many cases, you don’t need all 1024 points to describe the IR of the system. You tell RackAFX that you want it to populate your IR arrays by setting a flag m_bWantIRs in your plug-in constructor. When a user loads or creates an IR in the analyzer, it is automatically delivered to your plug-in.

## 8.3 Using RackAFX's FIR Designer

RackAFX has a powerful built-in module called FIR Designer that lets you use two popular methods to design FIR filters: the optimal method and the frequency sampling method. The optimal method is sometimes called the “Parks–McClellan algorithm.” When the module first opens, you will see the new controls at the right side, as shown in Figure 8.12.

This module creates IRs. You can save the IRs to a file or the clipboard using the same buttons as before. If your plug-in has the m_bWantIRs flag set, any time the user hits the Calculate button to make a new IR, it will automatically be delivered and copied into the plug-in’s default IR arrays. Even though the FIR Designer defaults to the optimal method for design, let’s begin with the frequency sampling method since the optimal method relies on it.

![](img/b54974d0a4317ec82d7ae02126d10a6f_252_0.png)

Figure 8.12: The FIR designer controls consist of three parts. The order slider and edit box and the Calculate and Complement buttons are shared between both methods. You enable the method of choice using the radio button controls.

## 8.4 The Frequency Sampling Method

The frequency sampling method is really interesting because it lets you design any kind of frequency response you want—it can be any arbitrary shape and it does not have to be a classical filter type (LPF, high-pass filter [HPF], band-pass filter [BPF], band-stop filter [BSF]), but you can make these types if you want to. The frequency sampling method involves these steps:

- 1. Decide on a desired frequency response and plot it in the frequency domain.
- 2. Sample the frequency response at evenly spaced intervals determined by the filter order you choose.
- 3. Take the inverse discrete cosine-transform (DCT) of the sampled frequency response to get the sampled IR (the DCT is simply the real part of the fast Fourier transform [FFT]).
- 4. Load the sampled IR into a convolver and go.

## 8.4.1 Linear-Phase FIR Using the Frequency Sampling Method

Choose:

N = number of coefficients

Calculate:

For N = odd:

- (N + 1)/2 = number of samples in frequency domain, starting at 0 Hz

For N = even

- N/2 = number of samples in frequency domain, starting at 0 Hz Δf = fs/N = frequency spacing, starting at 0 Hz

Calculate the filter coefficients $a_0$ to $a_{N/2}$ with Equation 8.5:

```
For $N =$ odd
$$a_n = \frac{1}{N} \left[ H(0) + 2 \sum_{i=1}^{(N-1)/2} |H(i)| \cos \left[ 2\pi i \left[ n - \frac{N-1}{2} \right] / N \right] \right]$$

For $N =$ even
$$a_n = \frac{1}{N} \left[ H(0) + 2 \sum_{i=1}^{N/2-1} |H(i)| \cos \left[ 2\pi i \left[ n - \frac{N-1}{2} \right] / N \right] \right]$$
```

Note: This produces half the coefficients; the other half are a mirror image, as shown in the example below. Because the IR is guaranteed to be symmetrical about its center, it produces a linear phase FIR filter every time.

Example: Design an LPF with a cutoff of 5.5 kHz, $f_s = 44.1$ kHz, $N = 16$.

### Solution:

- 1. $N = 16$, which produces eight sampled points in the frequency domain with a spacing of 2.756 kHz.
- 2. Sample the plot, producing the magnitude response, $H(i)$ (Figure 8.13).

For this plot notice that:

- The plot is linear in frequency. To design a frequency sampling method filter by hand, it is often easier to start with a linear frequency axis.
- The point at Nyquist is not used; it is there to pin down the response that would occur after Nyquist.

The sampled frequency response is read directly off the plot: (0 dB = 1.0, -60 dB = 0.001).

```
$|H(i)| = \{ 1.0, 1.0, 1.0, 0.001, 0.001, 0.001, 0.001, 0.001 \}$
```

- 1. Use Equation 8.5 to extract IR $h(n)$, which are the coefficients, $a_n$.

- $a_0 = 0.04858366$
- $a_1 = 0.00364087$
- $a_2 = -0.05199205$
- $a_3 = -0.07047625$
- $a_4 = -0.02194221$
- $a_5 = 0.08695625$
- $a_6 = 0.21101949$
- $a_7 = 0.29421023$
- $a_8 = 0.29421023$
- $a_9 = 0.21101949$
- $a_{10} = 0.08695625$
- $a_{11} = -0.02194221$
- $a_{12} = -0.07047625$
- $a_{13} = -0.05199205$
- $a_{14} = 0.00364087$
- $a_{15} = 0.04858366$

Notice the symmetry about $a_7$ to $a_8$ boundary.

- 2. Measure the response (Figure 8.14).

The resulting filter is guaranteed to exactly match the desired frequency response at the sampled points only. In between the sampled points, the frequency response can do anything; rippling in the pass band and stop band can occur as shown here. You can see that this is a pretty bad rendition of our desired response.

![](img/b54974d0a4317ec82d7ae02126d10a6f_254_0.png)

Figure 8.13: Here is our prototype LPF with cut-off at 5.5 kHz; its response becomes –60 dB (0.001) at 8.2 kHz, which is a steep roll-off.

The first lobe in the stop band only produces about –14 dB of attenuation, which is poor considering that we wanted a filter that would have a stop-band attenuation of –60 dB. To improve the response, you have several choices:

- Relax the specifications.
- Add more points to the desired response.
- Increase the filter order.

Relax the specifications and roll off the response less steeply by changing the point at 8.2 kHz to –12 dB (0.25) instead of –60 dB (Figure 8.15). Now, the sampled frequency response is

```
|H(i)| = {1.0, 1.0, 1.0, 0.25, 0.0, 0.0, 0.0, 0.0, 0.0}
```

The resulting magnitude response |H(f)| is shown in Figure 8.16.

![](img/b54974d0a4317ec82d7ae02126d10a6f_255_0.png)

Figure 8.14: The resulting low-pass filter magnitude response.

![](img/b54974d0a4317ec82d7ae02126d10a6f_255_1.png)

Figure 8.15: The same design with specifications relaxed; the slope is less steep.

![](img/b54974d0a4317ec82d7ae02126d10a6f_255_2.png)

Figure 8.16: The relaxed magnitude response shows improved stop-band attenuation. Now, the first lobe in the stop band has moved to a magnitude of about –30 dB, an improvement of about 15 dB.

## 8.5 Complementary Filter Design for Linear Phase FIR Filters

This technique results in a complementary filter, rotated about the center of the Nyquist bandwidth, that is, rotated about Nyquist/2. To convert an LPF to HPF or vice versa on a linear phase FIR:

For N = even

- Multiply the even-numbered coefficients by -1.

For N = odd

- Multiply the odd-numbered coefficients by -1.

This will rotate the frequency response around Nyquist/2 such that an LPF will become an HPF.
