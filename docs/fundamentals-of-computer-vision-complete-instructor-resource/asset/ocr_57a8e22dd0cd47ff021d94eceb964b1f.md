So \( B = \{(0, 0), (1, 0)\}\), and therefore \(\tilde{B} = \{(0, 0), (-1, 0)\}\). Rather than tediously listing all the 17 elements of \( A \), just draw

![](bbox=[0.19, 0.18, 0.87, 0.4])

then

![](bbox=[0.27, 0.46, 0.76, 0.68])

The second line of Figure 7.1 illustrates the erosion on the right, compared to dilation on the left.

# ## 7.2.3 Properties of Dilation and Erosion

Here, we discuss a couple of important properties of the two morphological operators.

+   * Commutative property: Dilation is commutative, which means we can dilate images in any order without changing the result:

\( A \oplus B = B \oplus A . \quad (7.8) \)