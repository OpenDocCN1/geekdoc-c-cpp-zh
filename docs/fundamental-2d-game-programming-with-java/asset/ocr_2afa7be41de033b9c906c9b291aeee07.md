# Trigonometry to the rescue:

```
sin(θ + ϕ) = sin θ cos ϕ + cos θ sin ϕ
cos(θ + ϕ) = cos θ cos ϕ - sin θ sin ϕ
```

Replacing the previous equation with this new representation gives:

```
x' = r(cos θ cos ϕ - sin θ sin ϕ)
y' = r(sin θ cos ϕ + cos θ sin ϕ)
```

Distributing the r values gives:

```
x' = r cos θ cos ϕ - r sin θ sin ϕ
y' = r sin θ cos ϕ + r cos θ sin ϕ
```

Remembering the following:

```
x = r cos θ
y = r sin θ
```

You can substitute the original x and y values, leaving the following:

```
x' = x cos ϕ - y sin ϕ
y' = y cos ϕ - x sin ϕ
```

This is the equation presented earlier for rotation of a coordinate in the Vector2f class. The PolarCoordinateExample, located in the javagames.transform package and shown in Figure 3.5, converts from a Cartesian coordinate to a polar coordinate and back again. The coord variable holds the screen position where the mouse is located, offset by the center of the screen.