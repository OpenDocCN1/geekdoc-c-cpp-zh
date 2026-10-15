![](bbox=[0.12, 0.095, 0.88, 0.49])

# **FIGURE 7.22**

(a) After processing pixel (0, 8).  
(b) After processing pixel (1, 8).  
(c) After processing of pixel (12, 8).  
(d) After processing pixel (13, 8).

a line belongs to the infinite region, it does not belong to the same pixel than its pixel to its left (except for the last line), and it belongs to the same region than the pixel to its up. Thus the edge containing *last* is kept and the edge containing *up* is removed, producing the 2-map shown in (c). Then the vertex containing *last* is removed (cf. (d)). This 2-map is equivalent to the one drawn in (e) due to the folding of the image in a cylinder. Indeed the two points associated with darts *last* and β₁(*last*) have n₁ + 1 as x coordinate. Thanks to the modulo computation (cf. Algorithm 76 line 8), they are moved to x = 0 and to the next line. The obtained configuration, regarding pixel (0, 1), is similar to the initial configuration of the initial border for pixel (0, 0). There is a dart to the up of each pixel of the second line, and a dart to the left of the first pixel. The pixels of the second line can thus be processed. The 2-map obtained after processing of all the pixels of the second line is shown in (f).

The different 2-maps obtained after processing each last pixel of the different lines of the image are shown in Fig. 7.21. The 2-map is progressively built,