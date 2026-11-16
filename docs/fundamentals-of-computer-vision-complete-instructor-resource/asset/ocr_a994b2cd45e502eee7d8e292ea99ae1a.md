![](bbox=[0.09, 0.11, 0.88, 0.32])

Figure 12.9 Two images, taken from the same point, but with rotation about the Y axis, and slight rotation about the Z axis. The authors are grateful to Junyi Liu for this figure.

You now have an 8-element vector

```
h = [h1, h2, h3, h4, h5, h6, h7, h8]^T
```

Construct the 3 x 3 matrix

```
H = [[h1, h2, h3], [h4, h5, h6], [h7, h8, 1.0]]
```

The matrix H satisfies x' = Hx. Thus, for any point x in image i, Hx will be the corresponding point in image i.

Once you have H, you can copy an image into the coordinates of another image. So for every point in Ii, find its coordinates in Ii' and copy the pixel from Ii to Ii'. Note that you will need to make Ii' bigger since many of the points of Ii will fall outside of the original Ii'.

As shown in the right-hand image, you are very likely have the same problem with black dots (which we call "interpolating in reverse") that you had in a previous homework. If this is a problem, instead of copying from Ii to Ii' using H, that is, scanning over the input image, and figuring out where it goes in the output, instead copy from Ii' to Ii using H^-1 scanning over the output image, and figuring out where it came from in the input.

If your two images fit together reasonably well, congratulations! You now can do image stitching.

An example of image stitching is presented in Figures 12.9 and 12.10.