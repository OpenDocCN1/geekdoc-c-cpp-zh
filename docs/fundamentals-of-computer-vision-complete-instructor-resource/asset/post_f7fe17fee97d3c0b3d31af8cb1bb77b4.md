
![](img/5f95dd954ac63cc68119f6f48ca99e18_158_0.png)

Figure 7.26 LEFT: The result of applying Connected Components to the dilated image. MIDDLE: Result of using thinning to find the closed boundaries. RIGHT: Result of using DT-erosion to find the boundaries. From [7.4]. Used with permission.

distance transform has been the subject of many papers (e.g., [7.2]) that improve the accuracy and/or speed up DT algorithms.

With proper combinations of the morphological operators, we can achieve special effects like noise removal and edge linking in a very efficient manner. However, the authors would like to point out that morphology-based noise removal or edge linking only removes noise features of small scale (i.e., smaller than the radius of the s.e.) and closes gaps of relatively small size. For example, in Figure 7.22, the largest gap in the edge is of 3 pixels. Therefore, a DT distance of 2 or less would work. However, suppose the size of the gap is of 7 pixels. Then the DT-dilation with DT distance of 4 or less would be needed, which would completely close up the background region marked with "x" in Figures 7.23 (LEFT) and 7.24 (LEFT). When there are large gaps in the edge, we can make use of the Hough transform, a technique to be discussed in detail in Chapter 9.

### 7.7 Assignments

- Assignment 7.1: In section 7.2.3, we stated that dilation is commutative because addition is commutative. Erosion also involves addition, but one of the two images is reversed. Is erosion commutative? Prove or disprove it.

- Assignment 7.2: Prove (or disprove) that binary images eroded by a kernel, _K_, remain invariant under closing by _K_. That is, prove that \( A \ominus K = (A \oplus K) \ominus K \).

- Assignment 7.3: Show that dilation is not necessarily extensive if the origin is not in the s.e.

- Assignment 7.4: Prove that dilation is increasing.

- Assignment 7.5: Let C be the class of binary images that have only **one** dark pixel. For a particular image, let that pixel be located at $(i_0, j_0)$.

Using erosion and dilation by kernels that have $(0, 0)$ as an element, devise an operator, that is, a set of erosions and dilations, and structuring elements (you may need only one s.e. or you may need more than one), which when applied to an element of C, would output an image with the dark pixel shifted to $(i_0 + 2, j_0 + 1)$. Disregard boundaries.

- Assignment 7.6: Which of the following statements is correct? (You should be able to reason through this, without doing a proof.)

  - 1) $(A \ominus B) \ominus C = A \ominus (B \ominus C)$
  - 2) $(A \ominus B) \ominus C = A \ominus (B \oplus C)$ (7.32)

- Assignment 7.7: Use the thresholded images you created in Assignment 5.4 or (it's up to the instructor) Assignment 5.5. Choose a suitable structuring element, and apply opening to remove the noise.

- Assignment 7.8: In section 7.4, a mask (Figure 7.16) is given and it is stated that application of this mask produces a distance transform that is "not a bad approximation" to the Euclidean distance from the interior point to the nearest edge point. How bad is it? Apply the algorithm to the following image:

| ∞ | ∞ | ∞ | ∞ |
|---|---|---|---|
| ∞ | ∞ | ∞ | ∞ |
| ∞ | ∞ | 0 | ∞ |
| ∞ | ∞ | 0 | ∞ |
| ∞ | 0 | 0 | ∞ |
| ∞ | 0 | 0 | ∞ |

Your instructor may ask you to do this by hand. Show the output after each pass through the program, or your instructor may ask you to write a program.

> CAUTION: If you do this manually, it can be tedious and time-consuming, as you will need to compute by hand a number of steps (something like fifteen). Or, if you write a program: That can be time-consuming too. Be sure you allocate sufficient time.

- Assignment 7.9: Consider a region with an area of 500 pixels of which 120 pixels are on the boundary. You need to find the distance transform from each pixel in the interior to the boundary, using the Euclidean distance. (Note: Pixels on the boundary are not considered in the region – at least in this problem). What is the computational complexity? (Note: You may come up with some algorithm more clever than that used to produce any of the answers below, so if your algorithm does not produce one of these answers, explain it.)

  - a) 60,000
  - b) 120,000
  - c) 45,600
  - d) 91,200

