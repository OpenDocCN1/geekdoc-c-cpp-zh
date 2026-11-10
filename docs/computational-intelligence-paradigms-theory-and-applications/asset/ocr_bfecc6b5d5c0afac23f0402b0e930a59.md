![](bbox=[0.087, 0.095, 0.854, 0.468])

**FIGURE 7.11:** Centroid defuzzification

```
```matlab
x1 = defuzz(x,m4,'centroid')
h1 = line([x1 x1],[-0.2 1.2],'Color','k');
t1 = text(x1,-0.2,' centroid','FontWeight','bold');
```
```

# Bisector method

The bisector is the vertical line that will divide the region into two sub-regions of equal area. It is sometimes, but not always coincident with the centroid line. Here the defuzzified value is -0.6000 as shown in Figure 7.12.

```
```matlab
x2 = defuzz(x,m4,'bisector')
h2 = line([x2 x2],[-0.4 1.2],'Color','k');
t2 = text(x2,-0.4,' bisector','FontWeight','bold');
```
```

# Mean of Maximum methods

MOM, SOM, and LOM stand for Middle, Smallest, and Largest of Maximum, respectively. These three methods key off the maximum value assumed by the aggregate membership function. The mean of maximum method is used to compute the defuzzified value at -4 as shown in Figure 7.13.