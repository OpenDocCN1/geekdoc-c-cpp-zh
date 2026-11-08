input impulse sequence. Hence, a *cloud of excitation points* is associated to the trajectories, which is denser in the centre and dilutes to the outside. As expected, the position radii follow a Rayleigh distribution (fig 2.b); accordingly, the distributions of x-y distances, as well (as of x-y velocity components), follow a gaussian form. The power spectrum of radii has also a concordant distribution in frequency, given by a second-order transfer function shifted by the natural angular frequency of the system.

Some of the peculiar properties of shot noise excitation arise already when the distributions of the mechanical energy of the system and of the virtual forces are considered. The distribution of the mechanical energy (fig 2.c) (as in addition to its transitions) has a spectral density that nearly follows a Planck type distribution with two degrees of freedom (the correlation factor is approximately 0.97):

$$F(\varepsilon)=A\cdot\frac{\varepsilon^2}{\exp(\varepsilon/\varepsilon_T-1)} \tag{7}$$

where ε represents energy, ε_T a “thermal” equilibrium in the system, while he is disribution of the x-y instant components of the input virtual forces follow a sine law (vector decomposition in uniformly distributed random phases), their mobile media (within a window as long as the feeding period T*) show the expected tendency to gaussian distributions, but with a clear fine reticular structure (fig. 2.d).

The former results show the need to consider the *quantification* of the bioautomaton’s behaviour as regards the *number of capture events associated to the noise density* (N). In fact, it is possible to analyse the device behaviour by decomposing its excitation in terms of a *random sum of k- input modes*, where k=1 always represents one input pulse per feeding period T*, k=2 represents a random sequence of just two impulses per period, k=3 represents three impulses, and so on. Denoting ζ(t) as the mobile average of excitation forces z(t), one gets the distribution $f_z(z)$, shown in figure (2.d), by doing

$$f_z(z)=\frac{1}{\pi}\sum_k b_k f_{zk}(z) \tag{8.a}$$

where:

$$f_{zk}(z)=\int_{0}^{\Omega_{max}}J_0(k\,d\Omega)\cos\Omega z\,d\Omega;\quad b_k=\frac{(\lambda\cdot T)^k\exp(-\lambda\cdot T)}{k!} \tag{8.b}$$

In eq. (8.a) and (8.b) $f_{zk}(z)$ is the *k-modal component* of the distribution density, expressed as the cosine Fourier transform of the k power of the first kind Bessel function of zero order, in the stochastic frequency domain Ω; Ωmax is a cut-off stochastic frequency which rises from the forces reticular structure in stationary conditions. At the same time $b_k$ is a weight factor of mode k, expressed as a *Poisson probability coefficient*.

A k=0 mode can be also defined, which means that no impulse is arriving (no resource is captured), so that the movement is carried out just by the use of the internal storage of energy. According to the *virial theorem* (case kₙ=2), the total average mechanical energy is *half of the system total energy in the k=1 mode*.

Taking into account the previous considerations it is also possible to decompose in k-modes the average value of the angular moment, as well as of the mechanical energy. In fact, the expected angular moment when excited by N capture events per feeding period is:

$$\langle M_\phi\rangle^2=N^2\varepsilon_0^2/\omega_0^2=m_0\omega_0^2r_0^4 \tag{9}$$