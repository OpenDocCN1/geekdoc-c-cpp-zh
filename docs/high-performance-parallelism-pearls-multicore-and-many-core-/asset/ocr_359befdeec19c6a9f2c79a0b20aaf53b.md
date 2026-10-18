+   - Zheng, Y., Kamil, A., Driscoll, M.B., Shan, H., Yelick, K., 2014. UPC++: a PGAS extension for C++. In: 2014 IEEE 28th International Parallel and Distributed Processing Symposium, May, pp. 1105-1114.

Download the code from this, and other chapters, http://lotsofcores.com.

# TILED hStreams MATRIX MULTIPLIER EXAMPLE SOURCE

```
```cpp
#include <stdio.h>
#include <math.h>
#include <mkl.h>
#include <hStreams_source.h> // <---hStreams Core API
#include <hStreams_app_api.h> // <---hStreams App API
typedef double MATRIX_TYPE;
void randomInit(MATRIX_TYPE *data,int size) { for(int i=0;i<size;++i) {
    data[i]=rand() / (MATRIX_TYPE)RAND_MAX;
} }
int main() { // compile and link with $ icpc app1ls.cpp -lhstreams_source -mkl
    HSTREAMS_options hstreams_options; // <---hStreams
    int partitions = 4; // computing partitions per card
    int max_log_str = 4; // number of logical hstreams: can be bigger
    int nIter=3, blocksize = 128; // run 3 times, 1st run is slow owing to MKL init
    int numRowsA=512,numColsA=1024,numColsC=5120;
    int numRowsB=numColsA,numColsB=numColsC,numRowsC=numRowsA;
    int Aindex, Bindex, Cindex;
    const MATRIX_TYPE alpha = 1.0; const MATRIX_TYPE beta = 1.0;
    hStreams_GetCurrentOptions(&hstreams_options, sizeof(hstreams_options));
    hstreams_options.verbose = 0;
    hstreams_options.domains_limit = 256; // Limit to 256 domains
    hStreams_options(&hstreams_options); // <---hStreams
    int mblocks = (int)numRowsA/blocksize;
    int kblocks = (int)numColsA/blocksize;
    int nblocks = (int)numColsC/blocksize;
    int totalblocks_A = mblocks * kblocks;
    int totalblocks_B = kblocks * nblocks;
    int totalblocks_C = mblocks * nblocks;
    unsigned int size_A = numColsA * numRowsA;
    unsigned int size_B = numColsB * numRowsB;
    unsigned int size_C = numColsC * numRowsC;
    // allocate host memory for matrices A and B and C
    MATRIX_TYPE *h_A = new MATRIX_TYPE[size_A];
    MATRIX_TYPE *h_B = new MATRIX_TYPE[size_B];
    MATRIX_TYPE *h_C = new MATRIX_TYPE[size_C];
    MATRIX_TYPE *reference = new MATRIX_TYPE[size_C];
    MATRIX_TYPE** h_Ablock = new MATRIX_TYPE*[totalblocks_A];
    MATRIX_TYPE** h_Bblock = new MATRIX_TYPE*[totalblocks_B];
    MATRIX_TYPE** h_Cblock = new MATRIX_TYPE*[totalblocks_C];
```
```