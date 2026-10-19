```
p = y[k] + h2*(-9.*F0 + 37.*F1 - 59.*F2 + 55.*F3)
    t[k + 1] = a + h*(k+1)                     # Next abscissa
    F4 = f(t[k+1], p)
    y[k+1] = y[k] + h2*(F1-5.*F2 + 19.*F3 + 9.*F4)   # Corrector
    F0 = F1
    F1 = F2
    F2 = F3
    F3 = f(t[k + 1], y[k + 1])
    return t,y

print(" k          t          Y numerical      Y exact")
t, y = ABM(A,B,n)
for k in range(0, n+1):
    print(" %3d %5.3f %12.11f %12.11f "
          % (k,t[k],y[k],(3.*exp(-t[k]/2.)-2.+t[k])))
    numsol.plot(pos = (t[k], y[k]))
    exsol.plot(pos = (t[k], 3.*exp(-t[k]/2.) -2. + t[k]))
```

# 8.7.1

# Assessment: rk2 vs. rk4 vs. rk45

While you are free to do as you please, unless you are very careful, we recommend that you not write your own rk4 or rk45 methods. You will be using this code for some high-precision work, and unless you get every fraction and method call just right, your code may appear to work well but still not give all the precision that you should be obtaining, and therefore we give you rk4, and rk45 codes to use. However, we do recommend that you write your own rk2, as doing so will make it clearer as to how the Runge–Kutta methods work, but without all the pain and danger.

+   1. Write your own rk2 method. Design your method for a general ODE; this means making the derivative function f(t,x) a separate method.
+   2. Use your rk2 solver in a program that solves the equation of motion (8.7) or (8.25). Plot both the position x(t) and velocity dx/dt as functions of time.
+   3. Once your ODE solver is running, do a number of things to check that it is working well and that you know what h values to use.
+      a) Adjust the parameters in your potential so that it corresponds to a pure harmonic oscillator (set p = 2 or a = 0). For an oscillator initially at rest, we have an analytic result with which to compare:
+         x(t) = A sin(ω₀ t),    v = ω₀ A cos(ω₀ t),    ω₀ = √(k/m).    (8.40)
+      b) Pick values of k and m such that the period T = 2π/ω is a nice number with which to work (something like T = 1).
+      c) Start with a step size h ≈ T/5 and make h smaller until the solution looks smooth, has a period that remains constant for a large number of cycles, and agrees with the analytic result. As a general rule of thumb, we suggest that you start with h ≈ T/100, where T is a characteristic time for the problem at hand. You should start with a large h so that you can see a bad solution turn good.