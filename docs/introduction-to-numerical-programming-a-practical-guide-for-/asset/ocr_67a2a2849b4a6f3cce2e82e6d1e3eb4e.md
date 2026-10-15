```
```python
# sig[]  - error bars of the tabulation points (useful for sty == 4)
# n[]    - ending index for the individual plots (nmax = n[nplot])
# col[]  - plot color ("red", "green", "blue" etc.)
# sty[]  - plot style 0 - scatter plot with squares
#                         1 - line plot;  -1 - dashed line
#                         2 - polar plot; -2 - dashed line
#                         3 - drop lines
#                         4 - error bars; -4 - including line plot
# nplot  - number of plots
# maxint - max. number of labeling intervals
# ioptx  - 0 - resize x-axis automatically
#          1 - resize x-axis based on user interval [xminp,xmaxp]
# iopty  - 0 - resize y-axis automatically
#          1 - resize y-axis based on user interval [yminp,ymaxp]
# fxmin  - min fractional x-limit of viewport (0 < fxmin < fxmax < 1)
# fxmax  - max fractional x-limit of viewport
# fymin  - min fractional y-limit of viewport (0 < fymin < fymax < 1)
# fymax  - max fractional y-limit of viewport
# xtext  - x-axis title; for "None" - axis is not labeled
# ytext  - y-axis title; for "None" - axis is not labeled
# title  - plot title

#===============================================================================
def RGBcolors(ncolstep):
#-------------------------------------------------------------------------------
# Generates ncol = 1280/ncolsep RGB colors in icol[1] through icol[ncol]
#
# Returns: icol, ncol

#===============================================================================
def ColorLegend(fmin, fmax, ixmin, ixmax, iymin, iymax):
#-------------------------------------------------------------------------------
# Draws and labels the color legend for the interval [fmin,fmax] in the
# rectangle [ixmin,ixmax] x [iymin,iymax]. [fmin,fmax] is extended to fit at
# most 10 intervals expressible as d * 10^p, with d = 1, 2, 5 and p integer.
#
# Returns: fmin, fmax, icol, ncol, nintv

#===============================================================================
def Contour(z, nx, ny, xmin, xmax, ymin, ymax, zmin, zmax, \
            fxmin, fxmax, fymin, fymax, xtext, ytext, title):
#-------------------------------------------------------------------------------
# Plots a function z(x,y) defined in [xmin,xmax] x [ymin,ymax] and tabulated
# on a regular Cartesian grid with (nx-1)x(ny-1) mesh cells as contour plot.
# The level curves result by inverse linear interpolation inside the cells.
#
# z      - tabulated function values
# nx     - number of x-mesh points
# ny     - number of y-mesh points
# zmin   - minimum level considered
# zmin   - maximum level considered
# fxmin  - minimum relative viewport abscissa (0 < fxmin < fxmax < 1)
# fxmax  - maximum relative viewport abscissa
# fymin  - minimum relative viewport ordinate (0 < fymin < fymax < 1)
# fymax  - maximum relative viewport ordinate
# xtext  - x-axis title; xtext = "" - axis is not labeled
# ytext  - y-axis title; ytext = "" - axis is not labeled
# title  - plot title
```
```