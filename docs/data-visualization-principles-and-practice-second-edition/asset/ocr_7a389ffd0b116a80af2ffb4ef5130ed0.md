![](bbox=[0.075, 0.12, 0.765, 0.39])

Figure 6.25. Line integral convolution visualization. (a) Input noise. (b) The resulting LIC texture.

which are coherent along various types of flow lines, such as streamlines or streaklines, and show a high noise-like variation between neighboring flow lines. This basic principle set aside, the specific algorithms differ in many respects, such as the type of vector field they can depict (stationary or time-dependent), the dimension of the depicted domain (planar, curved surface embedded in 3D, or volumetric), whether they generate a still or an animated texture, and the actual implementation used to create the texture. We point the interested reader to a survey article on this topic [Laramee et al. 04].

# 6.6.1 IBFV Method

A particularly attractive algorithm for texture-based vector visualization is the Image Based Flow Visualization method, or IBFV [van Wijk 02a]. IBFV and its variants [van Wijk 03, Telea and van Wijk 03] produce not just static, but animated, flow textures in real time, can handle both stationary and instationary fields defined on domains ranging from planar 2D to volumetric ones, and are quite simple to implement.

We next detail the IBFV method that operates on 2D planar domains, which is also the simplest to implement in its class. The principle of the method is sketched in Figure 6.26. To understand IBFV, consider a time-dependent scalar property \( I : D \times \mathbb{R}_+ \rightarrow \mathbb{R}_+ \) such as the image intensity, defined on a 2D domain