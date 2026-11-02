After the body of the header file has been read the first time during a compilation process, the macro _MYFILE_H_ is defined, thus the body will never be read again.

So far, macros are just constants. You will benefit from their full power when using macros with arguments. They are given in braces after the name of the macro, such as in

```
```
#define   MIN(x,y)   ( (x)<(y) ?  (x):(y) )
```
```

You do not have to worry more than usual about the names you choose for the arguments, there cannot be a conflict with other variables of the same name, because they are replaced by the expression you provide when a macro is used, e.g. MIN(4*a, b-32) will be expanded to (4*a)<(b-32) ? (4*a):(b-32).

The arguments are used in (  ) braces in the macro, because the comparison < must have the lowest priority, regardless of which operators are included in the expressions that are supplied as actual arguments. Furthermore, you should take care of unexpected side effects. Macros do not behave like functions. For example, when calling MIN(a++,b++) the variable a or b may be increased twice when the program is executed. It is usually better to use inline functions (or sometimes templates in C++) in such cases. But there are many applications of macros, which cannot be replaced by inline functions, like in the following example, which closes this section.

The example illustrates how a program can be written in a clear way using macros, making the program less error-prone, and furthermore allowing for a broad applicability. A system of Ising spins is considered, i.e., a lattice where at each site i a particle σ_i is placed. Each particle can have only two states σ_i = ±1. It is assumed that all lattice sites are numbered from 1 to N. This is different from C arrays, which start at index 0. The benefit of starting with index 1 for the sites is that, for many simulations of Ising systems, one needs the site 0 for additional technical reasons, see below. For the simplest version of the model only neighbors of spins are interacting. With a two-dimensional square lattice of size N = L × L a spin i, which is not at the boundary, interacts with spins i + 1 (+x-direction), i − 1 (−x-direction), i + L (+y-direction), and i − L (−y-direction). A spin at the boundary may interact with fewer neighbors when free boundary conditions are assumed. With periodic boundary conditions (pbc), all spins have exactly 4 neighbors. In this case, a spin at the boundary interacts