
```
for gc in range(0,256,ncolstep):
    i += 1; icol[i] = "#%02x%02x%02x" % (rc,gc,bc)

gc = 255; rc = 0
for bc in range(255,-1,-ncolstep):
    i += 1; icol[i] = "#%02x%02x%02x" % (rc,gc,bc)

bc = 0; gc = 255
for rc in range(0,256,ncolstep):
    i += 1; icol[i] = "#%02x%02x%02x" % (rc,gc,bc)

bc = 0; rc = 255
for gc in range(255,-1,-ncolstep):
    i += 1; icol[i] = "#%02x%02x%02x" % (rc,gc,bc)

gc = 0; rc = 255
for bc in range(0,256,ncolstep):
    i += 1; icol[i] = "#%02x%02x%02x" % (rc,gc,bc)

return (icol, ncol)

#==============================================================================
def ColorLegend(fmin, fmax, ixmin, ixmax, iymin, iymax):
#------------------------------------------------------------------------------
# Draws and labels the color legend for the interval [fmin,fmax] in the
# rectangle [ixmin,ixmax] x [iymin,iymax]. [fmin,fmax] is extended to fit at
# most 10 intervals expressible as d * 10^p, with d = 1, 2, 5 and p integer.
#
#### Returns: fmin, fmax, icol, ncol, nintv
#------------------------------------------------------------------------------
    global w, nxw, nyw                     # canvas object and size

    nfont = min(int((iymax-iymin)/20.),12)
    font = ("Helvetica",nfont)                       # label font

    ncolstep = 2
    (icol,ncol) = RGBcolors(ncolstep)

    hcol = float(ncol) / (iymax - iymin)
    for iy in range(iymax,iymin+1):
        ic = min(max(1,int((iy-iymin)*hcol)),ncol)
        w.create_line(ixmin,iy,ixmax,iy,fill=icol[ic])
    w.create_rectangle(ixmin,iymin,ixmax,iymax)

    (fmin,fmax,scale,nsigd,nintv) = Limits(fmin,fmax,10)      # extend limits
    ay = (iymax-iymin)/(fmax-fmin)                         # scaling coefficients
    by = iymin - ay*fmin
    h = (fmax-fmin)/nintv; htic = ay * h                   # labeling step size
    ixtext = ixmax + (nsigd+1)*nfont
    for i in range(0,nintv+1):                             # label legend
        iy = Nint(iymin + i*htic)
        (mant,expn) = FormStr(fmin+i*h,scale,nsigd)
        w.create_text(ixtext,iy,text=mant,font=font,anchor="e")      # labels

    if ((scale<0.1) or (scale>1000.0)):
        ytext = " x 1e" + expn
        w.create_text(ixtext,iymin+2*nfont,text=ytext,font=font,anchor="e")

return (fmin, fmax, icol, ncol, nintv)

#================================================================================
def Contour(z, nx, ny, xmin, xmax, ymin, ymax, zmin, zmax, \
            fxmin, fxmax, fymin, fymax, xtext, ytext, title):
#--------------------------------------------------------------------------------
# Plots a function z(x,y) defined in [xmin,xmax] x [ymin,ymax] and tabulated
# on a regular Cartesian grid with (nx-1)x(ny-1) mesh cells as contour plot.
#### The level curves result by inverse linear interpolation inside the cells.
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
#### title   - plot title
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

col = icol[iz]
else:
    # lines
    z0 = zmin + (iz-ncol)*hv
for i in range(1,nx):                # loop over cells [i][j]
    for j in range(1,ny):            # corner coordinates
        ix = Nint(ixmin + (i-1)*hx); ixh = Nint(ixmin + i*hx)
        iy = Nint(iymin + (j-1)*hy); iyh = Nint(iymin + j*hy)
        z1 = z[i][j]   - z0; z2 = z[i+1][j]   - z0   # rel. corner values
        z3 = z[i][j+1] - z0; z4 = z[i+1][j+1] - z0

        if (z1 < 0e0 or z2 < 0e0 or z3 < 0e0 or z4 < 0e0):
            ng = 0                      # level line passes through the cell
            if (z1*z2 <= 0):            # intersection with lower edge
                if (z1 != z2):
                    ng += 1; xg[ng] = Nint(ix + z1/(z1-z2)*hx); yg[ng] = iy
                else:                   # line coincides with edge
                    ng += 1; xg[ng] = ix ; yg[ng] = iy
                    ng += 1; xg[ng] = ixh; yg[ng] = iy

            if (z1*z3 <= 0):            # intersection with left edge
                if (z1 != z3):
                    ng += 1; xg[ng] = ix; yg[ng] = Nint(iy + z1/(z1-z3)*hy)
                else:                   # line coincides with edge
                    ng += 1; xg[ng] = ix; yg[ng] = iy
                    ng += 1; xg[ng] = ix; yg[ng] = iyh

            if (z2*z4 <= 0):            # intersection with right edge
                if (z2 != z4):
                    ng += 1; xg[ng] = ixh; yg[ng] = Nint(iy + z2/(z2-z4)*hy)
                else:                   # line coincides with edge
                    ng += 1; xg[ng] = ixh; yg[ng] = iy
                    ng += 1; xg[ng] = ixh; yg[ng] = iyh

            if (z3*z4 <= 0):            # intersection with upper edge
                if (z3 != z4):
                    ng += 1; xg[ng] = Nint(ix + z3/(z3-z4)*hx); yg[ng] = iyh

            if (iz <= ncol):
                polygon0 = ()
                if (z1 >= 0e0): polygon0 += ix , iy
                if (z2 >= 0e0): polygon0 += ixh, iy
                if (z3 >= 0e0): polygon0 += ix , iyh
                if (z4 >= 0e0): polygon0 += ixh, iyh
                for ig in range(1,ng+1):    # fill the polygon above level
                    for jg in range(1,ng):
                        polygon = polygon0 + (xg[ig],yg[ig],xg[jg],yg[jg])
                        w.create_polygon(polygon,fill=col,outline=col)
            else:
                for ig in range(1,ng+1):    # draw levele line
                    for jg in range(1,ng):
                        w.create_line(xg[ig],yg[ig],xg[jg],yg[jg])
        else:                           # all corner values exceed level - fill entire cell
            if (iz <= ncol):
                w.create_rectangle(ix,iy,ixh,iyh,fill=col,outline=col)

w.create_rectangle(ixmin,iymax,ixmax,iymin)          # draw border
                                            # X-AXIS
maxint = 10
(xmin1,xmax1,scale,nsigd,nintv) = Limits(xmin,xmax,maxint) # extend limits
```
