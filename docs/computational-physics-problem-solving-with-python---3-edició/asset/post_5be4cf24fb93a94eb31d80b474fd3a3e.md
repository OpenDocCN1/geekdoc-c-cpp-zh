
Explicit energy E at temperature T:

$$
P(E_i, T) = \frac{g(E_i) e^{-E_i/k_B T}}{Z(T)}, \quad Z(T) = \sum_{E_i} g(E_i) e^{-E_i/k_B T}. \tag{17.20}
$$

Here k_B is Boltzmann’s constant, T is the temperature, g(E_i) is the number of states of energy E_i (i = 1, ..., M), Z(T) is the partition function, and the sum is still over all M states of the system, but now with states of the same energy entering just once owing to g(E_i) accounting for their degeneracy. Because we again apply the theory to the Ising model with its discrete spin states, the energy assumes only discrete values. If the physical system had an energy that varied continuously, then the number of states in the interval E → E + dE would be given by g(E) dE and g(E) would be called the density of states. As a matter of convenience, we call g(E_i) the density of states even when dealing with discrete systems, although the term “degeneracy factor” may be more precise.

Even as the Metropolis algorithm has been providing excellent service for more than 60 years, recent literature shows increasing use of Wang–Landau sampling (WLS)² (Landau and Wang, 2001; STP, 2011). Because WLS determines the density of states and the associated partition function, it is not a direct substitute for the Metropolis algorithm and its simulation of thermal fluctuations. However, we will see that WLS provides an equivalent simulation for the Ising model.

The advantage of WLS is that it requires much shorter simulation times than the Metropolis algorithm and provides a direct determination of g(E_i). For these reasons, it has shown itself to be particularly useful for first-order phase transitions where systems spend long times trapped in metastable states, as well as in areas as diverse as spin systems, fluids, liquid crystals, polymers, and proteins. The time required for a simulation becomes crucial when large systems are modeled. Even a spin lattice as small as 8 × 8 has 2⁶⁴ ≃ 1.84 × 10¹⁹ configurations, which makes visiting them all too expensive.

In our discussion of the Ising model, we ignored the partition function when applying the Metropolis algorithm. Now we focus on the partition function Z(T) and the density-of-states function g(E). Because g(E) is a function of energy but not temperature, once it has been deduced, Z(T) and all thermodynamic quantities can be calculated from it without having to repeat the simulation for each temperature. For example, the internal energy and the entropy are calculated directly as

$$
U(T) \equiv \langle E \rangle = \frac{\sum_{E_i} E_i g(E_i) e^{-E_i/k_B T}}{\sum_{E_i} g(E_i) e^{-E_i/k_B T}}. \tag{17.21}
$$

$$
S = k_B \ln g(E_i). \tag{17.22}
$$

The density of states g(E_i) will be determined by taking the equivalent of a random walk in energy space. We flip a randomly chosen spin, record the energy of the new configuration, and then keep flipping more spins to change the energy. The table H(E_i) of the number of times each energy E_i is attained is called the energy histogram (Figure 17.5b). If the walk were continued for a very long time, the histogram H(E_i) would converge to the density of states g(E_i). Yet with 10¹⁹–10³⁰ steps required even for small systems, this direct approach is unrealistically inefficient because the walk would rarely ever get away from the most probable energies.

![](img/bccda43674e4a93dee81c749eba8d2f7_445_0.png)
![](img/bccda43674e4a93dee81c749eba8d2f7_445_1.png)

**Figure 17.5.** Wang–Landau sampling used in the 2D Ising model on an 8 × 8 lattice. (a) Logarithm of the density of states log g(E) ∝ S vs. the energy per particle. (b) The histogram H(E) showing the number of states visited as a function of the energy per particle. The aim of WLS is to make this function flat.

Clever idea number 1 behind the Wang–Landau algorithm is to explore more of the energy space by increasing the likelihood of walking into less probable configurations. This is carried out by increasing the acceptance of less likely configurations while simultaneously decreasing the acceptance of more likely ones. In other words, we want to accept more states for which the density g(E_i) is small and reject more states for which g(E_i) is large (fret not these words, the equations are simple). To accomplish this trick, we accept a new energy E_i with a probability inversely proportional to the (initially unknown) density of states,

$$
\mathcal{P}(E_i) = \frac{1}{g(E_i)}. \tag{17.23}
$$

and then build up a histogram of visited states via a random walk.

The problem with clever idea number 1 is that g(E_i) is unknown. WLS’s clever idea 2 is to determine the unknown g(E_i) simultaneously with the construction of the random walk. This is accomplished by improving the value of g(E_i) via the multiplication g(E_i) → f g(E_i), where f > 1 is an empirical factor. When this works, the resulting histogram H(E_i) becomes “flatter” because making the small g(E_i) values larger makes it more likely to reach states with small g(E_i) values. As the histogram gets flatter, we keep decreasing the multiplicative factor f until it is satisfactorily close to 1. At that point, we have a flat histogram and a determination of g(E_i).

At this point you may be asking yourself, “Why does a flat histogram mean that we have determined g(E_i)?” Flat means that all energies are visited equally, in contrast to the peaked histogram that would be obtained normally without the 1/g(E_i) weighting factor. Thus, if by including this weighting factor we produce a flat histogram, then we have perfectly counteracted the actual peaking in g(E_i), which means that we have arrived at the correct g(E_i).

