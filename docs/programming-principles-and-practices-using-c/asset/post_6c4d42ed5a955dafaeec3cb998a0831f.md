
vidual points with information. If we want to go beyond that, we’ll have to write new graphics classes or adopt another graphics library.

So, our data is basically pairs of values, such as **(year, number of children)**. If we have more data, with **(year, number of children, number of adults, number of elderly)**, we simply have to decide which pair of values – or pairs of values – we want to draw. In our example, we simply graphed **(year, number of children)**, **(year, number of adults)**, and **(year, steel production)**.

There are many ways of looking at a set of **(x,y)** pairs. When considering how to graph such a set it is important to consider whether one value is in some way a function of the other. For example, for a **(year, steel production)** pair it would be quite reasonable to consider the steel production a function of the year and display the data as a continuous line. **Open_polyline** (§13.6) is the obvious choice for graphing such data. If **y** should not be seen as a function of **x**, for example **(gross domestic product per person, population of country)**, **Marks** (§13.15) can be used to plot unconnected points.

Now, back to our Japanese age distribution example.

## 15.6.1 Reading a file

The file of age distributions consists of lines like this:

```cpp
( 1960 : 30 64 6 )
( 1970 : 24 69 7 )
( 1980 : 23 68 9 )
```

The first number after the colon is the percentage of children (age 0–14) in the population, the second is the percentage of adults (age 15–64), and the third is the percentage of the elderly (age 65+). Our job is to read those. Note that the formatting of the data is slightly irregular. As usual, we have to deal with such details.

To simplify that task, we first define a type **Distribution** to hold a data item and an input operator to read such data items:

```cpp
struct Distribution {
    int year, young, middle, old;
};

istream& operator>>(istream& is, Distribution& d)
// assume format: ( year : young middle old )
{
    char ch1 = 0;
    char ch2 = 0;
    char ch3 = 0;
    Distribution dd;

    if (is >> ch1 >> dd.year
        >> ch2 >> dd.young >> dd.middle >> dd.old
        >> ch3) {
        if (ch1!='(' || ch2!=':' || ch3!=')') {
            is.clear(ios_base::failbit);
            return is;
        }
    }
    else
        return is;
    d = dd;
    return is;
}
```

This is a straightforward application of the ideas from Chapter 10. If this code isn’t clear to you, please review that chapter. We didn’t need to define a Distribution type and a >> operator. However, it simplifies the code compared to a brute-force approach of “just read the numbers and graph them.” Our use of Distribution splits the code up into logical parts to help comprehension and debugging. Don’t be shy about introducing types “just to make the code clearer.” We define classes to make the code correspond more directly to the way we think about the concepts in our code. Doing so even for “small” concepts that are used only very locally in our code, such as a line of data representing the age distribution for a year, can be most helpful.

Given Distribution, the read loop becomes

```cpp
string file_name = "japanese-age-data.txt";
ifstream ifs (file_name);
if (!ifs) error("can't open ", file_name);

// ...

for (Distribution d; ifs>>d;) {
    if (d.year<base_year|| end_year<d.year)
        error("year out of range");
    if (d.young+d.middle+d.old != 100)
        error("percentages don't add up");
    // ...
}
```

That is, we try to open the file **japanese-age-data.txt** and exit the program if we don’t find that file. It is often a good idea *not* to “hardwire” a file name into the source code the way we did here, but we consider this program as an example of a small “one-off” effort, so we don’t burden the code with facilities that are more appropriate for long-lived applications. On the other hand, we did put **japanese-age-data.txt** into a named **string** variable so the program is easy to modify if we want to use it – or some of its code – for something else.

The read loop checks that the year read is in the expected range and that the percentages add up to 100. That’s a basic sanity check for the data. Since **>>** checks the format of each individual data item, we didn’t bother with further checks in the main loop.

### 15.6.2 General layout

