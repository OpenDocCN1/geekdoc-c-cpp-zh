![](bbox=[0.156, 0.095, 0.345, 0.535])

FIGURE 9-3 Waiting loop to be removed from ISR.

![](bbox=[0.41, 0.095, 0.93, 0.535])

FIGURE 9-4 Writing into a queue from inside an ISR and subsequently emptying it in the background loop.

One solution is to have the ISR write the output data into a queue. The data can be removed from the queue by a background task, as shown in Figure 9-4. The ISR then becomes straight-line code that imposes a more predictable latency on lower-priority interrupts

Using interrupt-driven input and polled waiting loop output is an intuitive solution, since the data flow from input to output is initiated by the input device. Unfortunately, the overall response time (from input to output) of such systems is far from optimal, since the background loop can be suspended by even the lowest priority interrupt. Rather than waiting for the background to output the result, a faster response time can be achieved by using interrupt-driven input/output (I/O) for both input and output.

The general structure of a fully interrupt-driven architecture is shown in Figure 9-5. There is one minor detail that must be resolved when using a queue in this manner. Output devices request an interrupt when they finish processing the current output byte to indicate that they are now ready for the next byte. In other words, the output ISR is