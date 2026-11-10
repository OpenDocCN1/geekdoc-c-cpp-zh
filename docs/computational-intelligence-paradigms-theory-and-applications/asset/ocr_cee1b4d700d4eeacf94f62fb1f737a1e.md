put vector can belong. This output layer typically uses the delta rule and is similar in operation to the counter-propagation paradigm.

The processing elements in the Kohonen layer measures the Euclidean distance of the weights from the presented input patterns. During recall, the Kohonen element with the minimum distance is the winner and outputs a one to the output layer. Since this is a competitive network, once the winning unit is chosen all the other processing elements are forced to zero. Hence the winning element is the nearest element to the input value and this represents the input value in the two-dimensional map.

During the training process, the Kohonen processing element with the smallest distance adjusts its weight to be closer to the values of the input data. The neighbors of the winning element also adjust their weights to be closer to the same input data vector.

The processing elements naturally represent approximately equal information about the input data set. Where the input space has sparse data, the representation is compacted in the Kohonen space, or map. Where the input space has high density, the representative Kohonen elements spread out to allow finer discrimination. In this way the Kohonen layer is thought to mimic the knowledge representation of biological systems.

Self-Organized Maps allow a network to develop a feature map. Self-Organized learning can be characterized as displaying “global order emerging from local interactions”. One example of self-organized learning in a neural network is the SOM algorithm. There are three important principles from which the SOM algorithm is derived:

+   1. Self-amplification
+   2. Competition
+   3. Co-operation

These principles are defined as follows:

+   1. **Self-amplification:** units, which are on together, tend to become more strongly connected. Thus, positive connections tend to be self-amplifying. This is the Hebbian learning principle.
+   2. **Competition:** Units enter into a competition according to which one responds “best” to the input. The definition of “best” is typically according to either (i) the Euclidean distance between the unit’s weight vector and the input, or (ii) the size of the dot product between the unit’s weight vector and the input. Provided the vectors are normalized, a minimum Euclidean distance is equivalent to a maximum dot product so it doesn't matter which you