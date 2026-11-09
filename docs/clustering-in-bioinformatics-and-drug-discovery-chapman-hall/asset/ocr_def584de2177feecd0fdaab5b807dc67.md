for as a first step after scaling and transformations. The choice of clustering algorithms may in turn be restricted by the computational resources implied by either the size of N or the size of the dimension, p, the number of variables, relative to N.

In some chemoinformatics applications N can be very large, on the order of several millions and up, and p may also be in the hundreds, or, in the case of binary or count fingerprints, in the several thousands. Expression data dimensions are typically smaller, but can be by no means insignificant.

# ## 2.6 Measures of Similarity

Similarity and its mirror, dissimilarity, quantitatively measure how close two things or a collection of things are to one another. This is within a space, defined by the data type and the measure. There are many ways to quantify similarity given the data type. The Euclidean distance between points in simple geometry is one such measure of dissimilarity. The measure or distance, d, between two points x, and y in Euclidean space with dimension P is

d = √(Σ_{i=1}^{P} (x_i − y_i)^2). (2.1)

Euclidean geometry maps intuitively to relate to every day experience where we have a sense of near and far so it is a simple and easy measure to understand. But measures of similarity and dissimilarity apply to the type of data: not all data are conveniently transformed to plane geometry, or even to the generalization of many dimensioned geometry for that matter. Thus, for binary data there are a host of measures, some simple and common, some complex and obscure, and similarly for count and continuous data.

Much is made of whether or not a measure is a metric: that is, does all of the data admit to the triangular inequality. We can see this most clearly with the use of the Euclidean distance, but it takes a bit more mathematics to show that other measures are or are not metrics [31, 54]. Simply, the following properties of d(x, y) in general, for any data items under consideration x, y, and z:

+   - d(x, y) ≥ 0 (Nonnegative)
+   - d(x, y) = 0 iff x = y (Reflexive)
+   - d(x, y) = d(y, x) (Symmetric)
+   - d(x, y) + d(y, z) ≥ d(x, z) (Triangle Inequality)