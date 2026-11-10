# ### 15.6.2 Algorithm of PSO

The pseudocode of the Particle Swarm Optimization Algorithm is shown below:

```
```
Initialize the size of the particle swarm n
Initialize the positions and the velocities for
all the particles randomly
While end criterion false do
    t=t+1
    Compute fitness value of each particle
    x* = arg min_{i=1}^n (f(x*(t-1)), f(x_1(t)), f(x_2(t)),
    ......, f(x_n(t)));
    For i=1 to n
        x_i^#(t) = argmin_{i=1}^n (f(x_i^#(t-1)), f(x_i(t))
        textbfFor j=1 to Dimension
            Update the j-th dimension value of x_i and v_i
            v_{ij}(t+1) = wv_{ij}(t)+c_1r_1(x_{ij}(t)-x_{ij}(t))+c_2r_2(x_j^*(t)-x_{ij}(t))
            x_{ij}(t+1) = x_{ij}(t)+v_{ij}(t+1)
            v_{ij} = sign(v_{ij})min(|v_{ij}|, v_{max})
        End For
    End For
End While
```
```

# ### 15.6.3 Parameters and Tuning of Parameters in PSO

PSO does not require a large number of parameters to be initialized. The initialization process is quite simple. This section gives a list of parameters and initialization process of PSO.

+   - ***Number of particles:*** The number of particles is a very important factor to be considered. For most of the practical applications a best choice of the number of particles is typically in the range [20,40]. Usually 10 particles is a large number which is sufficient enough to get best results. In case of difficult problems the choice can be 100 or 200 particles also.
+   - ***Inertia Weight:*** The inertia weight plays a very important role in the convergence behavior of the PSO algorithm. The inertia weight is employed to control the impact of the previous history of velocities on the current one. Accordingly, the parameter w regulates the trade-off between the global (wide-ranging) and local (nearby) exploration abilities of the swarm. Too large an inertia weight aids in global exploration (searching wide ranging areas), while too small an inertia weight aids in local exploration (searching within the nearby areas). To obtain a balance between the global and local exploration the number of iterations required to locate the optimum solution are reduced. The inertia weight