- Assignment 7.10: Trick question: For Assignment 7.9, how many square roots must you calculate to determine this distance transform? Remember, this is the Euclidean distance.

- Assignment 7.11: What is the major difference between the output of a thinning algorithm and the maxima of the distance transform? (choose the best answer).

  - c)
  - a) A thinning algorithm preserves connectivity. The maxima of the DT are not necessarily connected.
  - b) The maxima of the DT are unique, thinning algorithms do not produce unique results.
  - c) The DT preserves connectivity. Thinning algorithms do not.
  - d) Thinning algorithms produce the intensity axis of symmetry. The DT does not.

## Bibliography

- [7.1] C. Arcelli, L. Cordella, L., and S. Levialdi. Parallel thinning of binary pictures. Electron. Letters, (11) 1975.
- [7.2] H. Breu, J. Gil, D. Kirkpatrick, and M. Werman. Linear time Euclidean distance transform algorithms. IEEE Trans. Pattern Anal. and Machine Intel., 17(5), 1995.
- [7.3] C. Huang and O. Mitchell. A Euclidean distance transform using grayscale morphology decomposition. IEEE Trans. Pattern Anal. and Machine Intel., 16(4), 1994.
- [7.4] W. Snyder, M. Hsiao, K. Boone, M. Hudacko, and B. Groshong. Closing gaps in edges and surfaces. Image and Vision Computing, October 1992.
- [7.5] H. Tagare, F. Vos, C. Jaffe, and J. Duncan. Arrangement: A spatial relation between parts for evaluating similarity of tomographic section. IEEE Trans. Pattern Anal. and Machine Intel., 17(9), 1995.
- [7.6] R. van den Boomgaard and A. Smeulders. The morphological structure of images: The differential equations of morphological scale-space. IEEE Trans. Pattern Anal. and Machine Intel., 16(11), 1994.

## Part III

## Image Understanding

Finally! You have an image with relatively sharp edges (except for the occasional missing edge pixel and other defects), smooth region interiors (except that some variation still exists in brightness), and smooth background (except that there may be other objects in the background). Now, all you have to do is identify specific regions (segmentation), describe those regions (measure shapes and calculate features), and recognize them (match them to models). As you can guess, it’s not quite that simple. Nothing is ever that simple. Here’s a simple picture. Can your computer software recognize it?

![](img/5f95dd954ac63cc68119f6f48ca99e18_162_0.png)

This image has library name: StingRay.jpg.

## 8 Segmentation

> The partition between the sage and the fool is more slender than the spider web.
> – Kahlil Gibran

### 8.1 Introduction

Segmentation is the process of separating objects from background. It is the foundation for all the subsequent processes like shape analysis and object recognition.

A segmentation of a picture is a partitioning into connected regions, where each region is homogeneous in some sense and is identified by a unique label. For example, in Figure 8.2 (a “label image”), region 1 is identified as the background. Although region 4 is also background, it is labeled as a separate region, since it is not connected to region 1.

The term “homogeneous” deserves some discussion. It could mean all the pixels are of the same brightness, but that criterion is too strong for most practical applications. It could mean that all pixels are close to some representative (mean) brightness. Stated more formally [8.56], a region is homogeneous if the brightness values are consistent with having been generated by a particular probability distribution. In the case of range imagery [8.31] where we (might) have an equation that describes the surface, we could say a region is homogeneous if it can be described by the combination of that equation and some probabilistic deformation. For example, if all the points in a region of a range image lie in the same plane except for deviations whose distance from the plane may be described by a particular Gaussian distribution, one could say this region is homogeneous.

In this chapter, several ways to perform segmentation are discussed. We progress through problems and methods of increasing complexity:

- (Section 8.2) Threshold-based techniques are guaranteed to form closed regions because they simply assign all pixels above (or below, depending on the problem) a specified threshold to be in the same region. However, using a single threshold only allows regions to be classified as “foreground” and “background.”
- (Section 8.3) Brightness segmentation into two classes is the simplest case. It becomes more challenging when color images are considered and similarities of colors must be considered.
- (Section 8.4) Another level of complexity occurs when it is necessary to determine whether two apparently separate regions are really one region. That is, do they touch? For this, we need connected components.
