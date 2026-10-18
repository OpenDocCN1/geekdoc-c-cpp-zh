optimizations or introduce runtime overhead. Splitting up complex index computations into terms depending on different loop variables and moving them to outer loops also has a negative impact on performance. Even if in theory it would prevent unnecessarily repeating index computations in the inner-most loop, it prevents the compiler from recognizing memory access patterns.

Figure 19.1 shows a refactored variant of the kernel that uses the prescaled Hamiltonian and directly stores into sigma_out. Other variants accumulate the result in temporaries, or permute the j and k loops to cache the [k,j] accesses in temporary variables.

```
__kernel
void commutator_ocl_refactored_direct(__global real_t const* restrict sigma_in,
    __global real_t* restrict sigma_out,
    __global real_t const* restrict hamiltonian,
    const uint num, const uint dim,
    const real_t hbar, const real_t dt)
{
    // number of package to process == get_global_id(0)
    #define sig_real(i, j) (sigma_id + 2 * ((i) * dim + (j)))
    #define sig_imag(i, j) (sigma_id + 2 * ((i) * dim + (j)) + 1)

    #define ham_real(i, j) (2 * ((i) * dim + (j)))
    #define ham_imag(i, j) (2 * ((i) * dim + (k)) + 1)

    uint sigma_id = get_global_id(0) * dim * dim * 2;

    // compute commutator: (hamiltonian * sigma_in[sigma_id] - sigma_in[sigma_id] * hamiltonian)
    uint i, j, k;
    for (i = 0; i < dim; ++i)
    {
        for (j = 0; j < dim; ++j)
        {
            for (k = 0; k < dim; ++k)
            {
                sigma_out[sigma_real(i, j)] -= hamiltonian[ham_real(i, k)] * sigma_in[
                    sigma_real(k, j)];
                sigma_out[sigma_imag(i, j)] += sigma_in[sigma_real(i, k)] * hamiltonian[
                    ham_real(k, j)];
                sigma_out[sigma_imag(i, j)] += hamiltonian[ham_imag(i, k)] * sigma_in[
                    sigma_imag(k, j)];
                sigma_out[sigma_imag(i, j)] -= sigma_in[sigma_imag(i, k)] * hamiltonian[
                    ham_imag(k, j)];
                sigma_out[sigma_real(i, j)] += hamiltonian[ham_real(i, k)] * sigma_in[
                    sigma_imag(k, j)];
                sigma_out[sigma_imag(i, j)] -= sigma_in[sigma_real(i, k)] * hamiltonian[
                    ham_imag(k, j)];
                sigma_out[sigma_real(i, j)] += hamiltonian[ham_imag(i, k)] * sigma_in[
                    sigma_real(k, j)];
                sigma_out[sigma_real(i, j)] -= sigma_in[sigma_imag(i, k)] * hamiltonian[
                    ham_real(k, j)];
            }
        }
    }
```

# FIGURE 19.1

Refactored initial Hexciton OpenCL kernel. The arithmetic inside the loop maps to eight fused multiply-add instructions (FMA). The kernel prior to refactoring, and all others, are included in the downloadable examples. See the Readme for a mapping of figures and source files.