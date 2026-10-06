```
{
  a[j] = W(ids[j])
  total += a[j]
}

start = start ? (GetWindowWidth() - total) * start : offset * 1
```

The first line compares the argument with TP and BM (global variables containing the values 'top' and 'bottom'). If one of these values, the menu will be laid horizontally, the for () loop places all of the objects in the array by fetching them with the W() plug-in. The total variable is also increased by this value so that when the loop has finished it counts the sum of all object widths and all the gaps (the latter having been assigned earlier).

Then, if start is not zero, it calculates the percentage value that was previously assigned, so the width of the browser, as returned by GetWindowWidth() less the value in total, is multiplied by start. This value represents the percent offset from the start of the edge. However if start is 0, then offset contains the number of pixels the menus should be located from the edge. because this value may be a string, it is multiplied by 1 to turn it into an integer. The result is then placed in start.

The second part of the if () statement repeats the procedure, substituting values for the left or right edge of the screen, like this:

```
{
  for (var j = 0 ; j < len; ++j)
    a[j] = H(ids[j])
    total += a[j]
}

start = start ? (GetWindowHeight() - total) * start : offset * 1
```

Finally, another for loop iterates through the array and calls the HoverSlide() plug-on for each object, placing them in all their correct positions based on the value of start, plus that jump. Initially, jump is zero so there is no additional offset, but each object is added to the menu, jump is incremented by the previous object width and the size of the gap, so that each object is located at the correct distance from the previous one.

# How To Use It

To use this plug-in, you need to create an object for each of the sliding menu parts. A div is perfect for the job. Fill each with the images, links, and any other contents you need, and make sure the edge of the div is a suitable tab that will make people want to pass their mouse over it. Now you will need to call the plug-in, like this:

```
HoverSlideMenu(ids, 'top', '%50', 20, 10, 200)
```

In this example, the objects in the array ids are passed to the plug-in, telling it to place the menus at the browser top, 50 percent along the edge (therefore in the middle), with 20 pixels