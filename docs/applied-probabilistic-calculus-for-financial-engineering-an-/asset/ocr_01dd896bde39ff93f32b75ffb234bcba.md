```
> legend("topleft",c("real data","mean path",paste("bound of",
+ 95,"percent confidence")),
+ inset = .01,col=2:4,lwd=2,cex=0.8)
> # Output: Figure 2.22 Irates=10
> 
```

![](bbox=[0.18, 0.27, 0.62, 0.62])

Figure 2.22 Irates=10: Legend added for real data, mean path, and upper and lower bounds of 95% confidence levels (Ordinates are arbitrary).

# Review Questions and Exercises

+   1. Define differential calculus.
+      a. Define Ito calculus.
+      b. What are the essential differences between these two concepts? Explain
+   2. a. Why is the Ito calculus suitable for analyzing GBM (Geometric Brown motion)?
+      b. i) What are the advantages of using Ito calculus in this application?
+         ii) What are the disadvantages? Any limitations?
+   3. GBM: Let Y be a normal N(0, 1) function, then the process X_t = Y√t is continuous, and is marginally distributed as a normal N(0, t).
+      Is X_t a Brownian motion? Explain.