are matched to the ellipse. These optional arguments are then passed to the function to be used by various methods that tweak graphical parameters.

Ellipses are a convenient programming tool for writing variadic functions or functions where an unknown number of arguments may be supplied. This will become clearer when you start writing your own functions in Chapter 11. However, when writing functions like this, it is important to properly document the intended use of ... so the potential users of the function know exactly which arguments can be passed to it and what arguments are subsequently used for execution.

# Exercise 9.2

+   a. Use positional matching with seq to create a sequence of values between -4 and 4 that progresses in steps of 0.2.

+   b. In each of the following lines of code, identify which style of argument matching is being used: exact, partial,, or mixed. If mixed, identify which arguments are specified in each style.
   i. array(8:1,dim=c(2,2,2))
   ii. rep(1:2,3)
   iii. seq(from=10,to=8,length=5)
   iv. sort(decreasing=T,x<c(2,1,1,2,0,3,1,3,3))
   v. which(matrix(c(T,F,T,F),2,2))
   vi. which(matrix(c(T,F,T,T),2,2))=T=1

+   c. Suppose you explicitly ran the plotting function plot.default and supplied values to arguments tagged type, pch, xlab, ylab, lwd, lty, and col. Use the function documentation to determine which of these arguments fall under the umbrella of the ellipse.

# Important Code in this Chapter

| Function/operator | Brief description | First occurrence |
|---|---|-|
| ls | Inspect environment objects | Section 9.1.1, p. 167 |
| search | Current search path | Section 9.1.2, p. 168 |
| environment | Function environment properties | Section 9.1.2, p. 169 |
| rm | Delete objects in workspace | Section 9.1.3, p. 171 |
| args | Show function arguments | Section 9.2.3, p. 174 |