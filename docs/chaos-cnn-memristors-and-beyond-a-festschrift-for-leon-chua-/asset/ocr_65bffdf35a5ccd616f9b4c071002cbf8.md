The parameters are fixed as a = 1.0, b = 1.2 and τ = 20. On increasing the noise intensity, σ, we found that complete synchronization is established between two piecewise linear time-delay systems driven by a common Gaussian noise and without any explicit coupling between them. To quantify the degree of synchronization, we define the synchronization error as follows

```
η = ⟨√(x₁(t) − x₂(t))² + (x₁(t − τ) − x₂(t − τ))²⟩ ,
```

where ⟨·⟩ denotes the time average and we have averaged the error for N = 200,000 time steps in our simulations. The synchronization error, η, is illustrated in Fig. 17 as a function of noise intensity σ. It is clear from this figure that the degree of synchronization error decreases for increasing of the noise intensity σ and for σ > 0.006, η approaches zero indicating that the two time-delay systems driven by a common Gaussian noise oscillate in complete synchrony with each other.

We have also estimated the synchronization error as functions of both the noise intensity σ and the time-delay τ to investigate whether a common noise is capable of inducing synchronization in a wide range of delay times. The synchronization error is depicted in Fig. 18 in the range of τ ∈ (2,30) and σ ∈ (0,0.01). This figure portrays that synchronization is achieved even for feeble values of noise intensity for small values of delay time, τ ∈ (2,3) and the critical value of σ required for synchronization increases with the delay time in the range τ ∈ (3,7) and for τ > 7, the two time-delay systems are synchronized for σ > 0.006 as represented in Fig. 17. This confirms that complete synchronization can also be induced in time-delay systems that are driven by a common noise in a wide range of time-delay without any explicit couplings between them.

![](bbox=[0.09, 0.78, 0.42, 0.9])

Fig. 17. Synchronization error, η, as a function of noise intensity in the range of σ ∈ (0,0.01).

![](bbox=[0.52, 0.1, 0.85, 0.25])

Fig. 18. Synchronization error, η, as a function of both the time-delay and the noise intensity in the range of τ ∈ (2,30) and σ ∈ (0,0.01).

# 6. Delay Effects on Synchronization in Complex Networks

Recent investigations on synchronization is focused on nontrivial effects of delay coupling due to a finite propagation time of information transfer in communication channels [48–55]. Delay coupling enhances the synchronizability of networks and interestingly leads to the emergence of a wide range of new collective behavior [48, 49]. Further, it has also been shown that connection delays can actually be conductive to synchronization, so that it is possible for the delayed system to synchronize where the undelayed system does not [48].

Pecora and Carroll introduced an elegant approach, the master stability function (MSF), to investigate the stability properties of a network of oscillators, which allows one to separate the local dynamics of the individual oscillators from the coupling matrix characterizing the topology of the underlying network [56]. Despite of the flurry of independent research activities on both synchronization of delay coupled networks [48–50] and in analysing the stability of synchronization of a network of oscillators by exploiting the MSF [56–58], only a very few recent studies have been dealt with both MSF and delay coupled networks in probing the stability properties of the latter [51–55]. However, these reports limited their analysis either to phase oscillators or to maps except in [51], which reported the enhancement of neural synchrony by delay in two diffusively coupled Hindmarsh-Rose (HR) neurons and in Ref. [54], which analysed optically coupled semiconductor lasers modeled by Lang-Kobayashi equations using MSF. Nevertheless, the authors of [51] admitted that their analysis could not establish the stable