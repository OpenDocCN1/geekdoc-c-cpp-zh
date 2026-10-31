was operating in the room, and the associated cyclic behavior (of about 136 Hz) was apparent in the “silent spaces” in the signal. Using the tswge R function butterworth.wge, we applied a fourth-order zero-phase band-stop Butterworth filter to attempt to remove the fan noise. Our sampling rate was 8000 Hz (samples per second), so a frequency of 136 Hz corresponds to 136 cycles per 8000 units, or a frequency of f = 136/8000 = 0.017. We applied a fourth-order band-stop filter designed to filter out frequencies in the band f ∈ [0.0075, 0.0275]. The filtered signal is shown in Figure 2.10 where it can be seen that cyclic behavior due to the fan has been largely removed (with some ambient noise still remaining) while leaving the speech signal essentially unchanged.

# Appendix 2A: Theorem Poofs

# Proof of Theorem 2A.1

Without loss of generality, we assume μ = 0. If m > k then

E[ (∑_{j=0}^{m} h_j Z_{t-j} - ∑_{j=0}^{k} h_j Z_{t-j})^2 ] = E[ (∑_{j=k+1}^{m} h_j Z_{t-j})^2 ]  (2A.1)
≤ [ ∑_{j=k+1}^{m} { E | h_j Z_{t-j} |^2 }^{1/2} ]^2  (Minkowski inequality)
= [ ∑_{j=k+1}^{m} | h_j | sqrt(Var(Z_{t-j})) ]^2
≤ [ sqrt(M) ∑_{j=k+1}^{m} | h_j | ]^2 .