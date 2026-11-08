A control data set that draws the font characters (in this case just a circle) is first generated in a DATA step. Like annotate data sets, specific variables are used to pass information to the GFONT procedure. Here we are drawing the outline of a circle using 721 short line segments. This control data set is then passed to GFONT.

```
```sas
data fontdata(keep=char seg x y lp ptype);
retain char 'c';             /* 1 */
       seg;                   /* 2 */
       lp 'p';                /* 3 */
ptype='w'; x=10; y=110; output fontdata; /* 4 */
ptype='w'; x=100; y=50; output fontdata; /* 5 */
do deg = 0 to 360 by 5;
   rad = deg*arcos(-1)/180;
   x=50*cos(rad)+50;
   y=50*sin(rad)+50;
   output fontdata;           /* 6 */
end;
run;
libname gfont0 "path\\data"; /* 7 */
proc gfont data=fontdata
          name=mydot;          /* 8 */
          filled                /* 9 */
          resolution=3;         /* 10 */
run;
symbol1 f=mydot c=blue v='c' h=1;
```
```

+   1. The variable CHAR is used to hold the keyboard character ‘c’ used to designate its symbol within the MYDOT font.
+   2. Symbol segments allow you to create symbols with disconnected parts (segments). This symbol has only one segment so this value is a constant.
+   3. This is to be a polygon figure.
+   4. Width of the character (PTYPE='w'). The symbol will have a width of 100 units. Allow about 10% extra for character spacing.

+   5. This is the first coordinate of the plot symbol (PTYPE='v').
+   6. The segment is written to the control data set.
+   7. Generated fonts are stored in a catalog named FONTS. SAS/GRAPH software searches for this catalog in numbered librefs whose names start with GFONT.
+   8. Name the font.
+   9. We want the shape to be filled.
+   10. Increase the font resolution. You may notice little or no difference between a value of 1 and 3.

![](bbox=[0.206, 0.558, 0.512, 0.735])

The resulting dots are a bit smoother. In this screen capture some pixelation has taken place when the image was copied into this document.

# SEE ALSO

Carpenter (1995) uses PROC GFONT to create a logo and sunflower symbols that self adjust according to the plotted value. Plot symbol resolution was further discussed with alternate solutions in the SAS Forum thread at http://support.sas.com/forums/thread.jspa?threadID=12547&start=0&start=0.