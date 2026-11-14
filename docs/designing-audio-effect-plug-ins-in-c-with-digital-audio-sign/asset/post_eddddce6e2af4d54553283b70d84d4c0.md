
![](img/b54974d0a4317ec82d7ae02126d10a6f_349_0.png)

Figure 11.9: Four comb filters in parallel.

This means we can control the reverb time by using the gain factor or the delay length D. The tradeoff is that if we increase g to increase reverb time, the poles get very near the unit circle, causing resonances. If we increase D, then the echoes become distinctly audible rather than smearing together. This means that there is a tradeoff of the modal density versus the echo density in the design. The modal density for a parallel bank of N comb filters in Equation 11.10 is given by Jot (1991). From Equation 11.10 you can see that the modal density remains constant across all frequencies, which is not what happens in real rooms where the modal density increases with the square of the frequency (Equation 11.5).

$$M_d = \sum_{i=0}^{K} D_i T_s$$
where
\(D_i\) = the delay length of the \(i\)th comb filter
\(T_s\) = the sample period
(11.10)

or

$$M_d = N \overline{D} T_s$$
where

\(\overline{D}\) = the mean delay length of all filters averaged

The echo density for the parallel combs with delay lengths close to each other is given in Equation 11.11 (Jot 1991).

$E_d = \sum_{i=1}^N \frac{1}{D_i T_s}$
where
$D_i$ = the delay length of the \(i\)th comb filter
(11.11)

$E_d = \frac{N}{\overline{D} T_s}$
where
\(\overline{D}\) = the mean delay length of all filters averaged

Knowing the desired $M_d$ and $E_d$ you can then calculate the number of parallel comb filters $N$ with average delay time $DT_s$ with Equation 11.12.

$N = \sqrt{E_d M_d} / \overline{D} T_s = \sqrt{M_d / E_d}$
(11.12)

Plugging Schroeder's values of $M_d = 0.15$ eigenfrequencies/Hz and $E_d = 1000$ echoes/sec into Equation 11.12 yields $N = 12$ and the average delay time $DT_s = 12$ mSec.

## 11.4 The Delaying All-Pass Filter Reverberator

Schroeder also proposed the delaying all-pass filter (APF) as a reverberator unit. The impulse response is a decaying set of echoes but the frequency response is technically flat. Schroeder's APF is shown in Figure 11.10. In Figure 11.11, you can see that we get echoes that decay faster than the comb filter and at a different rate. It has a flat magnitude response due to the APF reciprocal zero/pole radii. However, as Gardner points out, our ears only perform a short-time integration, whereas the APF requires an infinite integration time to achieve the flat response, so we will still hear some timbral coloration in this unit.

![](img/b54974d0a4317ec82d7ae02126d10a6f_350_0.png)

Figure 11.10: Schroeder's APF reverberator.

![](img/b54974d0a4317ec82d7ae02126d10a6f_351_0.png)

Figure 11.11: Impulse response of Schroeder's APF reverberator; the frequency response is flat. The delay time was $D = 35$ mSec with $g = 0.6$.

Inspection of the block diagram in Figure 11.10 reveals that this is a rather complex feed-back/feed-forward structure. We need to extract the difference equation so we can synthesize the reverb unit. To start, we label the nodes $c(n)$ and $d(n)$ in the block diagram, then fashion the output $y(n)$ with respect to them:

```
$c(n) = x(n) + gd(n)$
$d(n) = c(n)z^{-D}$
$y(n) = -gx(n) + (1-g^2)d(n)$
(11.13)
```

Now, we expand out the internal nodes and use the familiar time and frequency shifting properties of the $z$ transform to continue Equation 11.14.

```
$d(n) = c(n)z^{-D}$
$= x(n-D) + gd(n-D)$
$y(n) = -gx(n) + (1-g^2)[x(n-D) + gd(n-D)]$
(11.14)
```

Examining the last term in Equation 11.14, $d(n-D)$, we can rearrange Equation 11.13 to continue and get Equation 11.15:

```
$d(n) = \frac{y(n)+gx(n)}{(1-g^2)}$
so
$d(n-D) = \frac{y(n-D)+gx(n-D)}{(1-g^2)}$
(11.15)
```

Substituting Equation 11.15 back into Equation 11.14 you get the difference equation in Equation 11.16:

```
$y(n) = -gx(n) + (1-g^2)\left[x(n-D) + g\left(\frac{y(n-D)+gx(n-D)}{(1-g^2)}\right)\right]$
$= -gx(n) + (1-g^2)x(n-D) + gy(n-D) + g^2x(n-D)$
$= -gx(n) + x(n-D) + gy(n-D)$
(11.16)
```

