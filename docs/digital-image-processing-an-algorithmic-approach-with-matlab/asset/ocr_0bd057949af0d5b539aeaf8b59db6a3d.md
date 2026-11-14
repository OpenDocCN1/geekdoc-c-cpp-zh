```
z6 = bwmorph(x1,'thicken') ;
figure ; imshow(y6)
figure ; imshow(z6)
```

```
% Skeletonization
y7 = bwmorph(xb,'skel',20) ;
z7 = bwmorph(x1,'skel') ;
figure ; imshow(y7)
figure ; imshow(z7)
```

# 10.11 SUMMARY

+   - Binary image processing essentially means operations that can modify the black-and-white content of an image.
+   - In some cases, the foreground pixels (with white color) are increased, whereas in other cases the background pixels (with black color) are increased.
+   - The processing involving such changes is called a _morphological operation_.
+   - The morphological operators dilation, closing, and thickening will increase the foreground content but in slightly varying degrees.
+   - Similarly, the morphological operators erosion, opening, and thinning will increase the background content but in varying degrees.
+   - If erosion is applied iteratively, keep in mind to avoid an opening or hole formation in the foreground objects, then it will converge to a final and most simplified connected version of the source image that is called the _skeleton_ of the image.
+   - Morphological operations are extremely useful in isolating certain regions of interest of the image for further processing, or in removing or increasing certain types of pixels in certain neighborhoods, or in getting the skeleton of the objects present in the image.

# 10.12 EXERCISES

+   1. In the usual erosion operation, the strel is moved pixel by pixel as in convolutional shifting. Modify this procedure for the nonoverlapping mode of erosion, in which the mask is shifted to a new location on the image with overlapping with any other previously used