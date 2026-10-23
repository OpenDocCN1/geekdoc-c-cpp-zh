For example, the tensor product of the N × N matrices A and A′ produces the tensor

(A ⊗ A′)i,j,k,l ≡ ai,j a′k,l.

Furthermore, the tensor-matrix product is the analogue of the matrix-vector product. More precisely, just as the matrix-vector product produces a vector, the tensor-matrix product produces a matrix. For example,

(SA′)i,j ≡ Σk,l=1N Si,j,k,l a′k,l.

If, however, the original tensor is of six indices, then the tensor-matrix product produces a four-index tensor. For example,

(RA′)i,j,k,l ≡ Σm,n=1N Ri,j,k,l,m,n a′m,n.

There are a few possible ways to define the transpose of a tensor. In this discussion we use the following nonstandard definitions:

Ri,j,k,l,m,n^t ≡ Ri,j,m,n,k,l

and

Si,j,k,l^t ≡ Sj,i,k,l.

Note that, with the above definition, we have

S^t A′ = (SA′)^t.

We are now ready to reformulate the inverse problem in a concrete mathematical setting.

# 30.10 The Minimization Problem

The inverse problem is thus to minimize b, or to find a scalar e for which

b′(e) = 0.

To make this formula more explicit, let us use the chain rule (Sections 10.11, 12.5, and 28.5). In fact, the chain rule is used twice: the first time, to derive b:

b′ = ∇c w′ = w′ w′;

and the second time, to derive w:

w′ = ((∂A⁻¹/∂A) A′)(∂w(A⁻¹)/∂A⁻¹) = ((∂A⁻¹/∂A) A′) f.

where

(∂A⁻¹/∂A)i,j,k,l ≡ ∂Ai,j⁻¹/∂ak,l

is the Jacobian tensor that linearizes the inverse operator A⁻¹(A).