## 11.5 More Delaying All-Pass Filter Reverberators

There are multiple ways to synthesize the delaying APF. Figure 11.12 shows another one. Deriving the difference equation is easier for this version; we only need to define one extra node, w(n) in Equation 11.17:

```
w(n) = x(n) + gw(n-D)
y(n) = -gw(n) + w(n-D)
   = -g[x(n) + gw(n-D)] + [(x(n-D) + gw(n-2D)]
   = -gx(n) - g^2w(n-D) + x(n-D) + gw(n-2D)
   = -gx(n) + x(n-D) - g^2w(n-D) + gw(n-2D)

grouping:
```

In order to finish, find y(n - D) from the second line in Equation 11.18 and notice that this is the same as the last two terms in Equation 11.17.

```
y(n) = -gw(n) + w(n-D)

y(n-D) = -gw(n-D) + w(n-2D)

and

gy(n-D) = -g^2w(n-D) + gw(n-2D)
```

Thus, the last two terms in Equation 11.17 can be replaced by gy(n-D), and the final difference equation matches Schroeder's APF:

```
y(n) = -gx(n) + x(n-D) + gy(n-D)
```

Figure 11.13 shows another version of the same APF. The proof that it has the same difference equation is easy if you look at the node w(n) in Equation 11.20:

```
w(n) = x(n) + gw(n-D)
y(n) = -gw(n) + w(n-D)
```

![](img/b54974d0a4317ec82d7ae02126d10a6f_352_0.png)

Figure 11.12: Another version of the delaying all-pass reverberator.

These are the first two lines in the derivation for the delaying APF above. Figure 11.14 shows yet another structure. To figure this one out, once again find the internal node w(n) as it relates to the output in Equation 11.21:

```
w(n) = x(n) + gy(n)
y(n) = -gx(n) + w(n-D)

then

w(n-D) = x(n-D) + gy(n-D)

and

y(n) = -gx(n) + x(n-D) + gy(n-D)
```

Equation 11.21 is identical to Equation 11.20, but care must be taken in the synthesis of this in code—you must form the internal nodes first to avoid a zero-delay loop (the x(n) + gw(n) term above). Inverted APFs simply swap signs on the g coefficients. This has the effect of inverting the impulse response while keeping the frequency response theoretically flat. By combining both inverting and regular delaying APFs, you can try to achieve a more uncorrelated echo density.

![](img/b54974d0a4317ec82d7ae02126d10a6f_353_0.png)

Figure 11.13: Alternate version of the delaying APF; the transfer function and difference equations are identical to the other structures.

![](img/b54974d0a4317ec82d7ae02126d10a6f_353_1.png)

Figure 11.14: Another delaying APF structure.

## 11.6 Schroeder's Reverberator

Schroeder combined a parallel comb filter bank with two APFs to create his first design. The comb filters produce the long series of echoes and the APFs multiply the echoes, overlaying their own decaying impulse response on top of each comb echo. The resulting reverberation unit, shown in Figure 11.15, sounds marginal but it is very simple to implement.

Schroeder suggests that the ratio of smallest to largest delay in the comb filters should be about 1:1.5 and originally specified a range of 30–45 mSec in total. The 1:1.5 ratio rule turns out to be useful for just about any set of parallel comb filters.

The comb filters should have the following properties:

- Choose the delays to have the 1:1.5 ratio above.
- Choose delay times that have no common factors (e.g., 2191, 2971, 3253, 3307).
- Set the gain values according to Equation 11.9.

![](img/b54974d0a4317ec82d7ae02126d10a6f_354_0.png)

Figure 11.15: Schroeder's original reverb design.

The APFs should have the following properties:

- Choose delays that are much shorter than the comb filters, 1 mSec to 5 mSec.
- Set both gain values the same, between 0.5 and 0.707.

## 11.7 The Low-Pass Filter–Comb Reverberator

One of the things missing from the original Schroeder reverb is the fact that in a real room, high frequencies decay much more rapidly than low frequencies, as shown in the EDRs of Figure 11.6 (Moorer 1979). Placing a low-pass filter (LPF) in the comb filter's feedback path will roll off the high-frequency content of successive echoes exponentially, which is what we want. The LPF–comb reverberator block diagram is shown in Figure 11.16.

The LPF is chosen to be a one-pole feedback type (infinite impulse response [IIR]) so that it will introduce not only low-pass filtering, but also its own impulse response into the echoes going through the feedback path. In Figure 11.17 the LPF is shown in the dotted box; notice that it is turned around backward to follow the flow of the feedback path.

To find the difference equation, it is easier to start in the frequency domain with the z transforms of the comb and first-order feed-forward filter, since we are already familiar with them by now (Equation 11.22).
