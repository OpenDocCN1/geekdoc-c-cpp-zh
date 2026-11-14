You can tell why it's called feed forward—the input branches feed forward into the summer. The signal flows from input to output. There is no feedback from the output back to the input. Now, suppose we let the coefficients $a_0$ and $a_1$ both equal 0.5 in Figure 4.6.

In order to analyze this filter we can go the easy but tedious route or the difficult but elegant route. Let's start with the easy way. In order to figure out what this does, you apply the five basic digital test signals you learned in Chapter 1 to the filter and then manually push the values through and see what comes out. You only need a pencil and paper or a simple calculator. The five waveforms we want to test are:

+   1. DC (0 Hz)
+   2. Nyquist
+   3. ½ Nyquist
+   4. ¼ Nyquist
+   5. Impulse

![](bbox=[0.3, 0.43, 0.7, 0.58])

Figure 4.5: The first-order feed-forward filter.

![](bbox=[0.3, 0.63, 0.7, 0.78])

Figure 4.6: What kind of filter is this? What are its frequency and phase responses?

For each audio sample that enters there are two phases to the operation:

+   1. Read phase: The sample is read in and the output is formed using the difference equation and the previous sample in the delay register.
+   2. Write phase: The delay element is overwritten with the input value—the sample stored in the single $z^{-1}$ register is effectively lost.

Start with the DC/step input and begin sequentially applying the samples into the filter shown in Figures 4.7 through 4.10.

Now, observe the amplitude and phase shift of the input versus output—the output amplitude