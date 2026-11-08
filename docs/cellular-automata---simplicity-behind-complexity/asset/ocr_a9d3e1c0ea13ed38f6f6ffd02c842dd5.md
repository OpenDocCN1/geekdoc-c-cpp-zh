The most active cells access the bus more frequently than less active ones, for example, the AER information transmitted by a visual AER sensor is usually coded in gray levels, so the number of events transmitted by a pixel through the bus identifies the gray level of that pixel.

# 3. Cellular automaton and AER processing

One of the first processing layers in the cortex consists of applying different kinds of convolution filters with different orientations and kernel sizes. These spike-based convolution filters may be developed through an AER system based on Cellular Automaton (AER-CA).

The philosophy of AER systems is lightly different from CA but also similar in a certain sense, so an AER-CA only uses some characteristics of each one. For example, the state of a cell is a function of the current state of the cell and its neighborhood like CA, but a cell only modifies its state when it receives a stimulus.

An AER-CA consists of a 2D grid of cells and every cell is connected to its neighbors. The state of a cell is defined by a set of bits that varies longitudinally when a stimulus arrives. The state of each cell is defined as a function of current state of the cell and its neighbors. When an AER event arrives, its address is decoded and a spike is sent to the corresponding cell. When a cell receives a spike, its state with an increment of the centre of the K×K kernel coefficient and it sends a spike to its neighbors which increments its state by the corresponding K×K kernel coefficient, i.e. the convolution kernel is copied in the neighborhood of the targeted cell. Therefore, for each spike received, several increment operations are carried out in the neighborhood of the target cell. When a cell reaches its threshold, a spike is produced and the state of the cell is reset.

![](bbox=[0.273, 0.529, 0.763, 0.744])

Fig. 2. Behavior of an AER-CA

In a Bi-dimensional image convolution, each cell represents a pixel from the image. So, each cell receives a number of events depending on the gray level of the corresponding pixel, so neighborhood increments its state as many times as the gray level and thus the multiplication of the convolution operation is implemented.

An acknowledge signal is sent to the AER emitter when the cell and its neighbors are updated. If the cell state achieves a threshold, such cell generates an event and resets itself.