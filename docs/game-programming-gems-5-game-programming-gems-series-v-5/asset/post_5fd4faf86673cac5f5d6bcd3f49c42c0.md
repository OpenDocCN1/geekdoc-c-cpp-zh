
Then in step 1b, we linearly interpolate between the two samples neighboring the read cursor. We also change the code to do the regular advance of the read cursor in the midst of the linear interpolation (so step 7 is left as the advance of the write cursor only):

```
// step 1b: linearly interpolate between the
// samples next to the read cursor, and advance integer cursor here
float r[4];
r[0] = line[0][ read[0] ];
// etc ...
read[0] = ( read[0] + 1 ) & mask[0];
r[0] += p[0] * ( line[0][ read[0] ] - r[0] );
// etc ...
```

What is not shown here is the code that slowly modulates the sweeping velocities, which is a simple sine table lookup or other modulation waveform, and can be done sparsely, like every 16–64 samples.

Let's fight the blurring. Linear interpolation is in effect a first-order finite impulse response filter, which may be cancelled with a first-order infinite impulse response filter, just like the one that is already in place in our feedback loops. We want to calculate which adjustment must be made to the filter alphas \(\alpha_i\) to compensate the blurring.

The transfer function of linear interpolation would be written as follows:

```
\(y_k = (1-p)x_k + p x_{k+1},\)
\(H(z) = \frac{y_k}{x_k} = 1 - p + pz.\)
```

Here, \(p\) is the current partial position of a read cursor. If \(p = 0\), we are sampling integer positions and no blurring is introduced, while with \(p = 1/2\), the blurring is at maximum. Let's assume that \(p\) is moving so fast that we get the net effect of a random \(p\). For this case, we can calculate the integral of the absolute value \(|H(z)|\) and come up with

```
\(\int_0^1 |1 - p + pz| \, dp = \int_0^1 \sqrt{Yp^2 - \gamma p + 1} \, dp, \text{ with } \gamma = 2 - 2\cos(2\pi f / f_s).\)
```

The interesting result is at the upper end of the spectrum, at \(f=f_n\) where the integral simply evaluates to 1/2. Therefore, we could try and adjust all our filter alphas as to increase by a factor of 2, and have a compensation for average blurring.

But not so fast here; this works as long as \(p\) is in effect random, but when it is not, the system may eventually blow up. Imagine a partial read cursor being stationary at or close to zero for long enough; the high frequencies would be amplified into infinity. In practice, the compensation factor must be less than 2 and needs to take into account the sweeping velocity $dp$, where the full compensation only kicks in if $dp$ is sufficiently high. To achieve this, the example program on the CD-ROM uses a smooth saturation curve, which saturates at 1.7 and falls with $dp^2$ if $dp$ is below $10^{-5}$. Specifically, the program calculates:

```
$$\beta'_i = \beta_i \left( 1 + \frac{0.7 dp^2}{10^{-9} + dp^2} \right),$$
```

and recalculates the filter alphas $\beta_i$ from $\beta i'$ every time $dp$ changes.

## Conclusion and Possible Improvements

So far, the general concept of FDN reverberation has been introduced, and the most important parameters—feedback matrices, delay lengths and reverberation times—have been discussed. More infrastructure would be needed to get the sound to the FDN and from the FDN to the listener. An example of how this can be done is shown in the example program, which is included on the CD-ROM. This program lets you play stereo wave files through the discussed four-channel FDN and experiment with different reverberation settings. To give you a quick start, the CD-ROM also includes two sample wave files, which are dry (unreverberated) excerpts of a game music remix.

In a 3D setting, it would be possible to associate the channels of a four-channel FDN with the front, left, right, and back directions of the listener’s space. Then, incoming sounds would be distributed to the delay lines according to their relative directions. The aim of this setting is to produce *gradual decorrelation*, where the late reverb comes equally from all directions while the early reflections are coupled to the sound source position.

Multiple rooms with different parameters would need to be simulated with multiple FDNs, and the results weighted. A transition of parameters of a single FDN generally does not produce meaningful results but can nevertheless be used for interesting special effects.

