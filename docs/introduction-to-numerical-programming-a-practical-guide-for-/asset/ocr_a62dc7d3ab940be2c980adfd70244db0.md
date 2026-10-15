```
f = 0e0                                      # npar = multiple of 3
for i in range(1,npar+1,3): f += a[i] * exp(-pow(x-a[i+1],2)/a[i+2])
return f

# main

nfit = 100                                      # number of points plotted from model
nn   = [0]*3                                    # ending indexes of plots
col  = [" "]*3                                 # colors of plots
sty  = [0]*3                                    # styles of plots

inp = open("fit2.dat","r")                    # open data file

line = inp.readline()                            # number of observed data and parameters
n = int(line.split()[0])
npar = int(line.split()[1])

x     = [0]*(n+nfit+1)                           # allocate arrays
                                                # x-coordinates of observed data
y     = [0]*(n+nfit+1)                           # y-coordinates of observed data
sigmy = [0]*(n+1)                                # standard deviations of observed data
a     = [0]*(npar+1)                             # model parameters
sigma = [0]*(npar+1)                             # uncertainties of parameters

iopt = int(inp.readline())                      # initialization option for sigmy[i]
line = inp.readline()
for i in range(1,npar+1): a[i] = float(line.split()[i-1]) # parameter guesses
for i in range(1,n+1):
    line = inp.readline()
    x[i] = float(line.split()[0])                # observed data
    y[i] = float(line.split()[1])
    if (iopt): sigmy[i] = float(line.split()[2]) # uncertainty
inp.close()

out = open("fit.txt","w")                      # open output file
out.write("n = {0:2d}   npar = {1:2d}\\n".format(n,npar))
out.write("Initial parameters:\\n")
for i in range(1,npar+1): out.write("a[{0:d}] = {1:6.3f}\\n".format(i,a[i]))

chi2 = MarqFit(x,y,sigmy,n,iopt,a,sigma,npar,Func)   # Levenberg-Marquardt fit

out.write("\\nFinal parameters:\\n")
for i in range(1,npar+1):
    out.write("a[{0:2d}] = {1:6.3f}  sigma[{2:2d}] = {3:7.1e}\\n".
              format(i,a[i],i,sigma[i]))
out.write("\\nChi^2 = {0:7.1f}\\n".format(chi2))
out.write("\\n     x          y       sigma     yfit     y-yfit\\n")
for i in range(1,n+1):
    yfit = Func(x[i],npar)                      # model values for adjusted parameters
    out.write("{0:2d}{1:10.5f}{2:10.5f}{3:10.5f}{4:10.5f}{5:10.5f}\\n".
              format(i,x[i],y[i],sigmy[i],yfit,y[i]-yfit))
out.close()

GraphInit(800,600)

nn[1] = n     ; col[1] = "red"  ; sty[1] = 4     # prepare plots:
                                                   # observed data
nn[2] = n + nfit; col[2] = "blue"; sty[2] = 1     # fitted model
h = (x[n]-x[1])/(nfit-1)
for i in range(1,nfit+1):
    x[n+i] = x[1] + (i-1)*h                     # append data for 2nd plot
```