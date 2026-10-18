# # Energy-Efficient Communication

signal _r_ is first passed through three bandpass filters (BPFs) as shown in the figure, with center frequencies at _f_c + Δ_f_, _f_c and _f_c − Δ_f_ (corresponding to _A_, _B_ and _C_, respectively). The outputs of these bandpass filters are applied to the inputs of three envelope detectors (ED) to derive the values _e_A, _e_B and _e_C_ at their outputs, corresponding to the symbols _A_, _B_ and _C_ respectively. In the ideal situation when there is no noise (η = 0), only one of these _e_A, _e_B and _e_C_ will assume a non-zero value if the transmitted symbol is _A_ or _B_ or _C_, and all of _e_A, _e_B and _e_C_ will be zero if the transmitted symbol is _N_. However, due to noise, even if the transmitted symbol is, for example, _A_, _e_B and _e_C_ may have non-zero values, although we may assume in this situation that _e_A > _e_B and _e_A > e_C_. Similarly, if the transmitted symbol is _B_ (or _C_), not only _e_B (or _e_C_) will have a non-zero value, but _e_A and _e_C_ (or _e_A and _e_B_) may also assume small non-zero values. If the transmitted symbol is _N_, all of _e_A, _e_B and _e_C_ may assume small non-zero values.

To detect the transmitted symbol correctly in the presence of channel noise, we first pass _e_A, _e_B and _e_C_ through a comparator to find which one is the largest, and also we use three threshold detectors to see whether _e_A, _e_B or _e_C_ is above a certain

![](bbox=[0.176, 0.08, 0.824, 0.366])

# FIGURE 8.19: Representative FSK receiver for CNS scheme