## Acknowledgments

Special thanks go to Pex “Mahoney” Tufvesson for providing the wave files included on the CD-ROM. Thanks to Peter Ohlmann for tips about the gritty details of MFC.

## References

- [FMOD] “fmod” music and effects sound system. Available online at http://www.fmod.org/.
- [Frenette00] Frenette, Jasmin. “Reducing Artificial Reverberation Algorithm Requirements using Time-Variant Feedback Delay Networks.” Masters Thesis. University of Miami, December 2000.
- [Geron76] Gerzon M. A. “Unitary (energy preserving) multichannel networks with feedback.” In Electronic Letters, vol. 12, no. 11, pp. 278–279, 1976.
- [Jo91] Jo, Jean Marc and Antoine Chaigne. “Digital delay networks for designing artificial reverberators.” In Proc. 90th Conv. Audio Eng. Soc., Feb. 1991, preprint 3030.
- [Jot93] Jot, Jean Marc and Antoine Chaigne. “Method and system for artificial spatialisation of digital audio signals.” United States Patent 5,491,754., Feb 1993.
- [Mathworld] Erich Weisstein’s world of mathematics. Available online at http://www.mathworld.com.
- [MSDN] Microsoft Developer Network. Available online at http://msdn.microsoft.com/default.aspx.
- [Moorer79] Moorer, J. A. “About this reverberation business.” In Computer Music Journal, vol. 3, no. 2, 1979.
- [Schroeder62] Schroeder, J. M. “Natural sounding artificial reverberation.” J Audio Eng Soc, vol. 10, no. 3, 1962.
- [Smith96] Smith, Julius O. and Davide Rocchesso. “Circulant and Elliptic Feedback Delay Networks for Artificial Reverberation.” In IEEE Transactions on Speech and Audio, vol. 5, no. 1, pp. 51–60, Jan. 1996.
- [SmithOnline] Smith, Julius O. “Physical Audio Signal Processing: Digital Waveguide Modeling of Musical Instruments and Audio Effects.” Available online at http://www-ccrma.stanford.edu/~jos/waveguide/wasp.html.
- [Stautner82] Stautner, John and Miller Puckette. “Designing Multi-Channel Reverberators.” In Computer Music Journal, vol. 6, no. 1, pp. 52–65, Spring 1982.
- [Valimaki00] Valimäki, V. and T. I. Laakso. “Principles of Fractional Delay Filters.” IEEE Int. Conf. on Acoustics, Speech and Signal Processing, June 2000.

## 7.5

## Introduction to Single-Speaker Speech Recognition

Julien Hamaide

julien_hamaide@hotmail.com

In the past years, much effort has been made in the fields of 3D and artificial intelligence but not in the area of human-computer interfaces. In a majority of games, our interactions are still limited to traditional peripherals: keyboard, mouse, joystick, or joypad. This gem presents a technique that will introduce a new dimension to these interfaces: the voice. With the recent apparition of recording systems on consoles, this new type of interaction makes sense. Moreover, it can be the basis for a new type of gameplay.

This gem introduces a single-locutor recognition technique based on examples. This technique is easy to implement, does not ask for much processing power, and is easily integrated in existing software. It does not try to understand the meaning of entire sentences, but rather tries to recognize isolated words. Demo software is provided on the CD-ROM, so you may evaluate the system.

![](img/672fe9a2d008ba627b1991e15d70f43e_790_0.png)

### Introduction

Speech is a pretty complex signal. Its human origin, made of imprecision, makes it difficult to analyze. In this section, the structure of a speech signal will be briefly introduced. In addition, the acoustic properties that make its recognition more difficult will be pointed out.

Voice is a signal produced by our body and our brain. The latter corrects it and adapts it continuously, thanks to the feedback received through the ears. The production of voice results from the circulation of the air through the vocal cords of the larynx. As the air passes through the vocal cords, it makes them vibrate, which results in the production of sounds.

A speech production model can be seen in Figure 7.5.1.
