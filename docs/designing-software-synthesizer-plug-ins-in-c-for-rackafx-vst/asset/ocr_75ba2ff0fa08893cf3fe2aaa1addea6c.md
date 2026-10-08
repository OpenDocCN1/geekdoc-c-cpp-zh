$n_1 \quad n_2 \qquad (12.14)$

Or:

$f_c = 100\text{ Hz}\nf_m = 133.333\text{ Hz}\n\frac{N_1}{N_2} = \frac{3}{4}\n\nf_a = \frac{f_c}{N_1} = \frac{f_m}{N_2} = 33.333\text{ Hz} \qquad (12.15)$

Notice in this second example that the resultant frequency is neither the carrier nor the modulator frequency!

# Rule Two: Spectral Purity

The value of $N_2$ affects the purity of the spectrum (whether it contains harmonics or has gaps in the spectrum):

$N_1 = 1 \qquad \text{spectrum contains all harmonic multiples}\nN_2 \ge 2 \qquad \text{spectrum is missing } N_2\text{th harmonic} \qquad (12.16)$

# Rule Three: Reflected Frequencies

The value of $N_2$ also gives the negative frequency components are reflected across the 0 Hz axis:

# Rule Four: Inharmonicity

The value of the $N_1/N_2$ ratio predicts the inharmonicity.

$N_1 = 1 \text{ or } N_2 = 2 \qquad \text{all-(harmonics) line up perfectly with } +\text{harmonics}\nN_2 > 2 \qquad \text{none of the } (-)\text{harmonics} line up with any } +\text{harmonics} \qquad (12.17)$

When the ratio is non-integer based (and especially irrational), the sound is inharmonic—there is technically no fundamental. However, this makes fantastic bell/gong percussion sounds, which are difficult to synthesize with subtractive synthesis. The sounds are such that many FM synth patches automatically include them as a matter of practice.
$N_1 \ge 5 \qquad f_0 \text{ is low in amplitude; difficult to pitch, somewhat inharmonic}\nN_1, N_2 \text{: integers} \qquad f_0 \text{ does not exist; completely inharmonic} \qquad (12.18)$

# 12.4 Dynamic Spectra

In previous years, we used dynamic filtering to shape the timbre in time: we used EGs and LFOs to shift the filter cutoff frequency during the note events. For the vector synthesizers, crossing between sounds with different timbres adds even more sonic. In FM synthesis, the index of modulation ultimately controls the bandwidth of the output. If you use this index, it will vary the bandwidth of the spectrum and can be seen to do much like filter sweeps without the filter. The idea is to place an envelope generator on the output of each oscillator. For the carrier, this EG affects the domain envelope in a way we used an EG to control the DCA. For the modulator, the EG controls to the depth of modulation of its carrier oscillator. For our PM synth, this means that it controls the phase deviation. By varying the deviation in time, we vary the spectrum. Figure 12.9 shows the simple FM synth with the adding of EGs—one oscillator.

In Figure 12.9, notice that the structures inside the dotted line boxes are identical; the only difference is naming the oscillators (Carrier or Modulator). Note also that the EGs control the output amplifiers within the oscillators themselves