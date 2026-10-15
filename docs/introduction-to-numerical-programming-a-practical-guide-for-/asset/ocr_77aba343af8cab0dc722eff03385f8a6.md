```
w.create_text((ixmin+ixmax)/2,i y max-3*nfont,text=title,font=font3)
else:
    w.create_text(ixmax,iymax,text=title,font=font2,anchor="ne")
    maxint y = max(5,(iymin-iymax)/(ixmax-ixmin)*maxintx)

(xmin,xmax,scale,nsigd,nintv) = Limits(xmin,xmax,maxintx)  # X-AXIS
ax = (ixmax-ixmin)/(xmax-xmin)                           # x scaling coefficients
bx = ixmin - ax*xmin

tic = (ixmax-ixmin)/100.                                  # tic length
h = (xmax-xmin)/nintv; htic = ax * h                       # labeling step
itytext = iymin + 1.5*nfont
for i in range(0,nintv+1):                                  # label axis
    ix = Nint(ixmin + i*htic)
    w.create_line(ix,iymin-tic,ix,iymin+tic)                 # tics
    if (xtext != "None"):
        (mant,expn) = FormStr(xmin+i*h,scale,nsigd)
        w.create_text(ix,itytext,text=mant,font=font1)       # labels

if (xtext != "None"):
    if ((scale<0.1) or (scale>1000.0)): xtext = xtext + " 1e" + expn
    ixtext = (ixmin+ixmax)/2
    iytext = iymin + 2*nfont
    w.create_text(ixtext,iytext,text=xtext,font=font2)       # x title

if (ymin == 0.0 and ymax == 0.0): ymin = -1e0; ymax = 1e0  # horizontal
if (abs(ymax-ymin) < 1e-5*abs(ymax)): ymin *= 0.9; ymax *= 1.1
(ymin,ymax,scale,nsigd,nintv) = Limits(ymin,ymax,maxinty)   # extend limits
ay = (iymax-iymin)/(ymax-ymin)                              # y scaling coefficients
by = iymin - ay*ymin

h = (ymax-ymin)/nintv; htic = ay * h                        # labeling step size
ixtext = ixmin - nfont
for i in range(0,nintv+1):                                  # label axis
    iy = Nint(iymin + i*htic)
    w.create_line(ixmin,iy,ixmin+tic,iy)
    w.create_line(ixmax,iy,ixmax-tic,iy)                    # tics
    if (ytext != "None"):
        (mant,expn) = FormStr(ymin+i*h,scale,nsigd)
        w.create_text(ixtext,iy,text=mant,font=font1,anchor="e")  # labels

if (ytext != "None"):
    if ((scale<0.1) or (scale>1000.0)): ytext = ytext + " 1e" + expn
    ixtext = ixtext - (3*nfont/4) * (len(mant) + 2)         # skip labels + 2
    iytext = (iymin+iymax)/2                                # vertical middle
    w.create_text(ixtext,iytext,text=ytext,font=font2,anchor="e") # y title

if (xmin*xmax < 0): w.create_line(Nint(bx),iymin,Nint(bx),iymax) # y-axis
if (ymin*ymax < 0): w.create_line(ixmin,Nint(by),ixmax,Nint(by)) # x-axis

tic = 2*tic/3
if (sty == 4): hx = ax * (x[2] - x[1])
ix0 = Nint(ax*x[1]+bx); iy0 = Nint(ay*y[1]+by)             # 1st point
for i in range(1,n+1):
    ix = Nint(ax*x[i]+bx); iy = Nint(ay*y[i]+by)             # new point
    if (sty == 0):                                           # scatter plot
        w.create_rectangle(ix-tic,iy-tic,ix+tic,iy+tic, \
                           fill="",outline=col)
```