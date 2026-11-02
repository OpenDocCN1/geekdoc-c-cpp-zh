# 3.2.1 Selection of transformation parameters for DRC

The intensity I of the color image $I_c$ can be determined by:

$I(m,n)=0.2989r(m,n)+0.587g(m,n)+0.114b(m,n)$ (17)

where $r$, $g$, $b$ are the red, green, and blue components of $I_c$, respectively, and $m$ and $n$ are the row and column pixel locations respectively. Assuming I to be 8-bits per pixel, $I_n$ is the normalized version of $I_c$ such that:

$I_n(m,n)=I(m,n)/255$ (18)

Using linear input-output intensity relationships typically does not produce a good visual representation compared with direct viewing of the scene. Therefore, nonlinear transformation for DRC is used, which is based on some information extracted from the image histogram. To do this, the histogram of the intensity images is subdivided into four ranges:

$r_1=0-63$, $r_2=64-127$, $r_3=128-191$ and $r_4=192-255$. $I_n$ is mapped to $I_n^{drc}$ using the following:

$I_n^{drc}=\begin{cases}(I_n)^x+\alpha & 0<x<1\\(0.5+(0.5I_n)^x)+\alpha & x\ge1\end{cases}$ (19)

The first mapping pulls out the details in the dark regions, and the second suppresses the bright overshoots. The value of $x$ is given by

$x=\begin{cases}0.2, & \text{if } (f(r_1)+r_2)\ge(f(r_3)+r_4)) \land (f(r_1)\ge(f(r_2)))\\0.5, & \text{if } (f(r_1)+r_2)\ge(f(r_3)+r_4)) \land (f(r_1)<(f(r_2)))\\3.0, & \text{if } (f(r_1)+r_2)<(f(r_3)+r_4)) \land (f(r_1)\ge(f(r_2)))\\5.0, & \text{if } (f(r_1)+r_2)<(f(r_3)+r_4)) \land (f(r_1)<(f(r_2)))\end{cases}$ (20)

where $f(a)$ refers to number of pixels between the range $(a)$, $f(a_1+a_2)=f(a_1)+f(a_2)$, and $\land$ is the logical AND operator. $\alpha$ is the offset parameter, helping to adjust the brightness of image. The determination of the $x$ values and their association with the range-relationships as given in Equation 20 was done experimentally using a large number of non-uniform and uniform dark images and $x$ value can be also determined manually. The DRC mapping of the intensity image performs a visually dramatic transformation. However, it tends to have poor contrast, so a local, pixel dependent contrast enhancement method is used to improve the contrast.

# 3.2.2 Selection of surround parameter and color restoration

Many local enhancement methods rely on center/surround ratios [L. Tao, 2005]. Hurlbert [A. C. Hulbert, 1989] investigated the Gaussian as the optimal surround function. Other