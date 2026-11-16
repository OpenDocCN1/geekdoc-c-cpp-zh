
### 10.5.1 Sensitivity analysis of masonry structures

In the above we assumed that the loads are known (either prescribed, or specified as a function of the surface area of the masonry structure). We know multiple characterizations of when the structure is stable under these known loads. However, will the structure remain standing if the loads change (as can easily happen during, for instance, a snowstorm, wind storm, or earthquake)? Can bounds be proven guaranteeing that the structure remains standing, if the loads do not change by more than some tolerance? How must the structure be modified to improve its resilience to additional loads?

The main challenge to addressing changes in load is that there is no simple relationship between the loads and the internal forces (or the \(w_{ij}\)), thanks to static indeterminacy. Instead, if the structure can bear additional load, it usually can do so in infinitely many ways. A more complete understanding of the space of possible stresses that can bear a given load, and how that space changes as the loads change, remains elusive.

### 10.5.2 Progressive stable structures

The analysis presented in this chapter only applies to complete masonry structures. Of course, these must still be built one brick at a time, and the stability of the final structure does not in any way speak to the stability of the structure in a partial state (consider that an arch is unstable up until the keystone is placed). When can a masonry structure be built progressively, so that at every point the structure is stable? Can a design be modified to eliminate, or at least mitigate, the need for scaffolding or formwork? Some work in a similar vein [121] has looked at supporting blocks from above using chains attached to fixed vertical anchors, and where to place the anchors to minimize the number of chains that must be added or removed.

## III Applications in Computational Mechanics

![](img/4913dd83a2a14bc205a0a92cce102c82_214_0.png)

## Taylor & Francis

Taylor & Francis Group

http://taylorandfrancis.com

## Applications of Polyhedral Finite Elements in Solid Mechanics*

Joseph E. Bishop

Sandia National Laboratories, Albuquerque, USA

## CONTENTS

- 11.1 Introduction .................................................... 180
- 11.2 Governing equations of solid mechanics .................... 183
- 11.3 Polyhedral finite element formulation ....................... 184
- 11.3.1 Weak form of governing equations ........................ 185
- 11.3.2 Shape functions ........................................... 185
- 11.3.3 Element integration ....................................... 186
- 11.4 Rapid engineering analysis .................................. 187
- 11.5 Fragmentation modeling ...................................... 191
- 11.5.1 Fracture methodology ...................................... 192
- 11.5.2 Random Voronoi meshes ..................................... 193
- 11.5.3 Fragmentation ............................................. 194
- 11.6 Summary and outlook ......................................... 195

THE FINITE element method has revolutionized structural analysis since its inception over 50 years ago, by enabling the computer analysis of geometrically complex structures. The main requirement of the finite element method is that an appropriate partition, or mesh, of the structure to be created first. The elements of the partition typically have standard shapes, such as the hexahedron, pentahedron,

* Research support of Sandia National Laboratories is gratefully acknowledged. Sandia National Laboratories is a multimission laboratory managed and operated by National Technology and Engineering Solutions of Sandia, L.L.C., a wholly owned subsidiary of Honeywell International, Inc., for the U.S. Department of Energy’s National Nuclear Security Administration under contract DE-NA0003525.

![](img/4913dd83a2a14bc205a0a92cce102c82_216_0.png)

Figure 11.1 Example structure (a) with finite element meshes composed of standard element shapes: (b) hexahedral mesh, (c) tetrahedral mesh.

and tetrahedron. While this small library of standard element shapes is sufficient for many applications, there is a growing need for more general polyhedral shapes, ones that can have an arbitrary number of vertices, edges, and faces, and ones that can be non-convex. In this chapter, we discuss current and possible future applications of polyhedral finite elements in solid mechanics. These applications include rapid engineering analysis through novel meshing and discretization techniques, and fracture and fragmentation modeling. Several finite element formulations of general polyhedra have been developed. In this chapter we use a polyhedral formulation based on the use of harmonic shape functions. Harmonic shape functions are one example of several possible generalized barycentric coordinates, as discussed in Chapter 1.

