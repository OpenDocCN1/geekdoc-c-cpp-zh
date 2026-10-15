
![](img/5c6c126e3d8cf2b3029f4242e9ad2887_60_0.png)

**FIGURE 3.6** There exists a *linear correspondence* between the user coordinates $(x_i,y_i)$ (on the left) and the *canvas coordinates* $(\bar{x}_i,\bar{y}_i)$ (on the right).

Considering, in particular for the $x$-axis, that the limits $x_{\min}$ and $x_{\max}$ of the user domain can be determined from the set of arguments $x_i$, and that the limits $\bar{x}_{\min}$ and $\bar{x}_{\max}$ of the canvas domain are set independently, in accordance with the desired positioning of the plot, the scaling coefficients $A_x$ and $B_x$ can be determined from the linear conditions:

$$\bar{x}_{\min}=A_xx_{\min}+B_x,$$

$$\bar{x}_{\max}=A_xx_{\max}+B_x,$$

wherefrom, the scaling coefficients for the $x$-axis are

$$A_x=(\bar{x}_{\max}-\bar{x}_{\min})/(x_{\max}-x_{\min})$$

$$B_x=\bar{x}_{\min}-A_xx_{\max}.$$ 

(3.1)

Analogously, the scaling coefficients $A_y$ and $B_y$ for the $y$-axis are given by

$$A_y=(\bar{y}_{\max}-\bar{y}_{\min})/(y_{\max}-y_{\min})$$

$$B_y=\bar{y}_{\min}-A_yy_{\min}.$$ 

(3.2)

There exists, though, a lack of symmetry between the $x$- and $y$-axes. This difference stems, on the one hand, from the fact that, while the set of arguments $x_i$ is supposed to be ascendingly ordered, with $x_{\min}$ and $x_{\max}$ coinciding, respectively, with $x_1$ and $x_n$, the set of ordinates $y_i$ is not necessarily ordered (except for the case of monotonic functions), and hence, the limiting values $y_{\min}$ and $y_{\max}$ have to be explicitly determined. On the other hand, since the vertical axes in user and canvas coordinates have opposite directions, ascending canvas $y$-coordinates actually decrease (down to $0$) for increasing $y$-coordinates.

With the scaling coefficients given by Equations 3.1 and 3.2, the canvas coordinates corresponding to the $n$-tabulated function values are determined from the relations:

$$\bar{x}_i=A_xx_i+B_x,\quad i=1,2,\ldots,n$$

$$\bar{y}_i=A_yy_i+B_y.$$

The minimal Python graphics library `graphlib0.py` presented in Listing 3.7 is meant to illustrate the basic concepts underlying scientific graphics, by providing elementary functionalities for plotting

## Listing 3.7 Minimal Python Library for Plotting Functions (graphlib0.py)

```
#------------------------------------------------------------------- graphlib0.py --------------------------------
# Graphics library based on Tkinter
#-------------------------------------------------------------------
from math import *
from tkinter import *

root = Tk()                                      # create Tk root widget
root.title("graphlib0 v1.0")

#===================================================================
def MainLoop():                                 # creates Tk event loop
    root.mainloop()

#===================================================================
def GraphInit(nxwin, nywin):       # creates Canvas widget and returns object
    global w, nxw, nyw                     # make canvas object available

    nxw = nxwin; nyw = nywin                       # canvas size
    w = Canvas(root, width=nxw, height=nyw, bg = "white")   # create canvas
    w.pack()                                       # make canvas visible
    return w

def Nint(x): return int(floor(x + 0.5))                 # nearest integer

#===================================================================
def Plot0(x, y, n, col, fxmin, fxmax, fymin, fymax, xtext, ytext, title):
#-------------------------------------------------------------------
# Plots a real function of one variable specified by a set of (x,y) points.
#
# x[]  - abscissas of tabulation points (x[1] through x[n])
# y[]  - ordinates of tabulation points (y[1] through y[n])
# n    - number of tabulation points
# col  - plot color ("red", "green", "blue" etc.)
# fxmin - min fractional x-limit of viewport (0 < fxmin < fxmax < 1)
# fxmax - max fractional x-limit of viewport
# fymin - min fractional y-limit of viewport (0 < fymin < fymax < 1)
# fymax - max fractional y-limit of viewport
# xtext - x-axis title
# ytext - y-axis title
# title - plot title
#-------------------------------------------------------------------
    global w, nxw, nyw                           # canvas object and size

    xmin = min(x[1:n+1]); xmax = max(x[1:n+1])           # user domain limits
    ymin = min(y[1:n+1]); ymax = max(y[1:n+1])
                                                   # corrections for horizontal plots
    if (ymin == 0.0 and ymax == 0.0): ymin = -1e0; ymax = 1e0
    if (ymin == ymax): ymin *= 0.9; ymax *= 1.1

    ixmin = Nint(fxmin*nxw); iymin = Nint((1e0-fymin)*nyw)   # canvas domain
    ixmax = Nint(fxmax*nxw); iymax = Nint((1e0-fymax)*nyw)
    w.create_rectangle(ixmin,iymax,ixmax,iymin)            # draw plot frame

    w.create_text((ixmin+ixmax)/2,iymin+10,text=xtext,anchor=N) # x-axis title
    w.create_text(ixmin-10,(iymin+iymax)/2,text=ytext,anchor=E) # y-axis title
    w.create_text((ixmin+ixmax)/2,iymax-10,text=title,anchor=S) # plot title
                                                   # labels axes ends
    w.create_text(ixmin,iymin+10,text="{0:5.2f}".format(xmin),anchor=NW)
```

