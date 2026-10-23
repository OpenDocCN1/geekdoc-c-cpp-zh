# Preface

There are many software packages used to solve partial differential equations (PDEs). However, because these packages are available as black boxes only, they often lack the flexibility required to improve the original physical, mathematical, or numerical model. This is why this book offers the user a completely open object-oriented framework to study and to adapt to his/her particular application. Indeed, the mathematical and numerical objects implemented here can be used not only in the present examples but also in many other problems in numerical modeling and engineering.

In particular, the book introduces advanced numerical methods such as adaptive finite elements and multigrid. Furthermore, it uses the powerful programming tools available in C++ to implement these methods in a transparent and well-debugged computer code.

For the sake of the present object-oriented implementation, there is a need to introduce briefly a few well-established topics in applied mathematics, numerical analysis, and programming. These topics are covered in much more detail in many other books. Still, the concise background provided here introduces the reader rather smoothly into the present problem area. This way, the book leads the reader along the entire solution process, from the original PDE, through the discretization stage, to the numerical solution of the resulting discrete system. The applications in the book stretch from image processing and cryptography to systems of nonlinear PDEs in 3-D adaptive meshes (Navier–Stokes, Maxwell, Helmholtz).

The book contains seven parts. The first and second parts introduce briefly the programming language and the object-oriented approach. The third and fourth parts introduce and implement finite differences and elements. The fifth part deals with numerical linear algebra and parallelism. The sixth and seventh parts use the present code to solve systems of nonlinear PDEs in two and three spatial dimensions, including the elasticity, Stokes, Navier–Stokes, Maxwell, and Helmholtz equations.

The new material in this second edition contains not just new applications but also a substantial extension of the original object-oriented framework to make it better understood and used. In particular, it contains:

+   - Part VII (Chapters 24–31) with the new three-dimensional applications,
+   - Chapter 23 with new applications in image processing,
+   - some philosophical remarks at the beginning of Chapter 4,
+   - new applications in cryptography at the end of Chapter 5,