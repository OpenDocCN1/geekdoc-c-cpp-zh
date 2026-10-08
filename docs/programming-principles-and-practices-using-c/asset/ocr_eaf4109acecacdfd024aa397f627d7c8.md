simplify the code and minimize that chance of error (and minimize frustrating debugging), we define a little class to do the calculation for us:

```
class Scale {
    // data value to coordinate conversion
    int cbase;      // coordinate base
    int vbase;      // base of values
    double scale;

public:
    Scale(int b, int vb, double s) :cbase{b}, vbase{vb}, scale{s} {}
    int operator()(int v) const { return cbase + (v-vbase)*scale; } // see $21.4
};
```

We want a class because the calculation depends on three constant values that we wouldn’t like to unnecessarily repeat. Given that, we can define

```
Scale xs (xoffset,base_year,xscale);
Scale ys (ymax-yoffset,0,-yscale);
```

Note how we make the scaling factor for **ys** negative to reflect the fact that *y* coordinates grow downward whereas we usually prefer higher values to be represented by higher points on a graph. Now we can use **xs** to convert a year to an *x* coordinate. Similarly, we can use **ys** to convert a percentage to a *y* coordinate.

# **15.6.4 Building the graph**

Finally, we have all the prerequisites for writing the graphing code in a reasonably elegant way. We start creating a window and placing the axes:

```
Window win {Point{100,100},xmax,ymax,"Aging Japan"};
```

```
Axis x {Axis::x, Point(xoffset,ymax-yoffset), xlength,
        (end_year-base_year)/10,
        "year    1960    1970    1980    1990    "
        "2000    2010    2020    2030    2040"};
x.label.move(-100,0);
```

```
Axis y {Axis::y, Point(xoffset,ymax-yoffset), ylength, 10,"% of population"};
```

```
Line current_year {Point{xs(2008),ys(0)},Point{xs(2008),ys(100)}};
current_year.set_style(Line_style::dash);
```