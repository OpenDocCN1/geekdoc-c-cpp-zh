Then, you can plot the corresponding sampling distribution using this code:

```
R> pvals <- seq(p.hat-5*p.se,p.hat+5*p.se,length=100)
R> p.samp <- dnorm(pvals,mean=p.hat,sd=p.se)
R> plot(pvals,p.samp,type="l",xlab="",ylab="",
    xlim=p.hat+c(-4,4)*p.se,ylim=c(0,max(p.samp)))
R> abline(h=0,col="gray")
```

Figure 17-2 gives the result.

![](bbox=[0.23, 0.27, 0.65, 0.57])

Figure 17-2: Visualizing the sampling distribution for the voting example as per Equation (17.1). The shaded area represents Pr(0.7 < P̂ < 0.75), which is the probability that the true sample proportion for samples of size n = 118 lies between 0.7 and 0.75.

Now you can use this distribution to describe the variability in the sample proportion of voters who already know how they will vote, for other samples of this size.

For example, the shaded area in Figure 17-2 highlights the probability that in another sample of the same size, the sample proportion of voters in the given city who already know how they’re going to vote is somewhere between 0.7 and 0.75. This shaded area can be added with the following code:

```
R> pvals.sub <- pvals[pvals>=0.7 & pvals<=0.75]
R> p.samp.sub <- p.samp[pvals>=0.7 & pvals<=0.75]
R> polygon(cbind(c(0.7,pvals.sub,0.75),c(0,p.samp.sub,0)),
    border=NA,col="gray")
```