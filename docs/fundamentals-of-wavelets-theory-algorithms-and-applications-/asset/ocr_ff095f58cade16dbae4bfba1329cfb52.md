![](bbox=[0.146, 0.083, 0.823, 0.265])

![](bbox=[0.146, 0.292, 0.823, 0.465])

Common sense dictates that to know the local frequency contents of a signal, we should first remove the desired portion from the given signal and then take the Fourier transform of the removed part. Such a method of the time-frequency analysis is referred to as short-time Fourier transform (STFT). Before we discuss STFT, let us discuss the notion of window function, by means of which the desired portion of a given signal can be removed.

# 4.1 WINDOW FUNCTION

A desired portion of a signal can be removed from the main signal by multiplying the original signal with another function that is zero outside the desired interval. Let \(\phi(t) \in L^2(\mathbb{R})\) be a real-valued window function. Then the product \(f(t)\phi(t - b) =: f_b(t)\) will contain the information of \(f(t)\) near \(t\)