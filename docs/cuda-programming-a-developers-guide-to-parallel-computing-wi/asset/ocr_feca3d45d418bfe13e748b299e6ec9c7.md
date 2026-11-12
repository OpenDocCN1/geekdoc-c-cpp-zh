![](bbox=[0.13, 0.11, 0.89, 0.45])

FIGURE 1.7 GPUs compared to a cluster.

applications. Distributed applications run on many nodes, each of which may contain many processing elements including GPUs. Distributed applications may, but do not need to, run in a controlled environment of a managed cluster. They can connect arbitrary machines together to work on some common problem, BOINC and Folding@Home being two of the largest examples of such applications that connect machines together over the Internet.

# THE EARLY DAYS OF GPGPU CODING

Graphics processing units (GPUs) are devices present in most modern PCs. They provide a number of basic operations to the CPU, such as rendering an image in memory and then displaying that image onto the screen. A GPU will typically process a complex set of polygons, a map of the scene to be rendered. It then applies textures to the polygons and then performs shading and lighting calculations. The NVIDIA 5000 series cards brought for the first time photorealistic effects, such as shown in the Dawn Fairy demo from 2003.

Have a look at http://www.nvidia.com/object/cool_stuff.html#demos and download some of the older demos and you'll see just how much GPUs have evolved over the past decade. See Table 1.2.

One of the important steps was the development of programmable shaders. These were effectively little programs that the GPU ran to calculate different effects. No longer was the rendering fixed in the GPU; through downloadable shaders, it could be manipulated. This was the first evolution of general-