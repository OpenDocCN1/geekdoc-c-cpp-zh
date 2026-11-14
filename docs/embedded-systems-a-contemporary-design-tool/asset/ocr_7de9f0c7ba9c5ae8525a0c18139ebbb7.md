negligible. As the transmission rate of the bus signals increases, the consequences of the delays become more significant. Under such circumstances, the following must be considered in higher performance systems:

![](bbox=[0.09, 0.15, 0.49, 0.26])

![](bbox=[0.09, 0.27, 0.49, 0.42])

# Figure P2.15

The delay for each individual bus signal is going to be different. That is, each signal on the bus is going to arrive at an individual module at a slightly different time.

As the collective signals propagate down the bus from source to destination, the set will experience a (different) delay along the bus. Thus, signals arriving at modules close to the source will see the signals at different times from those at greater distance.

The following circuit fragments in Figure 2.15 illustrate one line of a system bus interconnecting three modules and a basic first-order model for a segment of that path. The buffer B0 isolates the segments in the model and has no delay.

+   (a) Using the segment model given to model the bus between each module, build a model of a 4-bit bus interconnecting three modules.

+   (b) Place the bit patterns 0101 1010 successively onto the bus at the source. Draw a detailed timing diagram showing the propagation of the wave front down the bus. That is, show how the signals appear, in time, at the outputs of buffers B1-B3 on each of the respective modules. Make certain that you take into account the variation in delay through each of the module buffers B1-B3.