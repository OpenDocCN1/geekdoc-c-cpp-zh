Which one is better suited in general is not so easy to say. However, it is obvious that both notations are much better than

```
apply_symm_blk2x2_rowmajor_dnsvec_multhr_athlon(L.data_addr, L.nrows,
L.ncols, L.ldim, L.blksch, v.data_addr, v.size);
```

which exposes lots of technical details and distracts from the principal tasks.

Developing software in that style is far from being fun. It wastes so much energy of the programmer. Even getting the function calls right is much more work than with a simple and clear interface. Slight modifications of the program—like using another data structure for some object—can cause a cascade of modifications that must be meticulously made. Remember that the person who implements the linear projection wants to do science, actually.

The cardinal error of scientific software providing such interfaces (we have seen even worse than our example) is to commit to too many technical details in the user interface. The reason lies partly in the usage of simpler programming languages such as C and Fortran 77 or in the effort to interoperate with software written in one those languages.

# Advice

If you ever are forced to write software that interoperates with C or Fortran, write your software first with a concise and intuitive interface in C++ for yourself and other C++ programmers and encapsulate the interface to the C and Fortran libraries so that it is not exposed to the developers.

It is admittedly easier to call a C or Fortran function from a C++ application than the other way around. Nonetheless, developing large projects in those languages is so much more inefficient that the extra effort for calling C++ functions from C or Fortran is absolutely justified. Stefanus Du Toit demonstrated in his _Hourglass API_ an example of how to interface programs in C++ and other languages through a thin C API [12].

The elegant way of writing scientific software is to provide the best abstraction. A good implementation reduces the user interface to the essential behavior and omits all unnecessary commitments to technical details. Applications with a concise and intuitive interface can be as efficient as their ugly and detail-obsessed counterparts.

Our abstractions here are linear operators and vector spaces. What is important for the developer is how these abstractions are used, in our case, how a linear operator is applied on a vector. Let’s say the application is denoted by the symbol * as in L * v or a * x. Evidently, we expect that the result of this operation yields an object of a vector type (thus, the statement w = L * v; should compile) and that the mathematical properties of linearity hold. That is all that developers need to know for using a linear operator.

How the linear operator is stored internally is irrelevant for the correctness of the program—as long as the operation meets all mathematical requirements and the implementation has no accidental side effect like overwriting other objects’ memory. Therefore, two different implementations that provide the necessary interface and semantic behavior are interchangeable; i.e., the program still compiles and yields the same results. The different implementations can of course vary dramatically in their performance. For that reason, it is important that choosing the best implementation for a target platform or a specific application can be achieved with little (or no) program modifications.