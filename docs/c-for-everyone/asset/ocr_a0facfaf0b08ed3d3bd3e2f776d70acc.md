# Engineering P5.34

In a movie theater, the angle θ at which a viewer sees the picture on the screen depends on the distance x of the viewer from the screen. For a movie theater with the dimensions shown in the picture below, write a function that computes the angle for a given distance.

![](bbox=[0.32, 0.174, 0.806, 0.296])

Next, provide a more general function that works for theaters with arbitrary dimensions.

# Engineering P5.35

![](bbox=[0.0775, 0.383, 0.224, 0.543])

Electric wire, like that in the photo, is a cylindrical conductor covered by an insulating material. The resistance of a piece of wire is given by the formula

$$R = \frac{\rho L}{A} = \frac{4\rho L}{\pi d^2}$$

where ρ is the resistivity of the conductor, and L, A, and d are the length, cross-sectional area, and diameter of the wire. The resistivity of copper is $1.678 \times 10^{-8}\ \Omega\,\text{m}$. The wire diameter, d, is commonly specified by the American wire gauge (AWG), which is an integer, n. The diameter of an AWG n wire is given by

$$d = 0.127 \times 92^{\frac{36-n}{39}}\ \text{mm}$$

Write a C++ function

```
```cpp
double diameter(int wire_gauge)
```
```

that accepts the wire gauge and returns the corresponding wire diameter. Write another C++ function

```
```cpp
double copper_wire_resistance(double length, int wire_gauge)
```
```

that accepts the length and gauge of a piece of copper wire and returns the resistance of that wire. The resistivity of aluminum is $2.82 \times 10^{-8}\ \Omega\,\text{m}$. Write a third C++ function

```
```cpp
double aluminum_wire_resistance(double length, int wire_gauge)
```
```

that accepts the length and gauge of a piece of aluminum wire and returns the resistance of that wire.

Write a C++ program to test these functions.

# Engineering P5.36

The drag force on a car is given by

$$F_D = \frac{1}{2}\rho v^2 A C_D$$

where ρ is the density of air (1.23 kg/m³), v is the velocity in units of m/s, A is the projected area of the car (2.5 m²), and C_D is the drag coefficient (0.2).