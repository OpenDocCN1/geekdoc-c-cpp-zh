```
```text
<Place the tool at the start point S>
G17 G03 X_ Y_ Z_ R_ F_; or G17 G02 Y_ Z_ X_ J_ F_;
```
```

where X_, Y_, Z_ = coordinates of the end point P  
R_ = radius of the circular/circular interpolation  
I_, J_ = X-, Y-coordinates of the axis of the helix with respect to the start point S  
F_ = feedrate along the projected toolpath on the XY-plane

G03 generates a counter-clockwise helix, as in Fig. 8.2. Replace it by G02 for a clockwise helix. The direction of the helix (CW/CCW) is determined by the right-hand rule where the thumb points in the positive direction of the linear axis. Thus, if the tool follows the direction of the curled fingers, it is called a counter-clockwise helix.

Helical interpolations along X- and Y-axes are done in a similar manner. (Note that the chosen orders of X_, Y_, and Z_ are only for our convenience in identifying the order of placement of circular interpolation. The plane of circular interpolation is decided by G17/G18/G19. In the word address format, which the CNC machine uses, the order of the arguments of a G-code is not important, barring a few exceptions such as the order of I-, J-, and K-word of the G65 “6G argument list”.)

```
```text
G18 G02/G03 X_ Z_ Y_ R_ F_; or G18 G02/G03 X_ Z_ Y_ I_ K_ F_;
G19 G02/G03 Y_ Z_ X_ R_ F_; or G19 G02/G03 Y_ Z_ X_ J_ K_ F_;
```
```

![](bbox=[0.112, 0.516, 0.894, 0.919])

**Figure 8.2** Helical interpolation along Z-axis on a milling machine.