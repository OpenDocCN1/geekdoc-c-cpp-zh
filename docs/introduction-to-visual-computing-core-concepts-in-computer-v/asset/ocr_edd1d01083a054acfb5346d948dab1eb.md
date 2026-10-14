![](bbox=[0.17, 0.15, 0.82, 0.58])

Figure 4.3. This figure shows how the sine and cosine waves are scaled by the factors produced in x_c and x_s. These waves when added will create x, the original signal shown on the left.

you the particular representation used.

Now, consider the cosine wave c_k whose amplitude is given by x_c[k]. Note that c_k is a signal with N samples. Further, it is a cosine wave that makes k cycles over these N samples, and has an amplitude of x_c[k]. This cosine wave can be described as

c_k[i] = cos( (2π k i)/N ) = cos(2π f i) = cos(ω i)    (4.1)

where i denotes the i th sample of c_k, 0 ≤ i ≤ N − 1. Similarly, the k th sine wave, s_k, is given by

s_k[i] = sin( (2π k i)/N ) = sin(2π f i) = sin(ω i)    (4.2)