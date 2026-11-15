# Modify 6.9

+   1. Run the Newton–Raphson program using the same coefficients and an initial guess of –1.
+   2. Run the Newton–Raphson program using the same coefficients and an initial guess of –2. Explain what happens.
+   3. Modify the Newton–Raphson program to allow the user to input the tolerance used to stop the iterations.
+   4. Modify the Newton–Raphson program to find the roots of a fifth-degree polynomial.

# 6.11 Numerical Technique: Integration

The operation of integration gives engineers and scientists important information about functions or data sets. For example, distance, velocity, and acceleration all relate to each other through integration. Velocity is the integral of acceleration and distance is the integral of velocity. The topic of integration is covered in detail in calculus courses, but the underlying principles can be explained simply in terms of area. The integral of a function over an interval represents the area under the graph of the function. Integration can be numerically approximated using any one of several different techniques. In this chapter, we will present a technique for performing numerical integration using the trapezoidal rule.

trapezoidal rule

# Integration Using the Trapezoidal Rule

To use the analytical techniques of calculus to obtain the integral of a function over an interval, we must have an equation for the function. In many engineering and scientific applications, we have data points or measurements from the function, but we do not have an explicit equation. Therefore, we need a method that requires only points of the function to numerically compute the integral. In other applications, we may have an equation that defines the function, but it is difficult or impossible to determine the integral analytically. In this case, we would also like to have a method that allows us to compute points or values of the function and then numerically evaluate the integral. The technique that we present in this section is a simple way to numerically estimate the area under a curve, given points on the curve. The technique uses the areas of trapezoids and thus is called integration using the trapezoidal rule.

The integral of the function f(x), evaluated from a to b, is expressed as

![](bbox=[0.25, 0.87, 0.38, 0.91])

and represents the area under the function f(x) from x = a to x = b, as shown in Figure 6.14.