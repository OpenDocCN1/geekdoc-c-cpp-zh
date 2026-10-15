```
```python
out.write("{0:10.5f}{1:10.5f}\n".format(s,sigma))
x1[np+ip] =       n ; y1[np+ip] = s
x2[np+ip] = log10(n); y2[np+ip] = log10(sigma)

out.close()

                                      # linear regression
(a, b, sigma, sigmb, chi2) = LinFit(x2[0:],y2[0:],sig,np,0)
print("sigma = {0:6.3f} n**{1:6.3f}  w(x) = 1".format(pow(10e0,b),a))

(a, b, sigma, sigmb, chi2) = LinFit(x2[np:],y2[np:],sig,np,0)
print("sigma = {0:6.3f} n**{1:6.3f}  w(x) = exp(-x)". \\
      format(pow(10e0,b),a))

GraphInit(1200,600)

nn[1] =   np; col[1] = "blue"; sty[1] = 0             # uniform sampling
nn[2] = 2*np; col[2] = "red";  sty[2] = 0             # importance sampling
MultiPlot(x1,y1,nn,col,sty,2,10,0e0,0e0,0e0,0e0,0,
          0.10,0.45,0.15,0.85,"n","Int","Monte Carlo - integral")

MultiPlot(x2,y2,y2,nn,col,sty,2,10,0e0,0e0,0e0,0e0,0,
          0.60,0.95,0.15,0.85,"log(n)","log(sig)",
          "Monte Carlo - standard deviation")

MainLoop()
```
```

![](bbox=[0.141, 0.486, 0.857, 0.746])

**FIGURE 11.7** Monte Carlo estimates of integral 11.42 (left panel) and associated standard deviations (right panel) using uniform and, respectively, exponential sampling.

# PROBLEM 11.2

Consider the 2D integral:

$$\frac{1}{4\pi}\int_{-\infty}^{\infty}\int_{-\infty}^{\infty}(x^2+y^2)e^{-(x^2+y^2)/2}\,dy\,dx. \tag{11.44}$$