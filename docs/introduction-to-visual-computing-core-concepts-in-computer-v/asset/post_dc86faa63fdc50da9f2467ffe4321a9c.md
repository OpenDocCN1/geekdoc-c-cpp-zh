
vertical ranges of the bounding box of A are completely within the respective ranges of the window. So A is inside the window. In case of D, while the vertical range of the bounding box intersects that of the window, the horizontal range of the bounding box is completely outside that of the window. So D lies outside the window. For the other two cases, both the horizontal and vertical ranges of the bounding box and that of the window partially intersect leading to possible intersection of the primitive with the window. The primitive B intersects the window and will be clipped via intersection computation. However, there can be cases like C where the bounding box intersects though the triangle does not. The actual intersection computation in such cases will yield negative results.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_323_0.png)

Using Logic Operations: Another technique to expedite acceptance/rejection tests is to divide the 2D image plane into regions and assign binary codes to the regions. For example, we can have four bits, b1b2b3b4 associated with each projected vertex (x, y) such that b1 = y < tw, b2 = y > bw, b3 = x > rw, and b4 = x < lw. The four-bit code divides the image plane into nine different regions, each with a unique code (shown by green codes in Figure 13.7). Consider the four bit codes of two end points of a line segment. If the bitwise AND of these two codes is not zero, then both end points are outside the same window boundary and the line is completely outside the window and therefore rejected. If each of the two codes is zero then the line segment is inside the window and therefore accepted. If at least one of the two codes is not zero, but the AND operation of the two codes is zero, then the line intersects with the boundary of the window and therefore an accurate intersection test has to be performed. Such logic operations can be extended to triangles also to efficiently clip them. An acceptance or rejection test using logic operations is equivalent to, yet simpler than, the test using a bounding box.

Figure 13.7. This figure illustrates some of the efficiency improvements in clipping algorithms using bounding boxes or binary codes.

Using Integer Operations: Intersection of the lines and triangles that are not trivially accepted/rejected with the window boundaries have to be computed. For this we first find the window boundary that intersects the primitive and then find the exact intersection. For both of these steps, it is far more efficient if they can be achieved primarily via integer computation rather than floating point computation. Let us consider the red and green lines shown in Figure 13.8. The green line intersects the left window boundary before the top. This indicates that the line is entering the window at the left boundary. But, the red line meets the top boundary before left that can only happen when the line is completely outside the window and should be rejected. Therefore, to figure out which boundary intersection computation needs to be performed, it may be useful to find the parametric value α of the line intersection with different window boundaries. Denoting the alpha boundaries by α_l, α_r, α_t and α_b for the left, right, top and bottom boundary and simply ordering these parametric values we can find the portion of the line that is inside the window. However, computing these parametric values involve floating point operation. So, the next question is how can we make these operations more efficient?

![](img/66c45bbed85bb7ba7f7b05dff49b5060_324_0.png)

Figure 13.8. This figure shows the computation of which boundaries to intersect with using integer computations.

Consider a line given by two points defined by integers (x1, y1) and (x2, y2) where x1 < x2 and y1 < y2 (assuming the bottom left corner of the screen to be origin). We know

α_t = (t − y1)/(y2 − y1) (13.38)

α_l = (l − x1)/(x2 − x1) (13.39)

If α_t < α_l, i.e.

(t − y1)/(y2 − y1) < (l − x1)/(x2 − x1), (13.40)

the line should be rejected. Instead of carrying this test on the floating point numbers α_l and α_t, the same results can be obtained if we derive the decision factor from Equation 13.40 to be

(l − x1)(y2 − y1) < (t − y1)(x2 − x1). (13.41)

The advantage of Equation 13.41 is that it is completely in integers and does not involve any floating point computation. The methods of clipping are fraught with such techniques to avoid floating point computation thereby making the pipeline extremely efficient.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_328_0.png)

**Figure 13.10.** This figure illustrates the process of polygon rasterization (left) and shows a rasterized triangle with interpolated gray scale values (right).

intersections sorted in the increasing order of their *x* (note all of them have the same *y* since we are dealing with a horizontal scanline). Consider the two triangles in Figure 13.10 and the black scanline. The intersection points when ordered will be p₀, p₁, p₂, p₃. Next, the pixels within pairs of their intersections are filled up. Therefore, p₀ to p₁ and p₂ to p₃ is filled up. When filling up these pixels, their color and depth are also interpolated. For every pixel on a scanline that has been detected to be inside the triangle, first its reciprocal of depth is interpolated from the reciprocal of the depths stored at the intersection points of the scanline and the edges. If the interpolated value is larger than the existing value at that pixel in the *Z*-buffer (i.e. depth is smaller), only then the framebuffer is updated at that pixel with the interpolated color. Otherwise, this pixel is occluded and is not drawn in the framebuffer.

The polygon rasterization is also made efficient by several measures like incrementally updating the intersection of a polygon edge with a scan line by using the results with the previous scanline and the slope of the edge thereby avoiding computation of the intersections anew for every scanline. Several data structures are used to reduce computation. For example, the extent of the scanlines that a triangle spans (shown using red and orange dotted lines in Figure 13.10) can be maintained so that only the triangles whose span includes the scanline under consideration are included in the processing for that scan line. Other more complicated data structures like edge table (that is a bucket sort of edges bucketed by scanlines) are used. Several improvements are also achieved by using integer computation as much of the process as possible. Details of such processes are available in most traditional computer graphics books. The final rasterized polygon painted with interpolated color or gray values is shown in Figure 13.10.

## 13.4 Conclusion

We learnt about the interactive graphics pipeline in this chapter. We have deliberately kept this treatise API independent and given you the fundamental concepts. We hope that following this you can adapt API specific aspects into the pipeline easily. For example, OpenGL assumes the normal to the image plane in the view set-up to be negative Z. This means the view transformation and the perspective transformation will change slightly and we hope you can work through it. In this chapter we have not given you details about clipping and rasterization methods assuming they will be done in the graphics hardware. To learn more about such techniques, please look up [Foley et al. 90, Shirley and Marschner 09, Watt 99].

## Bibliography

- [Foley et al. 90] James D. Foley, Andries van Dam, Steven K. Feiner, and John F. Hughes. *Computer Graphics: Principles and Practice (2nd Ed.).* Boston, MA, USA: Addison-Wesley Longman Publishing Co., Inc., 1990.
- [Shirley and Marschner 09] Peter Shirley and Steve Marschner. *Fundamentals of Computer Graphics.* A. K. Peters, Ltd., 2009.
- [Watt 99] Alan Watt. *3D Computer Graphics.* Addison Wesley, 1999.
