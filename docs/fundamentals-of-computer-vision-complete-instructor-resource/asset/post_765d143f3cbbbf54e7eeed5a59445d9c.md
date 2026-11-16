
![](img/5f95dd954ac63cc68119f6f48ca99e18_229_0.png)

![](img/5f95dd954ac63cc68119f6f48ca99e18_229_1.png)

![](img/5f95dd954ac63cc68119f6f48ca99e18_229_2.png)

![](img/5f95dd954ac63cc68119f6f48ca99e18_229_3.png)

![](img/5f95dd954ac63cc68119f6f48ca99e18_229_4.png)

![](img/5f95dd954ac63cc68119f6f48ca99e18_229_5.png)

![](img/5f95dd954ac63cc68119f6f48ca99e18_229_6.png)

![](img/5f95dd954ac63cc68119f6f48ca99e18_229_7.png)

Figure 9.13 The result of matching a template extracted from one image in a stereo pair with a second and third image, as a function of the location of the inverse distance to the matching point. Figure from [9.8]. Used with permission.

cameras (All the cameras are assumed to be identical.) The most difficult problem is the determination of which pixels in each camera image correspond to the same points in 3-space. Suppose a small window is extracted from the leftmost image and use the sum of squared differences (SSD) to template match that small window along a horizontal line in the other image. One could graph that objective function vs. the disparity, or the inverse distance (1/z). It is convenient to use the inverse distance and we will typically find that the match function has multiple minima, as illustrated in Figure 9.13. If an image is taken from a third or fourth camera, with a different baseline from camera 1, similar nonconvex curves are found. However, all the curves will have minima at the same point, the correct disparity. Immediately, we have a consistency! A new function (an accumulator) can be formed, the sum of such curves taken from multiple baseline pairs. We find that this new function (called the SSD-in-inverse-distance) has a sharp minimum at the correct answer. Okutomi and Kanade [9.8] have proven that this function always exhibits a clear minimum at the correct matching position, and that the uncertainty of the measurement decreases as the number of baseline pairs increases.

## 9.9 Conclusion

In this chapter, the concept of parametric transforms was introduced in the form of the Hough transform and its descendents, all of which use accumulator arrays. An accumulator array allows for easy detection of consistency, since “things” that are consistent all add to the same accumulator cell, or at least to nearby accumulator cells. By constructing the accumulator array by adding hypotheses, we also gain a measure of noise immunity, since inconsistent solutions tend not to contribute to the globally consistent solution.

The term “Hough transform” is really a misnomer when applied to finding circles, ellipses, etc. Only the original work by Hough [9.4] to find straight lines should really be referred to by the term. However, many authors have come to use the term “Hough transform” when they really mean “parametric transform”. The exception to this is the Generalized Hough Transform [9.1], which has no parameters except the properties of the curve itself.

Since curvature represents rates of change of normal direction, the Gauss map can be related back to curvature. The invertibility of the Gauss map and invariance under rotation and translation are discussed in more detail in [9.5]. The map also finds application in identifying the vanishing points in an image [9.6].

Clustering, mentioned in this chapter as a way to find peaks in the accumulator and in section 8.3 as a way to group colors, is a general and powerful tool. For example, McLean and Kotturi [9.7] use one version of clustering [9.3] to locate the vanishing points in an image.

The topics listed in this chapter do not include all applications of accumulator methods. However the literature provides a variety of examples such as finding parabolas [9.10].

## 9.10 Assignments

Assignment 9.1: In the directory named “leadhole” is a set of images of wires coming through circuit board holes. The holes are roughly circular and black. Use parametric transform methods to find the centers of the holes. This is a project and will require a formal report. In your report, show the image, zoomed to a viewable size. Mark the pixels that are elements of the boundary of the hole, and the center of the hole. This marking process can be easily accomplished by simply setting those pixels to very bright. Process as many images as possible. If your method fails in some cases, discuss why.

Assignment 9.2: You are to use the Generalized Hough Transform approach to both represent an object and to search for that object in an image. (The object is a perfect square, black inside on a white background, centered at the origin, with sides two units long.) You only have five points to use, those at (0, 1), (1, 0), (1, 0.5), (-1, 0), and (0, -1). Fill out the “R-table” that will be used in the generalized Hough transform of this object.

