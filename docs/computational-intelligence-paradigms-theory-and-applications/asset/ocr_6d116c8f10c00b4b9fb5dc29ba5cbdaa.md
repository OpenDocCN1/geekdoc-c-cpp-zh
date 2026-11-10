association and gives the best output similar to the input pattern presented initially. Similar to the Hopfield network, the bi-directional associative memory network is liable to incorrectly find a trained pattern when complements of the training set are used as the unknown input vector.

# Architecture

The layers in BAM are referred as X-layer and Y-layer instead of input and output layer, because the weights are bidirectional and the algorithm alternates between updating the activations of each layer. Three forms of BAM are

+   1. Binary
+   2. Bipolar
+   3. Continuous

But the architecture for the three types remains the same. The architecture of BAM is shown in Figure 4.12.

![](bbox=[0.1, 0.49, 0.92, 0.78])

**FIGURE 4.12:** Architecture of Bi-Directional Memory Network

The hetero associative BAM network has “n” units in X-layer and “m” units in Y-layer. The connections between the layers are bi-directional, i.e., if the weight matrix for signals sent from the X-layer to Y-layer is W, then weight matrix for signals sent from Y-layer to X-layer is W_T.