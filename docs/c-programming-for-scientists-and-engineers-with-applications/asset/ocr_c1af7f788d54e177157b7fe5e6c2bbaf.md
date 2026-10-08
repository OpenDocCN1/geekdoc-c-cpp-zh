# 7.6 Sample Programs

# 421

# Method

Define the constants $ho$ and $\mu$ for air.
Vary the velocity from 100 to 1000 in increments of 100.
Calculate the Reynolds number for each velocity.
Store the velocity and the Reynolds number in one-dimensional arrays.

# Data

Density $ho$ of air $2.33 	imes 10^{-3}$ slug/ft$^3$
Viscosity $\mu$ for air $3.8 	imes 10^{-7}$ slug/ft.sec.
Velocity varies from 100 to 1000 at increments of 100

# Pseudocode

```
density $ho$ and viscosity $\mu$ for air are defined constants\for each velocity from 100 to 1000 in increments of 100
reynolds = (density * velocity * length) / viscosity
ynoldsnum[i] = reynolds
end\for each velocity from 100 to 1000 in increments of 100
Output velocity, reynoldsnum[i]
end
stop
```

# Program

> /**********************************************************************/
/* /
/* Compute the Reynolds Numbers for Different Velocities */
/* of Fluid Flow over a Circular Cylinder */
/* /
/***********************************************************************/
/* /
/* Constants:
/* density = $2.33 \times 10^{-3}$ slug/ft */
/* viscosity = $3.8 \times 10^{-7}$ slug/(ft.sec) */
/* /
/* Input Variables: */