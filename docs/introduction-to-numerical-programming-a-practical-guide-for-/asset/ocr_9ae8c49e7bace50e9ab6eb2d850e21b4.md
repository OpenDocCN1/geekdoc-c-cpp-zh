```
#     1 - resize x-axis to provided user interval (xminp,xmaxp)
# ioptx - 0 - resize y-axis automatically
#       1 - resize y-axis to provided user interval (yminp,ymaxp)
# fxmin  - min fractional x-limit of viewport (0 < fxmin < fxmax < 1)
# fxmax  - max fractional x-limit of viewport
# fymin  - min fractional y-limit of viewport (0 < fymin < fymax < 1)
# fymax  - max fractional y-limit of viewport
# title  - plot title
#------------------------------------------------------------
    global w, nxw, nyw                         # canvas object and size
    ind = [0]*(n+1)

    if (ioptx):                                # x-domain limits
        xmin = xminp; xmax = xmaxp             # input values
    else:
        xmin = min(x[1:]); xmax = max(x[1:])   # bounding values
    if (iopty):                                # y-domain limits
        ymin = yminp; ymax = ymaxp             # input values
    else:
        ymin = min(y[1:]); ymax = max(y[1:])   # bounding values

    ixmin = Nint(fxmin*nxw); iymin = Nint((1e0-fymin)*nyw)   # viewport limits
    ixmax = Nint(fxmax*nxw); iymax = Nint((1e0-fymax)*nyw)

    nfont = int((ixmax-ixmin)/20.)                         # font size
    font = ("Helvetica",nfont)                            # title font
    w.create_text((ixmin+ixmax)/2,iymax-3*nfont,text=title,font=font)  # title

    f = (xmax-xmin)/(ymax-ymin)                # scale viewport proportionally
    if (f < float(ixmax-ixmin)/(iymin-iymax)): # shorter x-axis
        ixmax = ixmin + ixmax                  # adjust ixmin and ixmax
        ixmin = int(0.5*(ixmax + (iymax-iymin)*f))
        ixmax = ixmax - ixmin
    else:                                      # shorter y-axis
        iymax = iymin + iymax                  # adjust iymin and iymax
        iymin = int(0.5*(iymax + (ixmax-ixmin)/f))
        iymax = iymax - iymin

    ax = (ixmax-ixmin)/(xmax-xmin); bx = ixmin - ax*xmin      # scaling coeffs
    ay = (iymax-iymin)/(ymax-ymin); by = iymin - ay*ymin

    for il in range(1,n+1):                    # draw bonds
        for i2 in range(1,il):
            dx = x[il] - x[i2]; dy = y[il] - y[i2]; dz = z[il] - z[i2]
            d = sqrt(dx*dx + dy*dy + dz*dz)
            if ( d <= dmax):
                ix1 = Nint(ax*x[il]+bx); iy1 = Nint(ay*y[il]+by)
                ix2 = Nint(ax*x[i2]+bx); iy2 = Nint(ay*y[i2]+by)
                w.create_line(ix1,iy1,ix2,iy2,fill="slate gray",width=10)
                w.create_line(ix1,iy1,ix2,iy2,fill="gray",width=6)
                w.create_line(ix1,iy1,ix2,iy2,fill="white",width=2)

    Index(z,ind,n)                             # index particles in increasing order of z

    for i in range(1,n+1):                     # draw particles in increasing order of z
        il = ind[i]
        ix = Nint(ax*x[il]+bx); iy = Nint(ay*y[il]+by)
        rgb = w.info_rgb(col[il])              # rgb representation of dimmed color
        (rc, gc, bc) = (int(rgb[0]/512), int(rgb[1]/512), int(rgb[2]/512))
```