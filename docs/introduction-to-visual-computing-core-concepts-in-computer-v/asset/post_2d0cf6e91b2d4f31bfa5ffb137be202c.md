
![](img/66c45bbed85bb7ba7f7b05dff49b5060_69_0.png)

**Figure 3.15.** This figure illustrates severe aliasing artifacts that can occur due to sub-sampling without prefiltering.

Let the low pass filtered image be $I_l$ and the high passed image be $I_h$. Therefore

$$I_h = I - I * l$$  (3.10)

$$= I * \delta - I * l$$  (3.11)

$$= I * (\delta - l)$$  (3.12)

In the second line of the above algebra, we consider the image to be an all pass filtered version of itself. Using this fact and the mathematical properties of convolution, we see that the high pass filtered image $I_h$ can be expressed as the convolution of the original image $I$ with a single filter given by $\delta-l$. This gives us the design of an *high pass filter* resulting from the subtraction of any low pass filter from $\delta$, as shown in **Figure 3.16**. This figure also shows the general shape of any high pass filter with its characteristic positive spike near the center and the negative lobes adjacent to it. For example, a Gaussian function is another good low pass filter which has a much smoother response than the box filter. In this case, the high pass filter will still look the same having smoother and deeper negative lobes. The image formed due to high pass filtering will have the complementary frequencies that will give the details of the image. This is illustrated in **Figure 3.17**. Now, do not confuse a Gaussian filter with a Gaussian pyramid. Both are named after the same person, but are entirely different concepts. A Gaussian filter is a kind of low pass filter, while a Gaussian pyramid is a pyramid of image formed by progressively applying any low pass filter on an image, not necessarily a Gaussian filter.

Now, let us consider the Gaussian pyramid $G_0, G_1, \ldots, G_n$. Let us now build

# Figure 3.16. This figure illustrates the creation of high pass filters (bottom) in 1D from box filters of size 3 (top) and 5 (middle)

another pyramid L0, L1, ..., Ln−1 where Li = Gi − Gi+1. Note that to construct this pyramid, Gi+1 has to be resampled at double the resolution since Gi and Gi+1 are not at the same resolution to perform an image subtraction (which is essentially a pixel by pixel subtraction). Now note what happens from the frequency standpoint in this pyramid. If f0, f1, ..., fn are considered to be the cut-off frequency of G0, G1, ..., Gn, then each of Li consists of only a band or range of frequencies fi − fi+1. Therefore, these images are created by passing a band of frequencies. This pyramid is called a Laplacian Pyramid as illustrated in Figure 3.18.

Now, let us consider the single filter that we will use on G0 to create the ith level of the Laplacian pyramid Li. This single filter is given by convolving l with itself for i + 1 times and subtracting from it l convolved for i times. This filter passes the band of frequencies between fi and fi+1 and is the band pass filter.

## 3.2.3 2D Filter Separability

From the above discussions, we are now capable of visualizing or generating 2D filters like a 2D box filter or a 2D high pass filter (Figure 3.19). Now, when considering 2D filters, there is another important property to be aware of. This is called separability. Let us consider a p × q 2D filter given by h[i][j] where

![](img/66c45bbed85bb7ba7f7b05dff49b5060_70_0.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_72_0.png)

Figure 3.18. On the left we show the frequency response of the band pass filters which can act on the original picture to create the first three levels of the Laplacian pyramid. On the right we show the Laplacian pyramid itself for the same image shown in Figure 3.13. The images are shown in the same size on the top for better perception.

We will see in the next chapter that this Gaussian function is a very good low pass filter (Figure 3.19). Now, let us consider the 2D Gaussian filter given by

φ(x, y) = 1/(2πσ²) e^(-(x²+y²)/(2σ²))  (3.15)
= φ(x) × φ(y).  (3.16)

Since the 2D Gaussian can be expressed as above, it is a separable filter. Therefore, it can be implemented efficiently using

I ⋆ φ(x, y) = (I ⋆ φ(x)) ⋆ φ(y)

## 3.2.4 Correlation and Pattern Matching

In this section, we will introduce yet another application of convolution. Consider a picture which is a checkerboard pattern and a filter which looks like a corner of the checker board (Fig 3.20). Consider the image and template both to be in grayscale with values between 0 and 1 (0 for black and 1 for white).

![](img/66c45bbed85bb7ba7f7b05dff49b5060_73_0.png)

Figure 3.19. Visualizing the 2D filters from their 1D counter part: Box filter (left), Gaussian filter (middle) which is a very good low pass filter and High-Pass Filter (right) obtained by subtracting the Gaussian from a delta.

On the left in Fig 3.20 the value of the convolution is shown for sample colored windows. Note that the value of the convolution is highest where the template matches the image at the blue window. It is also the lowest where the image is exactly complementary to the template as in the red window. Further it is something in between at the purple window which is also showing a corner but with a different distribution of black and white around it. But the problem is, other areas like the green window also shows the highest value and the yellow window shows the lowest value. Intuitively, correlation should provide a measure of the match between the template and the subregion of the image being considered. From that perspective, the subregions defined by the green and yellow windows are similar despite their vastly different colors (one black and one white). The justification for this is based on the variation of colors present in the template which can be considered maximal. Since correlation is a measure of similarity, one would expect the blue window to have the highest value since it has identical spatial distribution as the template (white on top right and bottom left quadrants and black elsewhere). Using the same measure of similarity, the red window should have the lowest value though it has the same color variation due to the complementary spatial distribution (black on top right and bottom left quadrants and white elsewhere). Also, one would expect the yellow and green windows to have some value right in the middle of these lowest and highest values since the template has to go through either of these to go to the complementary pattern in the red window. Similarly, the pattern in the purple window should also have a value between the lowest and the highest, but it should be closer to the lowest value (red square) than the highest value (blue square) since the

spatial distribution of the black and white pixels in the purple window is more similar to the former than the latter.

Figure 3.20. This image shows the convolution of an 8 × 8 template that needs to be matched with an identical subregion to the checkboard image. On the left image this is achieved by a simple convolution of the template with the image and on the right image this is achieved by first subtracting the average value of all the pixels from the template and the region to be matched before applying the convolution. On the left image, window of different colors show the result of convolution in those windows. On the right image, the information is also augmented with the value of the mean (μ) at those windows.

## Put a Face to the Name

Pierre-Simon Laplace (23 March 1749 to 5 March 1827) was an influential French scholar whose work was important to the development of mathematics, statistics, physics, and astronomy. He summarized and extended the work of his predecessors in his five-volume Mecanique Celeste (Celestial Mechanics) (1799–1825). This work translated the geometric study of classical mechanics to one based on calculus, opening up a broader range of problems. He formulated the Laplacian differential operator widely used in mathematics, pioneered the Laplace transform that forms the cornerstone of many branches of mathematical physics, and was one the first scientists to postulate the existence of black holes and the notion of gravitational collapse.

Laplace was the son of a farmer and cider merchant who intended that

![](img/66c45bbed85bb7ba7f7b05dff49b5060_74_0.png)
