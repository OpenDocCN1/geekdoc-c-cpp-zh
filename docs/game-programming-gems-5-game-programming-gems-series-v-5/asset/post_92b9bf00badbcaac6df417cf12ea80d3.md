
## Conclusion

In this gem, depth impostors were used to render foliage. The power of the technique becomes obvious when the objects are in motion, as there are no popping artifacts, no obvious flat sprites turning, etc. We can obtain a high level of detail since the number of leaves perceived can easily surpass one million for an average forest canopy.

The algorithm presented can be used in vehicle and human scale simulators to render realistic looking trees and forests in real time. The technique takes full advantage of the programmable rendering pipeline available on recent graphics accelerators.

## References

- [Microsoft04] Microsoft Corporation. DirectX 9.0. Available online at http://www.msdn.com/directx/.
- [NVIDIA02] NVIDIA Corporation. Cg Language Toolkit. Available online at http://www.nvidia.com.
- [Puppo97] Puppo, E. and R. Scopigno. Simplification, LOD, and Multiresolution—Principles and Applications. Eurographics’97. Tutorial Notes, 1997.
- [Remolar03] Remolar, I., M. Chover, J. Ribelles, and Ó. Belmonte. View-Dependent Multiresolution Model For Foliage. 370–378. WSCG 2003, 2003.
- [Szijtó03] Szijtó, G. and K. József. High Resolution Foliage Rendering for Real-time Applications. Budmerice, Slovak Republic: SCCG, 2003.
- [Szijtó032] Szijtó, G. and K. József. High Resolution Foliage Rendering for Real-time Applications. Budapest, Hungary: GrafGeo, 2003.
- [Szijtó04] Szijtó, G. and K. József. Real-time Hardware Accelerated Rendering of Forest at Human Scale. Plzen, Czech Republic: WSCG 2004.
- [Szirmay95] Szirmay-Kalos, L. Theory of Three-Dimensional Computer Graphics. Budapest: Akadémia Kiadó, 1995. Available online at http://www.iit.bme.hu/~szirmay/book.html.

## 5.5 Gridless Controllable Fire

Neeharika Adabala, School of Computer Science, University of Central Florida nadabala@cs.ucf.edu

Charles E. Hughes, School of Computer Science and School of Film and Digital Media, University of Central Florida ceh@cs.ucf.edu

Gaming scenarios often involve fire: objects/vehicles/buildings on fire, torches of fire, fireplaces, etc. Fire is a phenomenon created by glowing combustion products in turbulent motion. Fire simulation techniques used in computer graphics usually involve solving the equations for dynamics of fluids on grids. These approaches are often computationally intensive and do not work in real time [Nguyen01]. Other approaches [Wei02] work in real time; however, they are based on computations on three-dimensional grids that introduce significant design issues in terms of choice of grid size, resolution, and position. For example, what should be done when a wind blows on a fire? Should a grid be defined so that it encompasses the whole region that may ever contain the fire or should it be designed to move _with_ the fire? In the latter case, knowledge of the possible regions the fire could flow into is required. Also, grid-based computations are often not guaranteed to be stable and relate to the resolution of the selected grid, adding to the complexity of applying these approaches. Thus, grid-based simulations of fire demand skillful choice of grid size, position, and resolution in every scenario that involves fire, which can be a tedious task.

In this chapter, we present a gridless technique for modeling fire, based on a stochastic Lagrangian process [Pop00]. In this approach, the equations for dynamics simulation define the trajectory of each particle. As a result, they can be directly evaluated to yield the position of each particle at successive time steps. The stochastic nature of the approach makes the computations relatively stable.

Most fires that are created in gaming scenarios are diffusion fires, or fires in which the oxidizer and fuel are not premixed (unlike the steady flame of a burner where the fuel and oxidizer are premixed). The fuel or object that is burning has to evaporate and come in contact with the oxidizer before it can burn. Since this process does not occur uniformly, fires flicker and exhibit a characteristic “jumping” behavior. Most of the existing approaches do not allow us to capture this distinctive property of fire. In this chapter, we present a simplified approach to modeling flickering fire in order to enhance realism. The work of Lamorlette and Foster [Lamorlette02] identifies the intermittent flame region in fire, but their model is designed for an offline production environment rather than real-time applications. In this chapter, the flickering of fire is captured by creating a simplified model for the “global extinction” behavior of fire. Global extinction refers to the moment when the combustion in the fire is so low that no flame is visible. Our technique also models “flame brushes,” which are regions of greater brightness in flames that occur in areas of the flame where there is higher rate of chemical reaction.

