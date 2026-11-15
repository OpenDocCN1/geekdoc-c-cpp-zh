![](bbox=[0.23, 0.08, 0.93, 0.23])

**Figure 3.8** Plot of a sine function.

Consider the following three functions:

\(s_1(t) = 3 \sin(2\pi t),\)
\(s_2(t) = 5 \sin(0.4\pi t), \text{ and}\)
\(s_3(t) = 5 \sin(\pi t).\)

Function \(s_1\) has an amplitude of 3, and functions \(s_2\) and \(s_3\) have amplitudes of 5. Function \(s_1\) has a frequency of 1 Hz and thus a period of 1 s; function \(s_2\) has a frequency of 0.2 Hz and thus a period of 5 s; and function \(s_3\) has a frequency of 0.5 Hz and thus a period of 2 s. The phase shift for all three functions is zero. Figure 3.9 contains plots of these three sinusoids.

A property that we will not prove, but that will be useful in analyzing the interaction of waves, is that a sum of two sinusoids is also a periodic signal with a period that is equal to the least common multiple (LCM) of the periods of the two individual sinusoids. Thus, if the two waves are periods are 3 and 6 s, the period of the combined sinusoids is 6. If the two periods are 3 s and 5 s, the period of the combined signal is 15 s. If the two periods are \(\frac{2}{3}\) s and \(\frac{1}{3}\) s, the period of the combined signal is 1 s. If the two periods are \(\frac{2}{3}\) s and 2 s, the period of the combined signal is 6 s. Developing an algorithm to determine the least common multiple for two numbers is a nontrivial exercise. Since we want to focus on the characteristics of the wave interaction, we will assume that the wave periods entered into the program will be integers (in seconds). With this assumption, the least common multiple can be shown to be less than or equal to the product of the two integers. Thus, if we use the product as the period for the combined wave, we know that the maximum period will be in this period. Figure 3.10 contains the sums of each pair of sinusoids in Figure 3.9. Note that the period of \(s_1 + s_2\) is 5 (the LCM of 1 and 5), the period of \(s_2 + s_3\) is 10 (the LCM of 5 and 2), and the period of \(s_1 + s_3\) is 2 (the LCM of 1 and 2).

We now need to consider the relationship between the wavelength and the period of a wave. For a wave in deep water [5], this relationship is

\(L = 5.13 T^2,\)

where \(T\) is in seconds and \(L\) is in feet. This relationship does not hold for shallow-water waves. We now have all the pieces to describe a solution to the problem presented at the beginning of this section.

Write a program that will allow the user to enter the period and wave height for two waves, where the period (in seconds) is an integer and the wave height is measured in feet. The program should compute and print the wavelength for each wave. It should also compute 200 points of the sum of the two waves over a period equal to the product of the two individual periods. It should then find the maximum of the 200 points of the sum, and print that as an estimate of the maximum wave height of the combined waves, assuming that the phase difference between the two waves is zero.