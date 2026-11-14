```
static __global__ void nUpp_kernel(double *Vnl,
        /* </ beta1_i|nk > */
        doubleComplex *beta1,
        /* </ beta1_f|V|n'i > */
        cuDoubleComplex *VnlBeta1u,
        int nion,
        int N1,
        int num
        )
{
    __shared__ Vol_s[M_W*L];
    cuDoubleComplex VnlBeta1_local;

    //// one block per ion
    for (i = blockIdx.x; i < nion; i+=gridDim.x){
        for (j = threadIdx.x; j < M_W*L; j+=blockDim.x){
            Vol_s[j] = Vol[j * i * M_W + L];
            __syncthreads();
        }
    }

    //// one thread per projection
    for (j = threadIdx.x; j < M_L*num; j += blockDim.x){
        int i = blockIdx.x;
        VolBeta1_local = 0;
        for (l2 = 0; l2 < M_W; l2++){(
            VnlBeta1_local += Vnl[l2*N1+l12] * beta1[l2 + i*M_L + (j/M_L)*nion*N1*L];
        }
        VnlBeta1u[i1 + i*M_L + (j/M_L)*nion*N1*L] = VnlBeta1_local;
    }
}
```

# Listing 4 Nonlocal potential kernel

```
static __global__ void square_sum_kernel(cuDoubleComplex *u_r,
        double *rho,
        double *occ,
        int size,
        int num
        )
{
    const int idx = threadIdx.x + blockIdx.x * blockDim.x;
    const int nthreads = blockDim.x * gridDim.x;
    double rho_l;
    for (i = idx; i < size; i+=nthreads){
        rho_l = 0.;
        for (j = threadIdx.y; j < num; j+= blockDim.y){
            rho_l += occ[j] *
            ( u_r[i+j*size].x * u_r[i+j*size].x +
            u_r[i+j*size].y * u_r[i+j*size].y );
        }
        atomicAdd(rho + i, rho_l);
    }
}
```

# Listing 5 Density accumulation kernel