## 17.6 Wang–Landau Algorithm

The steps in WLS are similar to those in the Metropolis algorithm, but now with the use of the density-of-states function g(E_i) rather than a Boltzmann factor:

1. Start with an arbitrary spin configuration α_k = {s_1, s_2, …, s_N} and with arbitrary values for the density of states g(E_i) = 1, i = 1, …, M, where M = 2^N is the number of states of the system.
2. Generate a trial configuration α_{k+1} by
   a. picking a particle i randomly and
   b. flipping i’s spin.
3. Calculate the energy E_{α_tr} of the trial configuration.
4. If g(E_{α_tr}) ≤ g(E_{α_k}), accept the trial, that is, set α_{k+1} = α_tr.
5. If g(E_{α_tr}) > g(E_{α_k}), accept the trial with probability P = g(E_{α_k})/g(E_{α_tr}):
   a. choose a uniform random number 0 ≤ r_i ≤ 1;
   b. set α_{k+1} = α_tr if P ≥ r_i (accept), and α_{k+1} = α_k if P < r_i (reject).

This acceptance rule can be expressed succinctly as

$$
\mathcal{P}(E_{\alpha_k} \to E_{\alpha_{tr}}) = \min\left[1, \frac{g(E_{\alpha_k})}{g(E_{\alpha_{tr}})}\right], \tag{17.24}
$$

which manifestly always accepts low-density (improbable) states.

6. Once we have a new state, we modify the current density of states g(E_i) via the multiplicative factor f:

$$
g(E_{\alpha_{k+1}}) \to f g(E_{\alpha_{k+1}}), \tag{17.25}
$$

and add 1 to the bin in the histogram corresponding to the new energy:

$$
H(E_{\alpha_{k+1}}) \to H(E_{\alpha_{k+1}}) + 1. \tag{17.26}
$$

7. The value of the multiplier f is empirical. We start with Euler’s number f = e = 2.71828, which appears to strike a good balance between very large numbers of small steps (small f) and too rapid a set of jumps through energy space (large f). Because the entropy S = k_B ln g(E_i) → k_B[ln g(E_i) + ln f], (17.25) corresponds to a uniform increase by k_B in entropy.
8. Even with reasonable values for f, the repeated multiplications in (17.25) lead to exponential growth in the magnitude of g. This may cause floating-point overflows and a consequent loss of information (in the end, the magnitude

   In either case, it is good practice to normalize g(E_i) with one condition and then use the other as a check.

### 17.6.1 WLS Ising Model Implementation

We assume an Ising model with spin–spin interactions between nearest neighbors located in an L × L lattice (Figure 17.6). To keep the notation simple, we set J = 1 so that

$$
E = -\sum_{i \leftrightarrow j}^N \sigma_i \sigma_j, \tag{17.32}
$$

where ↔ indicates nearest neighbors. Rather than recalculate the energy each time a spin is flipped, only the difference in energy is computed. For example, for eight spins in a 1D array,

$$
-E_k = \sigma_0 \sigma_1 + \sigma_1 \sigma_2 + \sigma_2 \sigma_3 + \sigma_3 \sigma_4 + \sigma_4 \sigma_5 + \sigma_5 \sigma_6 + \sigma_6 \sigma_7 + \sigma_7 \sigma_0, \tag{17.33}
$$

where the 0–7 interaction arises because we assume periodic boundary conditions. If spin 5 is flipped, the new energy is

$$
-E_{k+1} = \sigma_0 \sigma_1 + \sigma_1 \sigma_2 + \sigma_2 \sigma_3 + \sigma_3 \sigma_4 - \sigma_4 \sigma_5 - \sigma_5 \sigma_6 + \sigma_6 \sigma_7 + \sigma_7 \sigma_0, \tag{17.34}
$$

and the difference in energy is

$$
\Delta E = E_{k+1} - E_k = 2(\sigma_4 + \sigma_6)\sigma_5. \tag{17.35}
$$

This is cheaper to compute than calculating and then subtracting two energies.

When we advance to two dimensions with the 8 × 8 lattice in Figure 17.6, the change in energy when a spin σ_{i,j} at site (i, j) flips is

$$
\Delta E = 2\sigma_{i,j}(\sigma_{i+1,j} + \sigma_{i-1,j} + \sigma_{i,j+1} + \sigma_{i,j-1}), \tag{17.36}
$$

which can assume the values −8, −4, 0, 4, and 8. There are two states of minimum energy E = −2N for a 2D system with N spins, and they are ones with all spins pointing in the same direction (either up or down). The maximum energy is 2N, and it corresponds to alternating spin directions on neighboring sites. Each spin flip on the lattice changes the energy by four units between these limits, and so the values of the energies are

$$
E_i = -2N,\ -2N + 4,\ -2N + 8,\ \ldots,\ 2N - 8,\ 2N - 4,\ 2N. \tag{17.37}
$$

These energies can be stored in a uniform 1D array via the simple mapping

$$
E' = \frac{E + 2N}{4} \quad \Rightarrow \quad E' = 0, 1, 2, \ldots, N. \tag{17.38}
$$

Listing 17.2 displays our implementation of Wang–Landau sampling to calculate the density of states and internal energy U(T) (17.21). We used it to obtain the
