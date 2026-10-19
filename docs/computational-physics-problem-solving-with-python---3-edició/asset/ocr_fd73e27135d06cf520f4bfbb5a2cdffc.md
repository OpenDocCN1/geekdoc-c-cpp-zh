![](bbox=[0.14, 0.09, 0.7, 0.33])

Figure 16.1 (a) A statistical fractal Sierpiński gasket containing 10 000 points. Note the self-similarity at different scales. (b) A geometric Sierpiński gasket constructed by successively connecting the midpoints of the sides of each equilateral triangle. The first three steps in the process are labeled as A, B, C.

can have the computer do the counting by defining an array *box* of all 0 values and then change a 0 to a 1 when a dot is placed there.)

# 16.2.2
Assessing Fractal Dimension

The topology in Figure 16.1 was first analyzed by the Polish mathematician Sierpiński. Observe that there is the same structure in a small region as there is in the entire figure. In other words, if the figure had infinite resolution, any part of the figure could be scaled up in size and would be similar to the whole. This property is called *self-similarity*.

We construct a nonstatistical form of the Sierpiński gasket by removing an inverted equilateral triangle from the center of all filled equilateral triangles to create the next figure (Figure 16.1b). We then repeat the process ad infinitum, scaling up the triangles so each one has side *r* = 1 after each step. To see what is unusual about this type of object, we look at how its density (mass/area) changes with size, and then apply (16.2) to determine its fractal dimension. Assume that each triangle has mass *m* and assign unit density to the single triangle:

$$\rho(L=r)\propto\frac{M}{r^2}=\frac{m}{r^2}\mathrel{\mathop:^{\rm def}}\rho_0 \qquad \text{(Figure 16.1b-A).} \tag{16.5}$$

Next, for the equilateral triangle with side $L=2$, the density is

$$\rho(L=2r)\propto\frac{M=3m}{(2r)^2}=\frac{3}{4}mr^2=\frac{3}{4}\rho_0 \qquad \text{(Figure 16.1b-B).} \tag{16.6}$$