except that the new location in the \( t - \omega \) domain is shifted along the frequency axis by the carrier frequency \( \omega_0 \).

# 4.3 DISCRETE SHORT-TIME FOURIER TRANSFORM

Similar to the discussion of Section 3.10, we can efficiently evaluate the integral of (4.7) as a series sum by appropriately sampling the function \( f(t) \) and the window function \( \phi(t) \). In its discrete form, the short-time Fourier transform can be represented as

(4.23) \( G_{\phi} f(b_n, \xi_n) = h \sum_{k=0}^{N-1} f(t_k) \phi(t_k - b_n) e^{-j \xi_n t_k}, \)

where

(4.24) \( t_k = bk = kh; \quad k = 0, ..., N-1 \)

and

(4.25) \( \xi_n = \frac{2\pi n}{Nh}; \quad n = -\frac{N}{2}, ..., \frac{N}{2}. \)

In particular, when \( h=1 \), we have

(4.26) \( G_{\phi} f(n, \xi_n) = \sum_{k=0}^{N-1} f(k) \phi(k-n) e^{-j \frac{2\pi kn}{N}}. \)