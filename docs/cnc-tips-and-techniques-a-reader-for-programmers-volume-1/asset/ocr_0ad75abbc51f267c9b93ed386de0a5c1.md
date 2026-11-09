tough nut to crack during the initial software design, but the Fanuc engineers came up with a brilliant solution. They decided that the axis value (the axis data) associated with G28 will represent the intermediate tool location on the way to machine zero. Practically speaking, it means the CNC programmer can say, *“Yes, I want to move the tool to the home position, but I want to move it through a special point on the way.”*

That point is called the *intermediate point*. It is a point to go through before the actual motion to machine zero is activated. One client of mine has compared this intermediate point with a stop at the Post Office on the way home from work. That is exactly what the intermediate point is all about — a position, a location, to go through on the way to machine zero.

# ## Dimensioning

In a typical CNC program, the G28 command (with associated data) may be programmed in two modes of dimensioning; in the G90 absolute mode or in the G91 incremental mode. A typical program entry may look like this (Z-axis only shown):

```
```
G21 G90
...
G00 Z2.0
G28 Z2.0
M01
```
```

The same program segment in the incremental mode (G91) will be only a slightly different:

```
```
G21 G90
...
G00 Z2.0
G91 G28 Z0
M01
```
```

Both versions represent the same machining situation as