```
SwingUtilities.invokeLater( new Runnable() {
public void run() {
app.createAndShowGUI();
} } );
}
```

# # USING POLAR COORDINATES

Cartesian coordinates are represented as a pair of (x,y) values. Polar coordinates are represented as an angle and a distance. See Figure 3.3.

![](bbox=[0.1, 0.34, 0.7, 0.58])

Figure 3.3
Cartesian vs. Polar Coordinates.
© 2014 Timothy Wright.

Instead of an (x,y) pair, polar coordinates are in the form (r,a), where r is a distance (radius), and a is an angle. Because Java's trigonometric functions use radians, all angles are assumed to be in radians. It is easy to convert between the two representations, however:

```
Math.toRadians( double degrees )
Math.toDegrees( double radians )
```

To convert from the Cartesian coordinates to the polar coordinates, the point can be treated as a triangle, using trigonometry to solve for the desired values.