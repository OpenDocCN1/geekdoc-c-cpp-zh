```
ymax = max(ymax,y[i]+sig[i])

i xmin = Nint(fxmin*nxw); iymin = Nint((1e0-fymin)*nyw)    # viewport limits
i xmax = Nint(fxmax*nxw); iymax = Nint((1e0-fymax)*nyw)

if (2 in sty[1:]):                                      # polar plot
    xmin = min(xmin,ymin); xmax = max(xmax,ymax)        # make domain square
    xmax = max(abs(xmin),abs(xmax)); xmin = -xmax
    ymin = xmin; ymax = xmax
    if (ixmax-ixmin > iymin-iymax):                    # adjust viewport limits
        c = 0.5*(ixmin+ixmax)
        d = 0.5*(iymin-iymax)
        ixmin = c - d; ixmax = c + d
    if (ixmax-ixmin < iymin-iymax):
        c = 0.5*(iymin+iymax)
        d = 0.5*(ixmax-ixmin)
        iymin = c + d; iymax = c - d

w.create_rectangle(ixmin,iymax,ixmax,iymin)            # draw plot frame

nfont = min(int((ixmax-ixmin)/60.) + 3,12)              # font size
font1 = ("Helvetica",nfont)                           # axis label font
font2 = ("Helvetica",Nint(1.2*nfont))                 # axis title font
font3 = ("Helvetica",Nint(1.4*nfont))                 # plot title font
if ((ixmax-ixmin) < 3 * (iymax-iymin)):
    w.create_text((ixmin+ixmax)/2,iymax-3*nfont,text=title,font=font3)
else:
    w.create_text(ixmax,iymax,text=title,font=font2,anchor="ne")

(xmin,xmax,scale,nsigd,nintv) = Limits(xmin,xmax,maxint)  # extend limits
ax = (ixmax-ixmin)/(xmax-xmin)                          # x scaling coefficients
bx = ixmin - ax*xmin

tic = (ixmax-ixmin)/100.                                # tic length
h = (xmax-xmin)/nintv; htic = ax * h                    # labeling step
iytext = iymin + 1.5*nfont
for i in range(0,nintv+1):                              # label axis
    ix = Nint(ixmin + i*htic)
    w.create_line(ix,iymin,ix,iymin-tic)               # tics
    w.create_line(ix,iymax,ix,iymax+tic)
    if (xtext != "None"):
        (mant,expn) = FormStr(xmin+i*h,scale,nsigd)
        w.create_text(ix,iytext,text=mant,font=font1)  # labels

if (xtext != "None"):
    if ((scale<0.1) or (scale>1000.0)): xtext = xtext + " 1e" + expn
    ixtext = (ixmin+ixmax)/2
    iytext = iytext + 2*nfont
    w.create_text(ixtext,iytext,text=xtext,font=font2) # x title

# Y-AXIS
if (ymin == 0.0 and ymax == 0.0): ymin = -1e0; ymax = 1e0   # horizontal
if (abs(ymax-ymin) < 1e-5*abs(ymax)): ymin *= 0.9; ymax *= 1.1
(ymin,ymax,scale,nsigd,nintv) = Limits(ymin,ymax,maxint)  # extend limits
a y = (iymax-iymin)/(ymax-ymin)                         # y scaling coefficients
by = iymin - ay*ymin

h = (ymax-ymin)/nintv; htic = ay * h                    # labeling step size
ixt ext = ixmin - nfont
for i in range(0,nintv+1):                              # label axis
```