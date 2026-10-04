# some different fonts

![](bbox=[0.247, 0.115, 0.752, 0.351])

Figure 23-11: Displaying fonts through use of the family and font graphical parameters

# 23.5.2 Greek Symbols

For statistically or mathematically technical plots, annotation occasionally require Greek symbols or mathematical markup. You can display these using the expression function, which among other things, is capable of invoking the plotmath of R (Murrell and Ihaka, 2000; Murrell, 2011). Use of expression returns a special object that has a class of the same name and can subsequently be passed to any argument in a plotting function that requires the character string to be displayed.

Focusing for the moment on Greek symbols, consider Figure 23-12, which is produced with the following code:

```
R par(mar=c(3,3,3,3))
R plot(1,1,type="n",xlim=(-1,1),ylim=c(0.5,4.5),xaxt="n",yaxt="n"
    ann=FALSE)
R text(0,4,label=expression(alpha),cex=1.5)
R text(0,3,label=expression(paste("sigma", "sigma", Sigma = "Sigma",
family="mono", cex=1.5))
R text(0,2,label=expression(paste("beta", "gamma", "Phi")),cex=1.5)
R text(0,1,label=expression(paste(Gamma,(",tau,") = 24 when ",tau,") = 5\)),
family="serif", cex=1.5)
R title(main=expression(paste("Gr",epsilon,epsilon, "k")),cex.main=2)
```