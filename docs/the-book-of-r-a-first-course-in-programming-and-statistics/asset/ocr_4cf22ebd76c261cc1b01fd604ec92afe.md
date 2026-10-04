If you’re working in degrees, then technically 0 ≤ θ < 360; to convert to radians, you must multiply by π/180 such that 0 ≤ θ < 2π.

To draw a circle based on the equations in (26.1), first decide on a radius, then decide on a center point, and then generate the corresponding values of x and y. Consider the following code:

```
R> radius <- 3
R> a <- 1
R> b <- -4.4
R> angle <- 0:360*(pi/180)
R> x <- a+radius*cos(angle)
R> y <- b+radius*sin(angle)
R> plot(x,y,ann=FALSE)
R> abline(v=a)
R> abline(h=b)
```

The circle will have a radius of 3 and be centered at (1,−4.4). Given the sequence defined as angle, note the plot will place a point at each integer angle from 0 to 360 degrees—I’ve allowed the upper limit to be equal to exactly 360 to fully complete the rotation—after which you convert to radians (with multiplication by π/180) in order to use the built-in R functions cos and sin. The geometric value of pi (π = 3.1415…) is held within the ready-to-use R object pi (see the help file ?constants). The last three lines execute the plot, shown in Figure 26-16.

![](bbox=[0.25, 0.55, 0.67, 0.84])

Figure 26-16: Drawing a 2D circle in R with center (1,−4.4) and radius 3, following the relevant parametric equations of the locus