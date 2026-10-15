```
w.create_text(ixmax,iymin+10,text="{0:5.2f}".format(xmax),anchor=NE)
w.create_text(ixmin-10,iymin,text="{0:5.2f}".format(ymin),anchor=E)
w.create_text(ixmin-10,iy max,text="{0:5.2f}".format(ymax),anchor=E)

ax = (ixmax-ixmin)/(xmax-xmin)                # x-axis scaling coefficients
bx = ixmin - ax*xmin
ay = (iymax-iy min)/(ymax-ymin)                # y-axis scaling coefficients
by = iymin - ay*ymin

if (xmin*xmax < 0): w.create_line(Nint(bx),iymin,Nint(bx),iymax)   # y-axis
if (ymin*ymax < 0): w.create_line(ixmin,Nint(by),ixmax,Nint(by))   # x-axis

i x0 = Nint(ax*x[1]+bx); iy0 = Nint(ay*y[1]+by)                # 1st point
for i in range(2,n+1):
    ix = Nint(ax*x[i]+bx); iy = Nint(ay*y[i]+by)                # new point
    w.create_line(ix0,iy0,ix,iy,fill=col)                      # draw line
    ix0 = ix; iy0 = iy                                          # save point
```

real functions of one variable. One of the basic ideas is to “hide” the technicalities involved by invoking the Tkinter methods underneath of simple wrapper functions, which should be called instead. Second, to simplify the calling and the argument lists of the graphic functions, context-related variables (such as Tk root object, canvas object, canvas size, etc.) are conveyed between the library’s functions behind the scenes, by global variables. Third, taking advantage of the remarkable portability of Python, the library’s functions are built so as to be readily embeddable in programs written in other languages, such as C++. The embedding technique is applied in Section 3.6.

The module graphlib0.py creates, first of all, the Tk root widget and wraps its mainloop method into the function MainLoop. The whole procedure of creating and packing the Canvas widget is wrapped into the function GraphInit, having as sole arguments the sizes nxwin and nywin of the canvas. These values are copied into the variables nxw and nyw, which are made accessible to all the functions contained in graphlib0.py, by way of global statements. The module also provides a general-purpose function, Nint(x), which returns the nearest integer to its real argument x.

The actual plotting function, Plot0, is based on the simple scaling procedure described above. It receives as a main input the n pairs of coordinates, (x[1],y[1]) through (x[n],y[n]), of the points that sample the function to be plotted. The color to be used for the plot is specified through the parameter col, and the corresponding arguments can be colors specified both in RGB format or by standard names ("red", "green", "blue", etc.).

Instead of passing actual canvas coordinates to Plot0 for positioning the plot onto the display, it is considerably more practical to convey fractional coordinates (comprised between 0 and 1). Indeed, while absolute coordinates produce different layouts on canvasses of different sizes, fractional coordinates are size independent. In addition, fractional coordinates also enable an intuitive positioning of several plots onto the same canvas. In fact, the parameters fxmin and fxmax specify, respectively, the minimum and maximum fractional limits of the x-interval of canvas coordinates, that is x~min/nx and x~max/nx. Similarly, fymin and fymax indicate, respectively, the minimum and maximum fractional canvas coordinates, y~min and y~max. Finally, the list of parameters of Plot0 contains titles for the x-axis (xt ext), y-axis (ytext), and the whole plot (title).

The routine Plot0 starts by determining the minima and maxima of the x and y user coordinates (xmin, xmax, ymin, and ymax). All operations concern, as mentioned, only the components of x[] and y[] indexed from 1 to n. On the basis of the bounding user coordinates, the corresponding absolute canvas coordinates are determined (ixmin, ixmax, iymin, and iymax). This is done by simply multiplying the fractional canvas coordinates (fxmin, fxmax, fymin, and fymax) with the absolute