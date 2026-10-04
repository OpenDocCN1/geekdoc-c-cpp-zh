![](bbox=[0.238, 0.076, 0.693, 0.365])

Figure 20-3: The student height regression example, with a fitted regression line and point estimates at x = 14.5 and x = 24 and with corresponding 95 percent Clis (black vertical lines) and Plis (gray vertical lines). The dashed black and gray lines lines provide95 percent confidence and prediction bands for the response variable over the visible range of x values.

In R, this requires you to rerun the command as follows:

```
R> xseq <- data.frame(Wr.Hnd=seq(12,25,length=100))
R> ci.band <- predict(surfit,newata=xseq,interval="confidence",level=0.95)
R> pi.band <- predict(surfit,newata=xseq,interval="prediction",level=0.95)
```

The first line in this code creates the sequence of predictor values and stores it in the format required by the newata argument. The y-axis coordinates for CI and PI bands are stored as the second and third columns of the matrix objects. Finally, lines is used to add each of the four dashed lines corresponding to the upper and lower limits of the response, and a legend adds a final touch.

```
R> lines(xseq[1],ci.band[2],lty=2)
R> lines(xseq[1],ci.band[3],lty=2)
R> lines(xseq[1],pi.band[2],lty=2,col="gray"
R> lines(xseq[1],pi.band[3],lty=2,col="gray"
R> legend("topleft","95% CI","95% PI",lty=c(1,2,2),col=c("black","black","gray"),lwd=c(2,1,1))
```

Note that the dashed CI band meets the black vertical lines and the gray dashed PI bands meet the vertical lines for the two individual x values from earlier, just as you'd expect.