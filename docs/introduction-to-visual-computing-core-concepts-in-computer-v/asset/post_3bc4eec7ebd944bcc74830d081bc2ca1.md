
![](img/66c45bbed85bb7ba7f7b05dff49b5060_117_0.png)

Figure 5.3. This shows edges in 1D functions. There can be three types of edges: step edge, ramp edge and roof edge.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_117_1.png)

Figure 5.4. This figure shows how the partial derivatives relate to the kind of edges we see in an image.

denote the image by a 2D function f. So, the gradient of f has a direction. We can compute gradient at a pixel in x-direction and y-direction separately and then combine them to get the gradient of the image at that point as follows.

```
∇f = (∂f/∂x, ∂f/∂y) = (g_x, g_y)  (5.1)
```

The gradient points in the direction of most rapid change as shown in Figure 5.4. In fact, we can quantify the direction and strength of the edge respectively by

```
θ = tan⁻¹ g_y / g_x  (5.2)
```

```
||∇f|| = √(g_x² + g_y²)  (5.3)
```

Therefore, now that we know how to detect edges, the next question is how we evaluate the partial derivatives in the digital domain. For this, we use the method of finite differences. The difference between the pixel's function value and that of its right (or left) neighbor gives g_x at that pixel. Similarly, the difference between its value and that of its top (or bottom) neighbor gives g_y.

```
g_x = f(x + 1, y) − f(x, y)  (5.4)
```

```
g_y = f(x, y + 1) − f(x, y)  (5.5)
```

Figure 5.5. This shows the gradient function represented as kernels or filters which are then convolved with the image to give two images – the gradient in x-direction (top) and y-direction (bottom) at any pixel.

Figure 5.6. Left: The top row shows the same image with noise increased as we go from left to right. The bottom row shows the effect of applying a finite different x-gradient filter to the corresponding images on the top row. These images get grainier and grainier as the noise increases. Right:This shows the Sobel gradient operator for x and y direction.

In fact, we can express this as a kernel or filter as shown in Figure 5.5 and when an image is convolved with each of these filters, we get two gradient images - one each for x and y directions. Once the gradient is detected we identify a pixel as an edgel if the strength of the edge (Equation 5.3) is above a certain value. The value we choose is called a threshold and is a parameter to the edgel detection process. This process of generating a binary image by choosing a threshold is called thresholding. Following the thresholding, instead of generating a binary image, one can also generate an image in which the egdes are marked by different

gray levels based on the direction or strength of the edges. Therefore, the gray value would encode $\theta$ or $\|\nabla f\|$.

The above finite difference gradients are the simplest operator possible and do not take noise in the image into account. Noise has its origin in the physical device and can be modeled by a random value added to every pixel of an image. Noise shows up as graininess in the image and if sufficiently high, it can increase error of most image processing algorithms including edge detection. **Figure 5.6** shows the effect of noise in finding the finite difference to generate the gradient images. The image becomes more and more grainy as the noise increases which indicates that the thresholding will start responding to noise rather than the content of the image. One way to make these filters more robust to noise would be to consider a bigger neighborhood. Several such filters exist and the one that is found to be very robust is the Sobel operator (**Figure 5.6**). The scale value of

1/8 does not make any difference in the edgel detection since the threshold can be adjusted to accommodate for it. It is there to normalize the gradient value. Figure 5.7 shows the results of the Sobel operator on an image where the gray values at the pixels indicate magnitude of the gradient at that pixel.

## 5.1. Edge Detection

![](img/66c45bbed85bb7ba7f7b05dff49b5060_119_0.png)

**Figure 5.7.** From left to right: The original image, the gradient image obtained after applying the Sobel detector where the gray values denote the strength of the edges, the edge binary image after thresholding with gray value of 64 and 96. Note fewer edges exist for larger thresholding value.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_119_1.png)

**Figure 5.8.** This figure shows the effect of noise on edge detection using the Sobel operator followed by thresholding with gray value of 150. From left to right: The original image, the edge detected image, the original image after noise is removed, the edge detected image.

