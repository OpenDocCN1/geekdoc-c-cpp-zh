
[6.20] M. Nashed. Aspects of generalized inverses in analysis and regularization. _Generalized Inverses and Applications_, 1976.

[6.21] N. Nordström. Biased anisotropic diffusion-a unified regularization and diffusion approach to edge detection. _Image and Vision Computing_, 8(4), 1990.

[6.22] S. Paris, P. Kornbrost, J. Tumblin, and F. Durand. A gentle introduction to bilateral filtering and its applications. In _ACM SIGGRAPH 2008_, 2008.

[6.23] P. Perona and J. Malik. Scale-space and edge detection using anisotropic diffusion. _IEEE Transactions on Pattern Analysis and Machine Intelligence_, 12, 1990.

[6.24] R. Ramanath and W. Snyder. Adaptive demosaicking. _Journal of Electronic Imaging_, 12(4), 2003.

[6.25] L. Rudin, S. J. Osher, and E. Fatemi. Nonlinear total variation based noise removal algorithms. _Physica D_, 60, 1992.

[6.26] C. Tomasi and R. Manduchi. Bilateral filtering for gray and color images. In _International Conference on Computer Vision_, 1998.

[6.27] J. Xiao, H. Cheng, H. Sawhney, C. Rao, and M. Isnardi. Bilateral filtering-based optical flow estimation with occlusion detection. In _Proceedings of the European Conference on Computer Vision_, 2006.

[6.28] J. Yi and D. Chelberg. Discontinuity-preserving and viewpoint invariant reconstruction of visible surfaces using a first-order regularization. _IEEE Trans. Pattern Anal. and Machine Intell._, 17(6), 1995.

## 7 Mathematical Morphology

> I think the universe is pure geometry – basically, a beautiful shape twisting around and dancing over space-time. – Antony Garrett Lisi

### 7.1 Introduction

In this chapter, a study of shape begins. Throughout the remainder of this book we will continue to look at shape in many different ways. Here, the topic is introduced at the pixel level, providing some simple, local operations that modify shapes, changing connectivity, and providing nonlinear ways to treat noise.

- (Section 7.2) Binary morphology changes the shape of binary objects. We define the two basic morphological operators, dilation and erosion, on the basis of which two other operators, opening and closing, can be derived. We also discuss some interesting properties of these morphological operators and their applications in noise removal and edge linking.
- (Section 7.3) We extend the discussion to grayscale morphology and define the dilation and erosion operations when the objects are not described in binary values. We progress from grayscale morphology using flat structuring elements to the use of grayscale structuring elements.
- (Section 7.4) As one of the most important applications of morphological operations, we discuss the distance transform (DT) and different ways to compute the DT.

Morphological operations may be considered as either the result of set operations, or the result of composition of functions. Both these approaches are described in this chapter, in order to provide the student with the insight to see similarities and suitability. We will find that set-theoretic ways of thinking about morphology are most appropriate for binary images, and functional notation is more convenient for grayscale images. In section 7.5, an application example of combining dilation, erosion, and distance transform for the purpose of edge linking is provided to illustrate the power of these operations.

1 That is, analogous to set intersection and union.

### 7.2 Binary Morphology

In this section, we first introduce two basic morphological operators, dilation and erosion. We then define opening and closing, two operators that are developed based on dilation and erosion. We also discuss interesting properties of these operators and their applications in solving computer vision problems.

#### 7.2.1 Dilation

First, we present the intuitive definition: the dilation of an image is that same image with all the foreground regions made just a little bit bigger.

Initially, we consider only binary images with foreground pixels having brightness 1 and background 0. With this definition, the foreground may be considered as a set of ordered pairs of the coordinates of each foreground pixel in the image. For example

```
A = {(4, 6), (6, 6), (5, 4), (4, 2), (5, 2), (6, 2)} . (7.1)
```

is a set representation of the image below (where coordinates are shaded).

![](img/5f95dd954ac63cc68119f6f48ca99e18_135_0.png)

Let us define a second image with only two pixels,

```
B = {(0, 0), (0, 1)} (7.2)
```

Consider one pixel in B and call that element b ∈ B. Create a new set by adding the ordered pair b to every ordered pair in A.

For example, for the image A, adding the pair (0,1) results in the set

