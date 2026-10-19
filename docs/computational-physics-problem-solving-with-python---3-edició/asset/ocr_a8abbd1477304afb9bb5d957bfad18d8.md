# 20.2.4

# Heat Equation Implementation

Recall that we want to solve for the temperature distribution within an aluminum bar of length L = 1 m subject to the boundary and initial conditions

T(x = 0, t) = T(x = L, t) = 0 K,    T(x, t = 0) = 100 K.    (20.22)

The thermal conductivity, specific heat, and density for Al are

K = 237 W/(mK),    C = 900 J/(kg K),    ρ = 2700 kg/m³.    (20.23)

+   1. Write or modify EqHeat.py in Listing 20.1 to solve the heat equation.
+   2. Define a 2D array T[101,2] for the temperature as a function of space and time. The first index is for the 100 space divisions of the bar, and the second index is for present and past times (because you may have to make thousands of time steps, you save memory by saving only two times).
+   3. For time t = 0 (j = 1), initialize T so that all points on the bar except the ends are at 100 K. Set the temperatures of the ends to 0 K.
+   4. Apply (20.14) to obtain the temperature at the next time step.
+   5. Assign the present-time values of the temperature to the past values: T[i,1] = T[i,2], i = 1,...,101.
+   6. Start with 50 time steps. Once you are confident the program is running properly, use thousands of steps to see the bar cool smoothly with time. For approximately every 500 time steps, print the time and temperature along the bar.

# 20.3

# Assessment and Visualization

+   1. Check that your program gives a temperature distribution that varies smoothly along the bar and agrees with the boundary conditions, as in Figure 20.3.

![](bbox=[0.12, 0.72, 0.46, 0.86])

Figure 20.3 A numerical calculation of the temperature vs. position and vs. time, with isotherm contours projected onto the horizontal plane.