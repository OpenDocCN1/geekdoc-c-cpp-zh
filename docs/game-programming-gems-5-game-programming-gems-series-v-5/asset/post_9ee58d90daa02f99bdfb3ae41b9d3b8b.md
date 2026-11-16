
![](img/672fe9a2d008ba627b1991e15d70f43e_480_0.png)

First, we model an associated mesh from a cloth object. A suitable mesh is chosen that will have an adequate number of particles to allow the representation of the surface to be as smooth as possible.

Second, we calculate the normal vectors of the surface at each particle. We then obtain the internal and external forces applied to each particle and formulate the differential equation system as previously shown.

Finally, we resolve the system by applying an incremental interval of time, with which a new position of the mesh can be obtained. Repetition of these steps results in a real-time animation of the cloth system.

## Conclusion

We have proposed a model for realistic cloth animation. The advantage of the model resides in the simplicity of its implementation. The mesh representation is based on a familiar mass-spring system and provides an efficient computational system viable for computer game application.

By considering the behavior of cloth as quasi-elastic, rather than perfectly elastic, we increase the realism and avoid undesired effects such as super-elastic effects [Cordero01].

Furthermore, distinguishing between in-plane and out-of-plane forces produces a more accurate simulation, avoiding (for example) the appearance of bending forces when only shearing forces exist.

Figures 4.3.9 and 4.3.10 (see Color Plates 1A and 1B) have been generated using the proposed method.

![](img/672fe9a2d008ba627b1991e15d70f43e_481_0.png)

FIGURE 4.3.9 A flag flying.

![](img/672fe9a2d008ba627b1991e15d70f43e_481_1.png)

FIGURE 4.3.10 A cloth draping over a sphere.

Any future work proposed should strive to find the \( K(\xi) \) functions capable of simulating cloth more realistically. That is, to find the best parametric function \( K(\xi) \) and the value of its parameters, to minimize the error between the real motion of a cloth and its simulation. Also, the method we have presented uses a mesh of a rectangular cloth. Future models should strive toward the mesh representation of any cloth, independent of its form.

## References

- [Cordero01] Cordero, J.M., J. Matellanes, and J. Cortés. Corrección del Efecto Superelástico en Dinámica de Telas. XI Congreso Español de Informática Gráfica (CEIG'2001), Girona. pp:141–147. 2001.
- [House00] House, D.H. and D. E. Breen. Cloth Modeling and Animation. A K Peters, Ltd, 2000.
- [Kawabata75] Kawabata, S. The Standardization and Analysis of Hand Evaluation. Committee of the Textile Machinery Society of Japan, 1975.
- [Provot95] Provot, X. Deformation Constraints in a Mass-Spring Model to Describe Rigid Cloth Behavior. Graphics Interface '95 Proceedings, 147–154. Quebec, Canada, 1995.
- [Tospelas91] Tospelas, N. Animating the Coupling Behavior of Garments, 11–24. Proc. 2nd Eurographics Workshop on Animation and Simulation. Blackwell, UK, 1991.
- [Volino00] Volino, P., N. Magnenat-Thalmann. Virtual Clothing. Theory and Practice. Springer-Verlag, 2000.
- [Weil86] Weil, J. The Synthesis of Cloth Objects. Computer Graphics (Proc. Siggraph), 20:49–54, 1986.
- [Witkin90] Witkin, A., M. Gleicher, and W. Welch. Interactive Dynamics. Computer Graphics (Proc. Symposium on 3D Interactive Graphics), 24(2):11–21. 1990.

## Practical Animation of Soft Bodies for Game Development: The Pressurized Soft-Body Model

**Maciej Matyka, University of Wroclaw**
maq@panoramix.ift.uni.wroc.pl

In Computer Graphics (CG) research, a number of approaches for simulating soft bodies exist. Generally, these can be divided into two primary models: geometric and physically based. Fast and simple geometric models (known as *free form deformations* [Sedenberg86]) are not feasible in game development because of limited control. For purposes of realistic computer animation, other methods—particularly physically based—have been proposed.

Physically based application of the theory of elasticity gives a mathematically complicated and complex solution for the problem of soft body motion. Using finite volume methods [Irving04], we are able to simulate the behavior of viscoelastic bodies accurately. Unfortunately, use of these engineering methods results in non real-time animation, and is therefore inappropriate for games. Even classic computational fluid dynamics (CFD) found its place here; in [Nixon02] the authors build a model of compressible fluid enclosed by a mesh that introduces additional forces into the model. That approach is discussed further because of its similarity to our model of pressurized soft bodies. Note that the CFD approach is not considered here because it is not a real-time solution due to the complexity of solving the Navier-Stokes equations.

We will not go deeper into non-real-time soft body models. We mention them because it is important to know that more accurate and physically correct models exist in current CG research that may serve as basis for future game development application.

Several different approaches have been proposed for the application of real-time soft body simulation, but none of them seem to be particularly suitable for game development. Simple spring-mass (SM) models were introduced mostly because of their ease of implementation and computation speed (see [Lander03]). However, SM models do not generally yield very good realism, and increasing the number of springs with the hope of increasing realism does not automatically result in an ideal solution; it comes with its own problems. Using a large number of springs typically creates difficulties with the “stiffness” of the simulation. Also, animators working with SM models will have to play with a large number of physics constraints, which involves dubious changes to the simulation model (imagine an object with 1,500 springs and an animator attempting to anticipate the effect of changing the properties of a single spring).

## Simplified Spring Mass Models

Because of the problems with SM models in deformable body simulation, some modifications have been proposed to avoid introducing additional spring connections.

Consider the geometric object shown in Figure 4.4.1a. Its construction would be nearly useless in a typical SM simulation; running the simulation in the presence of gravity would cause the object to immediately collapse. We need some kind of internal system of forces that will keep the object stable. The easiest and most intuitive way to do that is to add supporting springs between all vertices in the object.

A model constructed in this manner is presented in Figure 4.4.1b. Such a model should behave reasonably well as a deformable body in a typical SM simulation. Note the addition of connections between all pairs of points. This means that for N points we will need to do N^2 spring calculations. This is really too much for objects composed of more than a few thousand vertices, and in fact, we are probably quite close to precluding real-time SM simulation altogether. By increasing the number of springs, we have also increased the difficulty of maintaining rigidity and managing unwanted internal motion. There are two ways to reduce this “stiffness” problem. One way is to use implicit integration that is applied for calculation of the motion equations (Baraff98). Another is to use inverse dynamics constraints as corrective measures for the explicit integration method [Lander03, Provot95]. Both methods would help to some degree, but they of course incur additional costs in processing speed.

![](img/672fe9a2d008ba627b1991e15d70f43e_485_0.png)

FIGURE 4.4.1 Typical Spring-Mass models showing a) a simple hull without internal support and b) a hull supported with internal connections.

