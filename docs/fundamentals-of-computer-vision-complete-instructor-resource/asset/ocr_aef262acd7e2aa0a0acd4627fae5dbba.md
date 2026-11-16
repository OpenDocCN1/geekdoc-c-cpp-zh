![](bbox=[0.193, 0.116, 0.882, 0.382])

Figure 11.12 Enlargement of the same area from the two images in Figure 11.11: illustrating two corresponding points, points 42 and 69.

# 11.6 HoG

The Histogram of Oriented Gradients (HoG) descriptor [11.8] extends the use of histograms of gradient directions in SIFT to a more dense distribution of these gradient histograms. This approach has been demonstrated to be particularly good at identifying pedestrians in traffic scenes.

# 11.6.1 The HoG Descriptor

Dalal and Triggs, in their description of the concept of HoG, [11.8] first divide the image into ‘cells’ of 8 × 8 pixels. At every pixel in the cell, the gradient magnitude and direction are computed. The cells are grouped into blocks of two cells, or sixteen pixels on a side. Each cell thus defined contains 64 pixels and each block 256. A histogram of the gradient direction is created for each cell, and each such histogram is partitioned into 9 bins over 180 degrees.

The histograms in each block are normalized to correct for contrast variation due to illumination differences (See [11.8] for details on the normalization). Overlapping blocks are used to build the final descriptor, a vector of histograms.

The HoG descriptor may be visualized as illustrated in Figure 11.13 that shows the result of HoG applied to a person sitting.

# 11.6.2 Matching HoG Descriptors

Since the HoG descriptors are rather long vectors, they are usually matched using Support Vector Machines (SVMs), one of the advanced methods in pattern recognition systems. They have excellent performance, if the problem satisfies their architecture. They are extremely well suited to answering the question “Is the thing I am looking at an X or