```
w.create_text(ixmax,iymin+10,text="{0:5.2f}".format(xmax),anchor=NE)
w.create_text(ixmin-10,iymin,text="{0:5.2f}".format(ymin),anchor=E)
w.create_text(ixmin-10,iymax,text="{0:5.2f}".format(ymax),anchor=E)

ax = (ixmax-ixmin)/(xmax-xmin)                # x-axis scaling coefficients
bx = ixmin - ax*xmin
ay = (iymax-iymin)/(ymax-ymin)                # y-axis scaling coefficients
by = iymin - ay*ymin

if (xmin*xmax < 0): w.create_line(Nint(bx),iymin,Nint(bx),iymax)   # y-axis
if (ymin*ymax < 0): w.create_line(ixmin,Nint(by),ixmax,Nint(by))   # x-axis

ix0 = Nint(ax*x[1]+bx); iy0 = Nint(ay*y[1]+by)                # 1st point
for i in range(2,n+1):
    ix = Nint(ax*x[i]+bx); iy = Nint(ay*y[i]+by)                # new point
    w.create_line(ix0,iy0,ix,iy,fill=col)                      # draw line
    ix0 = ix; iy0 = iy                                          # save point
```

real functions of one variable. One of the basic ideas is to “hide” the technicalities involved by invoking the Tkinter methods underneath of simple wrapper functions, which should be called instead. Second, to simplify the calling and the argument lists of the graphic functions, context-related variables (such as Tk root object, canvas object, canvas size, etc.) are conveyed between the library’s functions behind the scenes, by global variables. Third, taking advantage of the remarkable portability of Python, the library’s functions are built so as to be readily embeddable in programs written in other languages, such as C++. The embedding technique is applied in Section 3.6.

The module graphlib0.py creates, first of all, the Tk root widget and wraps its mainloop method into the function MainLoop. The whole procedure of creating and packing the Canvas widget is wrapped into the function GraphInit, having as sole arguments the sizes nxwin and nywin of the canvas. These values are copied into the variables nxw and nyw, which are made accessible to all the functions contained in graphlib0.py, by way of global statements. The module also provides a general-purpose function, Nint(x), which returns the nearest integer to its real argument x.

The actual plotting function, Plot0, is based on the simple scaling procedure described above. It receives as a main input the n pairs of coordinates, (x[1],y[1]) through (x[n],y[n]), of the points that sample the function to be plotted. The color to be used for the plot is specified through the parameter col, and the corresponding arguments can be colors specified both in RGB format or by standard names ("red", "green", "blue", etc.).

Instead of passing actual canvas coordinates to Plot0 for positioning the plot onto the display, it is considerably more practical to convey fractional coordinates (comprised between 0 and 1). Indeed, while absolute coordinates produce different layouts on canvasses of different sizes, fractional coordinates are size independent. In addition, fractional coordinates also enable an intuitive positioning of several plots onto the same canvas. In fact, the parameters fxmin and fxmax specify, respectively, the minimum and maximum fractional limits of the x-interval of canvas coordinates, that is x~min/nx and x~max/nx. Similarly, fymin and fymax indicate, respectively, the minimum and maximum fractional canvas coordinates, y~min and y~max. Finally, the list of parameters of Plot0 contains titles for the x-axis (xtext), y-axis (ytext), and the whole plot (title).

The routine Plot0 starts by determining the minima and maxima of the x and y user coordinates (xmin, xmax, ymin, and ymax). All operations concern, as mentioned, only the components of x[] and y[] indexed from 1 to n. On the basis of the bounding user coordinates, the corresponding absolute canvas coordinates are determined (ixmin, ixmax, iymin, and iymax). This is done by simply multiplying the fractional canvas coordinates (fxmin, fxmax, fymin, and fymax) with the absolute