So what do we want to appear on the screen? You can see our answer at the beginning of **§15.6**. The data seems to ask for three **Open polylines** – one for each age group. These graphs need to be labeled, so we decided to write a “caption” for each line at the left-hand side of the window. In this case, that seemed clearer than the common alternative: to place the label somewhere along the line itself. In addition, we use color to distinguish the graphs and associate their labels.

We want to label the *x* axis with the years. The vertical line through the year 2008 indicates where the graph goes from hard data to projected data.

We decided to just use the window’s label as the title for our graph.

Getting graphing code both correct and good-looking can be surprisingly tricky. The main reason is that we have to do a lot of fiddly calculations of sizes and offsets. To simplify that, we start by defining a set of symbolic constants that defines the way we use our screen space:

```cpp
constexpr int xmax = 600;    // window size
constexpr int ymax = 400;

constexpr int xoffset = 100; // distance from left-hand side of window to y axis
constexpr int yoffset = 60;  // distance from bottom of window to x axis

constexpr int xpace = 40;    // space beyond axis
constexpr int ypace = 40;

constexpr int xlength = xmax–xoffset–xpace;    // length of axes
constexpr int ylength = ymax–yoffset–ypace;
```

Basically this defines a rectangular space (the window) with another rectangle (defined by the axes) within it:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_574_0.png)

We find that without such a “schematic view” of where things are in our window and the symbolic constants that define it, we get lost and become frustrated when our output doesn’t reflect our wishes.

### 15.6.3 Scaling data

Next we need to define how to fit our data into that space. We do that by scaling the data so that it fits into the space defined by the axes. To do that we need the scaling factors that are the ratio between the data range and the axis range:

```cpp
constexpr int base_year = 1960;
constexpr int end_year = 2040;

constexpr double xscale = double(xlength)/(end_year–base_year);
constexpr double yscale = double(ylength)/100;
```

We want our scaling factors (*xscale* and *yscale*) to be floating-point numbers – or our calculations could be subject to serious rounding errors. To avoid integer division, we convert our lengths to **double** before dividing (§4.3.3).

We can now place a data point on the *x* axis by subtracting its base value (1960), scaling with *xscale*, and adding the *xoffset*. A *y* value is dealt with similarly. We find that we can never remember to do that quite right when we try to do it repeatedly. It may be a trivial calculation, but it is fiddly and verbose. To simplify the code and minimize that chance of error (and minimize frustrating debugging), we define a little class to do the calculation for us:

```cpp
class Scale {
    // data value to coordinate conversion
    int cbase;      // coordinate base
    int vbase;      // base of values
    double scale;

public:
    Scale(int b, int vb, double s) :cbase{b}, vbase{vb}, scale{s} {}
    int operator()(int v) const { return cbase + (v-vbase)*scale; } // see §21.4
};
```

We want a class because the calculation depends on three constant values that we wouldn’t like to unnecessarily repeat. Given that, we can define

```cpp
Scale xs (xoffset,base_year,xscale);
Scale ys (ymax-yoffset,0,-yscale);
```

Note how we make the scaling factor for **ys** negative to reflect the fact that *y* coordinates grow downward whereas we usually prefer higher values to be represented by higher points on a graph. Now we can use **xs** to convert a year to an *x* coordinate. Similarly, we can use **ys** to convert a percentage to a *y* coordinate.

### 15.6.4 Building the graph

Finally, we have all the prerequisites for writing the graphing code in a reasonably elegant way. We start creating a window and placing the axes:

```cpp
Window win {Point{100,100},xmax,ymax,"Aging Japan"};

Axis x {Axis::x, Point(xoffset,ymax-yoffset), xlength,
        (end_year-base_year)/10,
        "year    1960    1970    1980    1990    "
        "2000    2010    2020    2030    2040"};
x.label.move(-100,0);

Axis y {Axis::y, Point(xoffset,ymax-yoffset), ylength, 10,"% of population"};

Line current_year {Point{xs(2008),ys(0)},Point{xs(2008),ys(100)}};
current_year.set_style(Line_style::dash);
```
