![](bbox=[0.19825, 0.03125, 0.80175, 0.13785])

**Figure 1.23:** An improperly bandlimited signal's spectral replicas overlap, this overlap produces aliasing.

![](bbox=[0.17625, 0.19925, 0.82375, 0.30125])

**Figure 1.24:** (a) A quasi bandlimited waveform and (b) its spectrum.

So far, this aliasing has been caused by improper band limiting on the input signal. But we are designing synthesizers and have no input so why should we choose? The answer is that we are completely able to mathematically create waveforms. In our world, we create waveforms that could never have made it past the inputpass filter in a normal digital system with both input and output. One of the oscillators we design is a quasi bandlimited oscillator. The idea is that we will allow a bit of aliasing as long as the aliased frequency components are far away from the fundamental and in limit. Figure 1.24 shows the time domain response and spectrum of a quasi bandlimited waveform. If you examine Figure 1.20(a–b) in the bandlimited wavelet, you can see that, although the time domain points are indistinguishable, the frequency domain tells a different story. In this particular case the fundamental is 440 Hz, and we see the last aliased component -60 db about 10 kHz.

In the preceding sections, we barely scratched the surface of DSP theory, as a complete treatise on the subject is outside the scope of the book and covered in scores of other texts. This book has been designed to minimize the math required to understand the operation of the functional components in our synths, and when we get into Virtual Analog (VA) filters, you will find the math to be refreshingly simple—there is no calculus involved!

# ## Bibliography

Moore, Richard. 1990. Elements of Computer Music, Chap. 3. Eagle Cliffs: Cambridge: Prentice-Hale.

Roads, Courts. 1996. The Computer Music Tutorial, Chap. 2. Cambridge: The MIT Press.

Sound on Sound Magazine. "Synth Secrets." Accessed June 2014

synthmuseum.com. "Taddeus Cail's Teleharmonium." Accessed June 2014,
http://www.synthmuseum.com/magazine/0102jw.html

# ## Very Approachable DSP Books

Ifeacher, Emmanuel C. and Jervis, Barrie W. 1993. Digital Signal Processing, A Practical Approach . Menlo Park: Addison Wesley.