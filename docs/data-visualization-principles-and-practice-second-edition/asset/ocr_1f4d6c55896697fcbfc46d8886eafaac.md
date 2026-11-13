![](bbox=[0.41, 0.12, 0.71, 0.32])

Figure 9.10. Connected components.

the test image[i][j] != FOREGROUND in floodFill can be more efficiently executed before pushing each new element on the stack than when popping it. This can significantly decrease the stack size.

After the function connectedComponents returns, the array comp contains every pixel marked by the nonnegative identifier of its connected component or the BACKGROUND value. Figure 9.10 shows the connected components for the segmented bone structures shown in Figure 9.8(c). Each component is color-coded by a different hue. We can now easily distinguish the largest component, marked in red, which corresponds to the cranial bone. If desired, we can now filter the components based on size. For this, we count the number of pixels in every connected component, e.g., using a scan-line traversal of the image or a flood fill from the first pixel belonging to that component, and next mark components whose size is below the desired threshold by the BACKGROUND value. Removing small connected components is also known as island removal [Schroeder et al. 06].

# 9.4.4 Morphological Operations

As we saw in the previous section, computing connected components and eventually removing the small ones that correspond to discretization noise is a powerful tool for extracting shape information from image data. However, noise can have another unpleasant effect that is not addressed by the small-size component removal. Figure 9.11 illustrates this. In this application, scientists are interested in studying the growth of the rice plant roots. The roots, grown in a half-transparent jelly, are photographed. The results (Figure 9.11(a)) needs to be analyzed in order to assess various root characteristics, such as number of branches, length of the main branches, and average length of the small branches.