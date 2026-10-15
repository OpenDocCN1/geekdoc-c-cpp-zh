```
#================================================================================
def Contour(z, nx, ny, xmin, xmax, ymin, ymax, zmin, zmax, \
            fxmin, fxmax, fymin, fymax, xtext, ytext, title):
#--------------------------------------------------------------------------------
# Plots a function z(x,y) defined in [xmin,xmax] x [ymin,ymax] and tabulated
# on a regular Cartesian grid with (nx-1)x(ny-1) mesh cells as contour plot.
# The level curves result by inverse linear interpolation inside the cells.
#
# z       - tabulated function values
# nx      - number of x-mesh points
# ny      - number of y-mesh points
# zmin    - minimum level considered
# zmax    - maximum level considered
# fxmin   - minimum relative viewport abscissa (0 < fxmin < fxmax < 1)
# fxmax   - maximum relative viewport abscissa
# fymin   - minimum relative viewport ordinate (0 < fymin < fymax < 1)
# fymax   - maximum relative viewport ordinate
# xtext   - x-axis title; xtext = "" - axis is not labeled
# ytext   - y-axis title; ytext = "" - axis is not labeled
# title   - plot title
#--------------------------------------------------------------------------------
    global w, nxw, nyw                         # canvas object and size
    xg = [0]*8; yg = [0]*8

    ixmin = Nint(fxmin*nxw); iymin = Nint((1e0-fymin)*nyw)   # viewport coords
    ixmax = Nint(fxmax*nxw); iymax = Nint((1e0-fymax)*nyw)

    f = (xmax-xmin)/(ymax-ymin)                     # scale viewport proportionally
    if (f < float(ixmax-ixmin)/(iymin-iymax)):
        # shorter x-axis
        ixmax = ixmin + ixmax                       # correct ixmin and ixmax
        ixmin = int(0.5e0*(ixmax + (iymax-iymin)*f))
        ixmax = ixmax - ixmin
    else:
        # shorter y-axis
        iymax = iymin + iymax                       # correct iymin and iymax
        iymin = int(0.5e0*(iymax + (ixmax-ixmin)/f))
        iymax = iymax - iymin

    nfont = min(int((ixmax-ixmin)/60.) + 3,12)          # font size
    font1 = ("Helvetica",nfont)                        # axis label font
    font2 = ("Helvetica",Nint(1.2*nfont))              # axis title font
    font3 = ("Helvetica",Nint(1.4*nfont))              # plot title font
    w.create_text((ixmin+ixmax)/2,iymax-3*nfont,text=title,font=font3)

    iyc = (iymax + iymin)/2.                            # color legend
    iyd = min((ixmax - ixmin + iymin - iymax)/8., (iymin - iymax)/3.)
    ixd = iyd/5.
    ix1 = Nint(ixmax +    ixd); iy1 = Nint(iyc + iyd)
    ix2 = Nint(ixmax + 2*ixd); iy2 = Nint(iyc - iyd)
    (zmin,zmax,icol,ncol,nintv) = ColorLegend(zmin,zmax,ix1,ix2,iy1,iy2)
    if (nintv <= 6): nintv *= 2

    hx = (ixmax-ixmin)/(nx-1e0)                         # draw grid
    hy = (iymax-iymin)/(ny-1e0)
    hz = (zmax-zmin)/(ncol-1e0)
    hv = (zmax-zmin)/nintv
    for iz in range(1,ncol+nintv+1):                    # loop over levels
        if (iz <= ncol):                                # color shades
            z0 = zmin + (iz-1)*hz
```