Nevertheless, noise poses a serious issue in edge detection and if it goes beyond a certain level, no operator can really achieve an accurate edgel detection (Figure 5.8). So, it is important to handle noise. The most common way to do it is to low pass filter the image first so that the noise is smoothed out. A Gaussian filter is usually used for this purpose due to the property of reducing high frequency leaks. The edge operator is then applied on the smoothed signal to achieve the edgel detection. This concept is explain pictorially using 1D signals in Figure 5.9.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_120_0.png)

Figure 5.9. This shows the noisy function (f) first smoothed using a Gaussian filter (h) to give h ⋆ f which is then convolved with gₓ = ∂/∂x giving ∂/∂x (h ⋆ f).

However, the operation of smoothing and the gradient filter can be achieved in one filter. It can be showed that

∂/∂x (h ⋆ f) = ∂h/∂x ⋆ f. (5.6)

This means that the effect of applying a gradient filter (∂/∂x) to a function f convolved with a low pass filter h is the same as convolving f with a new filter formed by applying the gradient filter to the low pass filter (∂h/∂x). Therefore, we can take the derivative of the Gaussian low pass filter to create a single filter which can then be convolved with the image to provide our gradient images. This is explained in the Figure 5.10.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_121_0.png)

Figure 5.10. This shows the noisy function (f) convolved with the derivative of the Gaussian, ∂h/∂x, providing g_x = ∂h/∂x * f.

## Curvature Based Detectors

The gradient based operators work well but they suffer from two problems. First, for step or ramp edges (brightness that smoothly changes from one level to another to create the edge rather than a sharp change from one level to another and back to the previous level), they have poor localization (i.e. precise location of the edge) after thresholding which becomes especially evident at thicker edges.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_121_1.png)

This is due to the fact that a step or ramp edge can trigger response on multiple adjacent pixels based on how smooth the step or ramp is. Second, the response of the gradient based operators is different for different direction edges. As a result, the gradient based operators can miss edges based on the thresholding value since the value favors some directions over others.

Curvature based edge detectors alleviate these problems. The basic idea behind these operators lies in the realization that edges occur when the first derivative (or gradient) of an image reaches a maxima or a minima. This means at these points the second derivative or curvature should have a zero-crossing (Figure 5.11). The goal of the curvature based operators is to detect these zero crossings to find the precise location of the edge and mark these pixels. This edge detector is often called the

Figure 5.11. This shows the zero crossing in the 2nd derivative for a feature edge in 1D.

Marr-Hildreth edge detector based on the name of scientists who first proposed it. The advantage of this detector is that it responds similarly to all different direction edges and finds the correct positions of the edges.

The curvature of any 2D function is given by the sum of the directional curvatures in two orthogonal directions as

```
∇² f = ∂² f / ∂x² + ∂² f / ∂y²
```

(5.7)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_122_0.png)

Figure 5.12. The Laplacian operator considering only four perpendicular neighbors (left) and considering all eight neighbors (right).

The curvature at a pixel can be computed using finite differences for digital data. Curvature at a pixel (x, y) in x-direction is computed by the difference between the gradient g_x and g_{x+1} at (x, y) and (x+1, y) respectively. Therefore, curvature in this direction is given by

```
g_x - g_{x-1} = f(x+1, y) - f(x) - (f(x-1, y) - f(x, y))
```

(5.8)

```
= f(x+1, y) - 2f(x) + f(x-1, y)
```

(5.9)

If we consider the same finite differences gradient in the vertical direction and add it to the above formula, the curvature operator will involve the pixel itself and its 4-connected neighbors to the left, right, top and bottom. Similarly, if the diagonal neighbors are also considered, the finite difference formula for curvature involves all the eight neighbors around a pixel, referred to as the 8-connected neighbors. The filters thus formed as shown in Figure 5.12 are called the Laplacian operators. Once the image is convolved for Laplacian operator, pixels at which a zero crossing occurs are marked as edge pixels. In order to detect the zero crossings, first the convolved image is thresholded to retain values

![](img/66c45bbed85bb7ba7f7b05dff49b5060_122_1.png)

Figure 5.13. This figure shows a 2D Gaussian filter, its derivative and a LoG filter along with their analog equations. Sampling these functions would generate the filters we have been discussing for edge detection.