### 11.1 INTRODUCTION

The analysis of stress and strain in a mechanical part or structure is critically important to the overall engineering design and development process. The finite element method has revolutionized analysis in solid mechanics by enabling the computer analysis of geometrically complex, nonlinear structures subjected to general loading conditions. Additionally, the finite element method can incorporate general material constitutive models, interface models, and constraints, making it an extremely versatile engineering analysis tool [41]. The main requirement of the finite element method is that an approximate partition, or mesh, of the domain be created first, as shown in Figure 11.1. This partition of the domain typically consists of standard finite element shapes, such as the hexahedron and tetrahedron, as shown in Figures 11.2(a) and 11.2(b), respectively. Once the finite element mesh is created, analyzing the response of the structure to applied loads can be obtained using standard computational techniques, starting with the weak form of the governing field equations of solid mechanics [41]. Figure 11.3 shows the stress field (von Mises) resulting from the application of torsional tractions to the I-beam shown in Figure 11.1. This type of structural analysis is now an indispensable tool in engineering practice.

![](img/4913dd83a2a14bc205a0a92cce102c82_217_0.png)

![](img/4913dd83a2a14bc205a0a92cce102c82_217_1.png)

While the small library of element shapes consisting of hexahedra, pentahedra, and tetrahedra is sufficient for many applications, there is a growing need to have access to finite element formulations for general polyhedral shapes, ones that can have an arbitrary number of vertices, edges, and faces (see Figure 11.2(c)). For additional flexibility, it is also desirable to have formulations that can handle warped polygonal faces and allow for non-convex shapes. (Note that the conventional formulation of the hexahedral finite element, using trilinear shape functions mapped from a parent element, allows for warped faces.) While several finite element formulations of general polyhedra now exist (see, for example, [27, 47, 322]), in this chapter a formulation based on harmonic shape functions is used. Harmonic shape functions are one example of several possible generalized barycentric coordinates, as discussed throughout this book. A different formulation for polyhedra, one that is based on the virtual element method, is given in Chapter 15.

A driving application for general polyhedral finite elements in solid mechanics is rapid engineering analysis. Despite several decades of research on mesh generation, the meshing process for geometrically complex shapes, though much advanced, is still time consuming and labor intensive. While automated tetrahedral meshing

![](img/4913dd83a2a14bc205a0a92cce102c82_218_0.png)

Figure 11.4. Conventional meshing techniques on a portion of an automotive cylinder head. The cylinder head contains a multitude of machine features such as holes, fillets, blends, and chamfers: (a) hybrid hexahedral/pentahedral mesh, (b) tetrahedral mesh. (Adapted from [45].)

technology seemingly circumvents the manual meshing process, there are still numerous heuristics involved with geometry defeaturing and cleanup, a priori mesh adaptation for minimization of solution error, and dimensional representations (e.g., beam versus shell versus continuum elements). The challenges in meshing realistic domains is shown in Figure 11.4. The automotive cylinder head has several geometric scales and numerous machine features such as holes, fillets, blends, and chamfers. Two examples of conventional meshing techniques are shown. Several possible uses of polyhedral finite elements to speed up the meshing process will be discussed in Section 11.4.

Another application of polyhedral finite elements is modeling pervasive fracture and fragmentation processes using dynamically changing mesh connectivity without remeshing [46, 49]. In this approach, fracture surfaces are allowed to nucleate and propagate only along inter-element faces. This is demonstrated in Figure 11.15 in which a quasi-brittle column impacts a rigid surface at an oblique angle. This technique for modeling fracture typically results in a type of mesh-dependency. The use of random polyhedral meshes can alleviate this mesh-dependency and restore a notion of convergence with mesh refinement. Details of this application and simulation are given in Section 11.5.

Additional advantages of polyhedral finite elements have been explored in modeling fluid dynamics using finite-volume techniques [207] and for topology optimization [390]. These applications will not be discussed here. The application of polyhedral finite elements for extremely large deformations in solid mechanics is discussed in Chapter 12.
