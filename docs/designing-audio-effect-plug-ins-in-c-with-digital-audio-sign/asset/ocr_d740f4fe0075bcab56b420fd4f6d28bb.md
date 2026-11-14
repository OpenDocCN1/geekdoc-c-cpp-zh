eventually settles out to a constant 1.0 or unity gain condition, so at DC or 0 Hz, the output equals the input. However, there is a one sample delay in the response, causing the leading edge of the step-input to be smeared out by one sample interval. This time smearing is a normal consequence of the filtering.

![](bbox=[0.25, 0.08, 0.75, 0.25])

![](bbox=[0.25, 0.25, 0.75, 0.4])

Figure 4.7: On the first iteration the input sample is used in the difference equation to create the output, x(n) = 0, y(n) = 0 and then the input is shifted into the delay register.

In a feed-forward filter, the amount of time smearing is equal to the maximum delayed path through the feed-forward branches.

![](bbox=[0.2, 0.54, 0.8, 0.72])

![](bbox=[0.2, 0.72, 0.8, 0.9])

Figure 4.8: The process continues with each sample. Here the input 1.0 is combined with the previous input; the second output y(n) = 0.5.