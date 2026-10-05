data:

```
class fft_mkl{
private:
    int n;
    DFTI_DESCRIPTOR_HANDLE handle;
public:
    fft_mkl(int nin);
    ~fft_mkl(*f);
    void fwd(double *f){
        DftiComputeForward(handle, f);
    }
    void bwd(double *f){
        DftiComputeBackward(handle, f);
    }
};
```

Unlike the Vector and Matrix classes from before, fft_mkl is a narrowly defined class. It does just one thing, which is to provide an interface to MKL's FFT for complex one-dimensional data. It is typical of the way we use C++.

The class may be used as shown below to apply the FFT to a complex data of size n. It is assumed that v is of type double * pointing to 2n or more double locations.

```
for(int i=0; i < n; i++) {
    v[2*i] = rand()*1.0/RAND_MAX - 0.5;
    v[2*i+1] = rand()*1.0/RAND_MAX - 0.5;
}
```

```
fft_mkl fft(n);
fft.fwd(v);
```

The array v[] is initialized with uniformly distributed random numbers and its FFT is taken. All the details of the MKL library are cleanly hidden away.

The member functions fft_mkl::fwd() and fft_mkl::bwd() are defined completely within the class definition. These member functions correspond to (2.1) and (2.2), respectively.

The private data members of the class fft_mkl are n, for saving the dimension of the transform, and handle. The handle is initialized by the constructor and used