width and height of the viewport region (in pixels). We have defined the variables sizeX and sizeY to common dimensions for a modern laptop screen; they should be set to match the machine being used. We then use these values to divide the screen in half, one side for each eye. The resulting output is shown in Figure 17.6. In this example, we have also set the clear color to the fog color, as we did in Program 17.1.

![](bbox=[0.197, 0.257, 0.803, 0.5])

**Figure 17.6**  
Side-by-side rendering of Program 17.2, the fog example.  
(best viewed through a stereo headset)

By comparing Figures 17.5 and 17.6, we can see that the images in 17.6 have clearly been compressed horizontally. With only half of the screen width available for rendering each image, an application would need to take this into account by changing either the field of view or the aspect ratio. We have ignored that in this simple example.

# 17.4 CORRECTING LENS DISTORTION IN HEADSETS

Headsets for viewing side-by-side images utilize high field-of-view lenses that often suffer from lens distortion. Two important types of distortion in lenses are *pincushion distortion*, where objects on the periphery bow outward, and *barrel distortion*, where objects on the periphery bow inwards. Figure 17.7 shows a simple grid, and then the same grid having been distorted with both pincushion and barrel distortions.