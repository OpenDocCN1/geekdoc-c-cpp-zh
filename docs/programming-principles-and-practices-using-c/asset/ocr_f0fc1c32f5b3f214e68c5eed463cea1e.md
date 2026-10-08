That is, we try to open the file **japanese-age-data.txt** and exit the program if we don’t find that file. It is often a good idea *not* to “hardwire” a file name into the source code the way we did here, but we consider this program as an example of a small “one-off” effort, so we don’t burden the code with facilities that are more appropriate for long-lived applications. On the other hand, we did put **japanese-age-data.txt** into a named **string** variable so the program is easy to modify if we want to use it – or some of its code – for something else.

The read loop checks that the year read is in the expected range and that the percentages add up to 100. That’s a basic sanity check for the data. Since **>>** checks the format of each individual data item, we didn’t bother with further checks in the main loop.

# ### 15.6.2 General layout

So what do we want to appear on the screen? You can see our answer at the beginning of **§15.6**. The data seems to ask for three **Open polylines** – one for each age group. These graphs need to be labeled, so we decided to write a “caption” for each line at the left-hand side of the window. In this case, that seemed clearer than the common alternative: to place the label somewhere along the line itself. In addition, we use color to distinguish the graphs and associate their labels.

We want to label the *x* axis with the years. The vertical line through the year 2008 indicates where the graph goes from hard data to projected data.

We decided to just use the window’s label as the title for our graph.

Getting graphing code both correct and good-looking can be surprisingly tricky. The main reason is that we have to do a lot of fiddly calculations of sizes and offsets. To simplify that, we start by defining a set of symbolic constants that defines the way we use our screen space:

```
    constexpr int xmax = 600;    // window size
    constexpr int ymax = 400;

    constexpr int xoffset = 100; // distance from left-hand side of window to y axis
    constexpr int yoffset = 60;  // distance from bottom of window to x axis

    constexpr int xpace = 40;    // space beyond axis
    constexpr int ypace = 40;

    constexpr int xlength = xmax–xoffset–xpace;    // length of axes
    constexpr int ylength = ymax–yoffset–ypace;
```