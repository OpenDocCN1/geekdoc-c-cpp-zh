$E_d = \sum_{i=n}^N \frac{1}{D_i T_s}$
where
$D_i$ = the delay length of the $i$th comb filter
(11.11)

$E_d = \frac{N}{\overline{D} T_s}$
where
\(\overline{D}\) = the mean delay length of all filters averaged

Knowing the desired $M_d$ and $E_d$ you can then calculate the number of parallel comb filters $N$ with average delay time $DT_s$ with Equation 11.12.

$N = \sqrt{E_d M_d} / \overline{D T_s} = \sqrt{M_d / E_d}$
(11.12)

Plugging Schroeder's values of $M_d = 0.15$ eigenfrequencies/Hz and $E_d = 1000$ echoes/sec into Equation 11.12 yields $N = 12$ and the average delay time $DT_s = 12$ mSec.

# 11.4 The Delaying All-Pass Filter Reverberator

Schroeder also proposed the delaying all-pass filter (APF) as a reverberator unit. The impulse response is a decaying set of echoes but the frequency response is technically flat. Schroeder's APF is shown in Figure 11.10. In Figure 11.11, you can see that we get echoes that decay faster than the comb filter and at a different rate. It has a flat magnitude response due to the APF reciprocal zero/pole radii. However, as Gardner points out, our ears only perform a short-time integration, whereas the APF requires an infinite integration time to achieve the flat response, so we will still hear some timbral coloration in this unit.

![](bbox=[0.22, 0.63, 0.78, 0.82])

Figure 11.10: Schroeder's APF reverberator.