Run the following nvprof command to gather global load efficiency and store efficiency metrics:

```
$ nvprof --devices 0 --metrics gld_efficiency,gst_efficiency ./simpleMathAoS
```

The results are summarized below. An efficiency of 50 percent indicates that both load and store memory requests are replayed for the AoS data layout. The fields x and y are adjacent in memory and have the same size, every time a memory transaction is performed to load the values of a particular field, exactly half of the bytes loaded must also belong to the other field. Thus, 50 percent of required load and store bandwidth is unused.

```
gld_efficiency    50.00%
gst_efficiency    50.00%
```

# Example: Simple Math with the SoA Data Layout

The following kernel is implemented using an AoS layer. Two 1D global memory arrays of primitives are allocated to store all for the two values, x and y. The kernel fetches the values by indexing into each primitive array.

```
__global void testInnerArray(InnerArray *data,
    InnerArray *result, const int n) {
unsigned int i = blockIdx.x + blockDim.x + threadIdx.x;

if (i<n) {
    float tmpx = data->x[i];
    float tmpy = data->y[i];

    tmpx += 10.0f;
    tmpy += 20.0f;
    result->x[i] = tmpx;
    result->y[i] = tmpy;
}
```

The input length is the same as the AoS test case, 1M:

```
#define LEN 1<<20
```

Allocate global memory with the following statements. That size(InnerArray) includes the size of its statically declared fields, x and y.

```
int nElem = LEN;
size_t nBytes = sizeof(InnerArray);

InnerArray *d_A, *d_C;
cudaMalloc((InnerArray **)&d_A, nBytes);
cudaMalloc((InnerArray **)&d_C, nBytes);
```

The main function for the SoA test is very similar to the main function in the previous simpleMathSoA.cu. You can download the full example code in simpleMathSoA.cu from Wrox.com. Compile the file with the following command and launch it.

```
$ nvcc -O3 -arch=sm_20 simpleMathSoA.cu -o simpleSoA
./simpleSoA
```