An additional issue in modeling of fire in games is the need to have parameters to control the appearance of fire. The approach presented in this chapter, enables control of the flicker rate, flame height, and number of flame regions in the fire. In addition to the simulation, a technique for real-time fire rendering that uses the programmability of graphics hardware is described.

Our fire model is presented in the next section. There are two main aspects to our model: the stochastic Lagrangian model for the dynamics and the chemical evolution model that represents the combustion accompanying the fire. The rendering of the model using programmable graphics hardware is then detailed. This is followed by a discussion with examples demonstrating the capabilities of the technique. Conclusions are given in the final section.

### Model of Fire

The key aspects that have to be modeled while simulating fire are turbulent dynamics and the chemical reaction accompanying them.

### Dynamics Model

The flow of hot gaseous products in a diffusion flame can be modeled as an incompressible turbulent flow. The equations that define this flow are the equation for conservation of mass, shown in Equation 5.5.1.

```
∇ · u = 0 (5.5.1)
```

and the Navier-Stokes equation, shown in Equation 5.5.2.

```
$$ \frac{D\mathbf{u}}{Dt} = -\frac{1}{\rho}\nabla p + \nu\nabla^2\mathbf{u} + \mathbf{F} $$ (5.5.2)
```

where \( D\mathbf{u}/Dt \) is the material derivative \( \partial/\partial t + u\partial/\partial x + v\partial/\partial y + w\partial/\partial z = \partial/\partial t + \mathbf{u} \cdot \nabla \), \( \mathbf{u} \) is the velocity field \( (u, v, w) \), \( p \) is the pressure, \( \nabla^2 \) is the Laplacian operator, \( \rho \) is the density, \( \nu \) is the coefficient of kinematic viscosity, and \( \mathbf{F} \) represents the external and body forces.

These equations can be solved by the *Eulerian approach*, where one solves for the vector fields that define the flow at fixed points of a grid, or by the *Lagrangian approach*, where one solves for the trajectory of a set of particles evolving in the flow. In the case of turbulent flow, the chaotic nature of the flow makes the problem of defining the size, shape, placement, and resolution of the grid tricky. Also grid-based techniques require significant insight into the expected behavior of the flow. For example, the grid should be shifted in the direction of an external wind field to keep the solutions on the grid points relevant. Because of these issues, we choose a Lagrangian approach because it is gridless.

When computations are applied for real-time simulations, they must be stable. Turbulent flows are chaotic and notoriously sensitive to small changes in initial conditions. Therefore, the stability of the computations cannot be guaranteed. However, this sensitivity of flow to small changes in initial conditions makes it suitable to stochastic modeling. The stochastic Lagrangian approach to maintain the gridless nature of the computations was used here. In this approach, the fluid flow is modeled by a set of particles whose statistical characteristics are the same as those of particles that evolve based on the equations of flow. These approaches are numerically more stable than the deterministic solutions to the equations.

The turbulent motion of the particles is simulated by using a stochastic Lagrangian approach. Equations 5.5.3 through 5.5.5 define the evolution of the *ith* particle in the simulation [Pope00].

```
\( d\mathbf{X}^{(i)} = \mathbf{U}^{(i)}dt \) (5.5.3)
```

```
\( d\mathbf{U}^{(i)} = \frac{3}{4}C_o\langle\mathbf{u}\rangle\mathbf{U}^{(i)}(t) - \langle\mathbf{U}\rangle dt + \sqrt{C_o k\langle\mathbf{w}\rangle}d\mathbf{W} \) (5.5.4)
```

```
\( d\omega^{(i)} = -(\omega^{(i)} - \langle\omega\rangle)C_s\langle\omega\rangle + \sqrt{(2\sigma^2\langle\omega\rangle^{(i)}C_s\langle\omega\rangle)}dW^* \) (5.5.5)
```

Equation 5.5.3 defines the position of a particle based on its velocity. The computation of velocity is based on the simplified Langevin model for stationary isotropic turbulence with constant density. The details of the derivation are beyond the scope of this chapter and can be found in the book on turbulent flows by Pope [Pope00]. The terms that are enclosed in \( \langle \rangle \) represent the local mean values of the enclosed variables. In combustion studies, they are evaluated by dividing the region occupied by
