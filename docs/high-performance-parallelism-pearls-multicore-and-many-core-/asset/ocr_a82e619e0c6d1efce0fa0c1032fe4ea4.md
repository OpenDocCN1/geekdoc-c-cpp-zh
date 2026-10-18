# PyFR

The PyFR framework is the other full application we are going to explore in this chapter. It uses pyMIC in a different way to integrate the coprocessor into applications using the PyFR framework.

# OVERVIEW

PyFR is an open-source Python framework for solving advection-diffusion problems of the form

∂u/∂t + ∇·f(u,∇u) = S(x,t) (14.13)

where u(x,t) is a state vector representing the solution, f a flux function, and S a source term. A prominent example of an advection-diffusion type problem are the compressible Navier-Stokes equations of fluid dynamics. PyFR is based around the flux reconstruction (FR) approach of Huynh. In FR, the computational domain of interest is first discretized into a mesh of conforming elements. Inside of each element, two sets of points are defined: one in the interior of the element, commonly termed the solution points, and another on the boundary of the element, termed the flux points.

The objective of FR is to obtain an approximation of ∇·f that sits in the same polynomial space as the solution which can be used to march forwards in time. Accomplishing this requires two kinds of distinct operations (i) moving quantities between flux/solution points, and (ii) evaluating quantities (such as f) at either individual solution points or pairs of flux points. When moving quantities, say from the solution points to the flux points, the value at each flux point is given as a weighted sum of the quantity at each solution point

q_{e,i}^{(f)} = Σ_j α_{e,i j} q_{e,j}^{(u)} (14.14)

where q represents the quantity, e the element number, i the flux point number, and α_{e,i j} is a matrix of coefficients that encodes the numerics. This can be identified as a matrix-vector product; or in the case of an N-element simulation, N matrix-vector products. If the quantities are first mapped from physical space to a reference space then the α_{e,i j} coefficients become identical for each element of a given type. Hence, the above operation can be reduced to a single matrix-matrix product. Depending on the order of accuracy, PyFR spends between ~50% and ~85% of the wall clock time performing such multiplications. The remaining time is spent in the point-wise operations. These kernels are a generalization on the form f(in1[i], in2[i], ..., &out1[i]). As there are no data dependences between iterations, the point-wise kernels are both trivial to parallelize and highly bound by available memory bandwidth.

# RUNTIME CODE GENERATION

PyFR aims to support a variety of modern hardware platforms. While the matrix multiplications can be offloaded to a vendor supplied BLAS library, the point-wise operations must be coded up once for each key platform. This presents both a barrier to entry with respect to adding new physics into the code and further represents a significant maintenance burden. To avoid this, the point-wise kernels in PyFR are specified in a C-like domain-specific language built on top of the Mako template engine. The language exploits the fact that—at least for point-wise operations—the major parallel programming languages