implement u by observing that 1/1 + KG is a scalar value, so the input will be the difference of x and KΣ multiplied by 1/1 + KG, where Σ is the sum of S's.

In Figure 7.44 we have labeled the nodes G4, G3 and G2 in each filter stage. These contribute to the global feedback path around the entire structure eventually summed by the loop gain. The a0 coefficients in each block represent the attenuators of 0.5 for the last three LPFs, and it is set to 1.0 for the first LPF as in Figure 7.24. Figure 7.45 shows the frequency response for the filter with various values for $f_C$ with K=16 and no NLP.

Figure 7.44: The complete diode ladder filter diagram.

Figure 7.45: The filter's response is consistent across the spectrum; here K=16 and $f_c$ is 100 Hz, 500 Hz, 1 kHz, 2.5 kHz, 5 kHz, 10 kHz and 20,480 Hz.

# 7.12 Designing the Filter Objects

It's time to design our C++ objects that will handle the filtering duties of our synth projects. We are going to design a separate C++ object for each of the five categories of filters in the chapter. This will result in a total of 15 filters to choose from in your own projects.

+   - CVAOnePoleFilter: the first order VA LPF and HPF
- CSEMFilter: the Oberheim SEM LPF, HPF, BPF and variable BSF
- CKThreeFiveFilter: the Korg35 second order LPF and HPF

![](bbox=[0.318, 0.046, 0.881, 0.966])