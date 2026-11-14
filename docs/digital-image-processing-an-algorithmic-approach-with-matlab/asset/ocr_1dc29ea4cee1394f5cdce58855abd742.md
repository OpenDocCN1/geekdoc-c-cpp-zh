other sources; and blurring of the image by linear motion of the imaging equipment or misalignment, causing defocusing.

One of the most intriguing questions in image processing is the problem of recovering the desired or perfect image from a degraded version. The amount of lost information that can be recovered from the blurred version of an image depends on the extent of degradation. This sets a bound on the performance of the image restoration algorithm.

In order to solve the image restoration problem, mathematical models are required for real-world processes involved in image generation, formation, and recording. It may be argued that the ultimate objective of a restoration scheme is the inverse manipulation of the degraded model into the original nondegraded model. If this task is performed based on certain statistical knowledge, known beforehand, about the degradation process, the medium, and the noise, the procedure is called a priori restoration. On the other hand, this information may not be available with a high degree of fidelity. In that case, blind restoration or blind deconvolution methodologies are adopted.

# 7.2 IMAGE REPRESENTATION

In order to understand the functioning of certain restoration techniques, the morphology of the target image and the degradation in it should be understood first. The general notation for digital images is to consider them as matrices represented in x and y coordinates. Thus, an image of interest f(m,n) is a matrix of m x n order that is the result of 2D sampling of the real image. However, the image model f(m,n) is not the observed image because of the distortion present in the imaging system. A general imaging system block diagram is shown in Figure 7.1.

Hence, the observed image g(m,n) is given by

g(m,n) = f(m,n) \circledast h(m,n) + \eta(m,n), (7.1)

![](bbox=[0.2, 0.75, 0.78, 0.88])

FIGURE 7.1 Imaging system and its block diagram.