These issues have been successfully avoided in computer graphics research involving models composed of simplified spring-mass constructions (see [Matyka03, Nixon02, Mesureu00]). Nixon et al. [Nixon02] build a three-dimensional mesh filled with compressible fluid, and they solve Navier-Stokes equations inside of the object. This approach seems to be an accurate and very interesting new idea for physically based models. Unfortunately, the solution is completely inappropriate for efficient real-time simulation because of the complexity of the solutions to the Navier-Stokes equations and the need to construct a time-dependent grid.

The fields of medical imaging and virtual reality have also delved into real-time deformable bodies and have produced very interesting results. Mesureur et al. [Mesureu00] claim that models composed only of springs are not visible for surgical applications because of the complexity of geometric construction for objects containing a large number of points. They built an SM mesh in the same way Nixon et al. did, but without filling the object with fluid. Instead, the object is filled with a “virtual rigid component.” The rigid component is called “virtual” because it does not interact with the simulation environment.

The idea of a virtual rigid component introduced by Mesureur et al. seems to be interesting for game development. However, one disadvantage is that it introduces some complications over the simple model. For example, the physics background of the model is somewhat abstruse. Of course, in results-oriented game development we are only interested in getting a good deformable body simulation, but when working with a model of physically based animation, we should be reasonably up to speed about the physics behind it.

## Physics behind the PSB Model

In the Pressurized Soft Body (PSB) model, we consider a geometric object consisting of a mesh made of nodes (mass material points) and spring connections (Hooke linear springs), as shown in Figure 4.4.1. We assume that the shape of the object is closed, which means that there are no holes (discontinuities) occurring in it. Because of the similarity to SM construction of cloth-like objects [Baraff98, Provot95], we generally consider it to be similar to an object sewn out of cloth.

To get deformable body behavior out of the “sewn cloth” object we introduce the PSB model. The basic idea is illustrated in Figure 4.4.2, in which a small pipe has been inserted into the object.

The pipe has been connected to a gas container. Inside the container, a gas with pressure \(P_c > 0\) exists. Because of the difference between the pressure inside the body (\(P_b = 0\)) and pressure inside the connected container (\(P_c > 0\)), gas will flow from the container to the object as long as \(P_c\) is not equal to \(P_b\). The pipe is then removed. After that, the simulation model will be slightly different from that shown in Figure 4.4.1. It will have been reshaped (expanded) due to the fact that the gas inside of it is under a pressure that exceeds that of the atmosphere (\(P_b > P_a\)).