```
A(0,1) = {(4, 7), (6, 7), (5, 5), (4, 3), (5, 3), (6, 3)}.
```

The corresponding image is

![](img/5f95dd954ac63cc68119f6f48ca99e18_136_0.png)

By now, you have probably observed that \(A_{(0,1)}\) is nothing more than a translation of \(A\). With this concept firmly understood, think about what would happen if you constructed a set of translations of \(A\), one for each pair in \(B\). We denote that set as \(\{A_b, b \in B\}\), that is, \(b\) is one of the ordered pairs in \(B\).

Formally, the *dilation* of \(A\) by \(B\) is defined as \(A \oplus B = \{a + b \mid (a \in A, b \in B)\}\), which is the same as the union of all those translations of \(A\),

\(A \oplus B = \bigcup_{b \in B} A_b \quad (7.3)\)

Using these two sets, \(A\) and \(B\), and thinking of \(B = \{(0, 0), (0, 1)\}\) as an image,

![](img/5f95dd954ac63cc68119f6f48ca99e18_136_1.png)

The resulting union produces

\(A \oplus B = A_{(0,0)} \cup A_{(0,1)} = \{(4, 6), (6, 6), (5, 5), (4, 4), (4, 2), (5, 2), (6, 2), (4, 7), (6, 7), (5, 5), (4, 3), (5, 3), (6, 3)\}\)

which, represented as an image, is

![](img/5f95dd954ac63cc68119f6f48ca99e18_137_0.png)

The number of elements in set A is denoted by #A, (the cardinality of the set). In this example, #A=6, #B=2, and #(A \(\oplus\) B)=12. This happens to be true only coincidentally, because there was no overlap between \(A_{(0,0)}\) and \(A_{(0,1)}\), or said another way: \(A_{(0,0)} \cap A_{(0,1)} = \emptyset\). For a more general problem, this will not be the case. In general,

#(A \(\oplus\) B) \(\le\) #A \(\cdot\) #B . (7.4)

You will observe that usually (for all practical purposes) one of the images is “small” compared to the other. That is, in the example above,

#A >> #B . (7.5)

When this is the case, we refer to the smaller image B, as the structuring element (s.e.). Observe that all images (whether data images or structuring elements) are based on coordinate systems, and coordinates can go positive or negative. The special pixel located at (0,0) is referred to as the origin.

We will frequently use structuring elements, and will often make use of the origin. All the points in an s.e. are relative to some origin, but it is important to note that the origin is not necessarily in the s.e. For example, consider the s.e. {(1,0),(0,1),(-1,0),(0,-1)} that has four points, none of which are (0,0).

Figure 7.1 illustrates a binary image, its dilation, and its erosion using the following structuring element:

| 0 | 1 | 0 |
|---|---|---|
| 1 | 1 | 1 |
| 0 | 1 | 0 |

In the following material, we will no longer distinguish between the set notation and the image represented by that set. Figure 7.2 shows a code clip for implementing dilation.

![](img/5f95dd954ac63cc68119f6f48ca99e18_138_0.png)

Figure 7.1 A binary figure (above) and its dilation and erosion by a 3 x 3 structuring element.

```
// Code Clip: Binary Dilation
#define GOOD(r,c) ((r >= 0) && (r < nr) && (c >= 0) && (c < nc))
int bdila(float **inp, float **sep, float **oup, int nr, int nc,
    int nser, int nsec, int orgr, int orgc, float th)
{
int r, c, i, j, I, J;
for (r = orgr; r < nr; r++)
    for (c = orgc; c < nc; c++)
    {
    if (inp[r][c] > th)
    {
        for (i = 0; i < nser; i++) // i is same direction as r
        for (j = 0; j < nsec; j++) // j is same direction as c
        if (sep[i][j] > th)
        {
        I = i - orgr;
        J = j - orgc;
        if (GOOD(r,c))
        oup[r-1][c-1] = ONE;
        }
    }
}
return 0;
}
```

Figure 7.2 A function that computes binary dilation of input image inp by s.e. sep producing output oup. r and c denote rows and columns in the image, whereas i and j denote rows and columns in the structuring element. orgr and orgc are the coordinates of the origin of the structuring element. th is the threshold that defines foreground as a point with brightness greater than th.