The example table below contains four rows. You are not required to fill them all in, and if you need more rows, you can add them.

| p1(x,y) | p2(x,y) |
|---|---|
| | |
| | |
| | |
| | |

Assignment 9.3: Let P1 = [x1, y1] = [3, 0] and P2 = [x2, y2] = [2.39, 1.42] be two points, that lie approximately on the boundary of the same circular disc. We do not know a priori whether the disk is dark inside or bright. The image gradients at P1 and P2 are 5∠0 and 4.5∠π/4 (using polar notation).

Use Hough methods to estimate the location of the center of the disc, and radius of the disc, and determine whether the disc is darker or brighter than the background.

Assignment 9.4: Let P1 = [x1, y1] = [3, 0], P2 = [x2, y2] = [2.39, 1.42] and P3 = [1.1, 1.99] be three points that lie approximately on the boundary of the same disc. We do not know a priori whether the disk is dark inside or bright. The image gradients at P1, P2, and P3 are 5∠0, 4.5∠π/4, and 4.9∠π/2 (using polar notation), respectively.

Use Hough methods to estimate the location of the center of the disc, and the radius of the disc, and determine whether the disc is darker or brighter than the background.

Assignment 9.5: Noise is always present, even though parametric transforms like the Hough do a remarkably good job of reducing it. Could you apply the concepts we learned in Chapter 6 such as VCD, to an accumulator to reduce the noise in that accumulator? Discuss.

Assignment 9.6: Is the Generalized Hough Transform (GHT) as described in section 9.5 invariant to zoom? That is, suppose you have two regions, A and B, which are identical except for the fact that B is a zoomed version of A. Will the GHT described in that section conclude that they are the same shape? If not, how would you modify that algorithm to make it invariant to zoom?

Assignment 9.7: In Figure 9.11 a Hough accumulator is illustrated. Invent a way to find the peaks using a clustering algorithm. (Do not simply find the brightest point). Suggestions might include weighting each point by the square of the accumulator value, doing something with the exponential of the square of the value, etc.

## Bibliography

- [9.1] D. Ballard. Generalizing the Hough transform to detect arbitrary shapes. *Pattern Recognition*, 13(2), 1981.
- [9.2] Y. Cheng. Mean shift, mode seeking, and clustering. *IEEE Trans. Pattern Anal. and Machine Intel.*, 17(8), 1995.
- [9.3] T. Hofmann and J. Buhmann. Pairwise data clustering by deterministic annealing. *IEEE Trans. Pattern Anal. and Machine Intel.*, 19(1), 1997.
- [9.4] P. V. C. Hough. Method and means for recognizing complex patterns. *U.S. Patent*, 3069654, 1962.
- [9.5] P. Liang and C. Taubes. Orientation-based differential geometric representations for computer vision applications. *IEEE Trans. Pattern Anal. and Machine Intel.*, 16(3), 1994.
- [9.6] E. Lutton, H. Maitre, and J. Lopez-Krahe. Contribution to the determination of vanishing points using the Hough transform. *IEEE Trans. Pattern Anal. and Machine Intel.*, 16(4).
- [9.7] G. McLean and D. Kotturi. Vanishing point detection by line clustering. *IEEE Trans. Pattern Anal. and Machine Intel.*, 17(11), 1995.
- [9.8] M. Okutomi and T. Kanade. A multiple-baseline stereo. *IEEE Trans. Pattern Anal. and Machine Intel.*, 15(4), 1993.
- [9.9] J. Princen, J. Illingworth, and J. Kittler. Hypothesis testing: A framework for analyzing and optimizing Hough transform performance. *IEEE Trans. Pattern Anal. and Machine Intel.*, 16(4), 1994.
- [9.10] H. Wechsler and J. Sklansky. Finding the rib cage in chest radiographs. *Pattern Recognition*, 9, 1977.
- [9.11] Y. Xie and Q. Ji. A new efficient ellipse detection method. In *ICRA*, 2002.
- [9.12] Yli-Jääski and N. Kiryati. Adaptive termination of voting in the probabilistic circular Hough transform. *IEEE Trans. Pattern Anal. and Machine Intel.*, 16(9), 1994.
