Due to the complexity of the implementation, a better approach that utilizes some interesting properties of the Fourier transform is presented here. If one of the images is symmetric, then flipping it columnwise will not make any difference and, hence, the correlation and convolution can be treated in the same way. Because convolution in the spatial domain becomes pixel-by-pixel multiplication in the frequency domain, which is a much faster process than convolution, the cross-correlation can, therefore, be applied using Fourier transforms of the two images. Hence:

$R_{xy} = X(u,v)Y(u,v) \Rightarrow \rho_{xy} = \mathfrak{F}^{-1}R_{xy}.$ (13.4)

Now, consider the case when one of the foregoing two images is the target object in the source image, which itself is the second image. Wherever there is a perfect match between the source image and the target image, the cross-correlation is also very large. The resulting correlation image is then thresholded to isolate the location points.

Figure 13.4 shows an interesting example of the application of such a technique in which the goal is to count the number of trees present in the

![](bbox=[0.255, 0.485, 0.755, 0.64])

(a)

![](bbox=[0.255, 0.67, 0.755, 0.84])

(b)

FIGURE 13.4 Using cross-correlation-based target tracking. (a) Original scene with trees and target is highlighted with dotted rectangle, (b) result of correlation highlighting the peaks.