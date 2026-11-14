# 1.10 Bookkeeping

You can see that there are already three sequences to deal with: the input, output, and impulse response, all of which are coded with the same variable n to keep track of the location of samples within the sequence. The first step is to decide how to use n to do this bookkeeping task. Using it to represent the absolute position in the sequence would quickly become tiresome—how do you deal with indexing numbers like x(12,354,233)? Figure 1.17 shows an input signal, x(n), starting from t = 0 or x (0). The x(0) sample is the first sample that enters the signal processing algorithm. In the grand scheme of things, x(0) will be the oldest input sample ever. Indexing the numbers with absolute position is going to be a chore as the index values are going to become large, especially at very high sample rates.

![](bbox=[0.2, 0.25, 0.8, 0.35])

Figure 1.16: An audio signal processing algorithm that converts an input sequence x(n) into an output sequence y(n).

![](bbox=[0.1, 0.43, 0.9, 0.72])

Figure 1.17: Using the absolute position within the sequence is one way to keep track, but the index values are going to get very large very quickly.

Another problem with dealing with the absolute position of samples is that algorithms do not use the sample's absolute position in their coding. Instead, algorithms use the position of the current sample and make everything relevant to that sample. On the next sample period, everything gets reorganized in relation to the current sample again. It might sound confusing at first, but it is a much better method of keeping track of the samples and more importantly, defining the I/O characteristics of the algorithm, called the transfer function. Figure 1.18 shows the input signal frozen at the current time, x(n), and the other samples are indexed based on its location. One sample period later (Figure 1.19) you can see the frame of reference has shifted to the right and that x(n) has now become x(n - 1).