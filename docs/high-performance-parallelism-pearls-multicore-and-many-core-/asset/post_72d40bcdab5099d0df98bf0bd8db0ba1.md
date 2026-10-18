
- OpenCL SYCL, cross-platform abstraction layer. Available from: https://www.khronos.org/opencl/sycl.
- Parallel computing (MARE). Available from: https://developer.qualcomm.com/mobile-development/maximize-hardware/parallel-computing-mare.
- PCIe. Available from: https://www.pcisig.com/specifications/pciexpress.
- Duran, A., 2011. OmpSs: a proposal for programming heterogeneous multicore architectures. Parallel Process. Lett. 21 (2), 173-193.
- Unat, D., Chan, C., Zhang, W., Bell, J., Shalf, J., 2013. Tiling as a durable abstraction for parallelism and data locality. In: Workshop on Domain-Specific Languages and High-Level Frameworks for High Performance Computing.
- Bauer, M., Treichler, S., Slaughter, E., Aiken, A., 2012. Legion: expressing locality and independence with logical regions. In: Proceedings of the International Conference on High Performance Computing, Networking, Storage and Analysis, SC '12, Los Alamitos, CA, USA. IEEE Computer Society Press, pp. 66:1-66:11.
- Bianchi, L., Dorigo, M., Gambardella, L.M., Gutjahr, W.J., 2009. A survey on metaheuristics for stochastic combinatorial optimization. Nat. Comput. 8 (2), 239-287. Available from: http://dx.doi.org/10.1007/s11047-008-9098-4.
- Borges, L., 2012. Experiences in developing seismic imaging code for Intel Xeon Phi Coprocessor. http://software.intel.com/en-us/blogs/2012/10/26/experiences-in-developing-seismic-imaging-code-for-intel-xeon-phi-coprocessor.
- Chamberlain, B.L., Callahan, D., Zima, H.P., 2007. Parallel programmability and the Chapel language. Int. J. High Performance Comput. Appl. 21 (3), 291-312.
- Garland, M., Kudlur, M., Zheng, Y., 2012. Designing a unified programming model for heterogeneous machines. In: Proceedings of the International Conference on High Performance Computing, Networking, Storage and Analysis, SC '12, Los Alamitos, CA, USA. IEEE Computer Society Press, pp. 11.
- Heroux, M.A., Bartlett, R.A., Howle, V.E., Hoekstra, R.J., Hu, J.J., Kolda, T.G., Lehoucq, R.B., Long, K.R., Pawlowski, R.P., Phipps, E.T., Salinger, A.G., Thornquist, H.K., Tuminaro, R.S., Willenbring, J.M., Williams, A., Stanley, K.S., 2005. An overview of the Trilinos Project. ACM Trans. Math. Softw. 31 (3), 397-423.
- Jeannot, E., 2012. Performance analysis and optimization of the tiled Cholesky factorization on NUMA machines. In: PAAP 2012-IEEE International Symposium on Parallel Architectures, Algorithms and Programming.
- Kale, L.V., Krishnan, S., 1993. Charm++: a portable concurrent object oriented system based on C++. In: Proceedings of the Eighth Annual Conference on Object-Oriented Programming Systems, Languages, and Applications, OOPSLA '93, New York, NY, USA, ACM. pp. 91-108.
- Kim, W., Voss, M., 2011. Multicore desktop programming with Intel threading building blocks. IEEE Softw. 28 (1), 23-31.
- Nieplocha, J., Palmer, B., Tipparaju, V., Krishnan, M., Trease, H., Apra, E., 2006. Advances, applications and performance of the global arrays shared memory programming toolkit. Int. J. High Performance Comput. Appl. 20 (2), 203-231.
- OpenMP Language Working Group. OpenMP Technical Report 3 on OpenMP 4.0 enhancements, 2014. Available from: http://openmp.org/TR3.pdf.
- Trefethen, L.N., Bau III, D., 1997. Numerical Linear Algebra. SIAM.
- Zheng, Y., Kamil, A., Driscoll, M.B., Shan, H., Yelick, K., 2014. UPC++: a PGAS extension for C++. In: 2014 IEEE 28th International Parallel and Distributed Processing Symposium, May, pp. 1105-1114.

Download the code from this, and other chapters, http://lotsofcores.com.

## TILED hStreams MATRIX MULTIPLIER EXAMPLE SOURCE

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
    unsigned int mem_size_Ablock = sizeof(MATRIX_TYPE) * size_A/totalblocks_A;
    unsigned int mem_size_Bblock = sizeof(MATRIX_TYPE) * size_B/totalblocks_B;
    unsigned int mem_size_Cblock = sizeof(MATRIX_TYPE) * size_C/totalblocks_C;
    //the second arg is logStrPerPartition! not perCard
    int iret = hStreams_app_init(partitions, 1); // <---- hStreams
    if( iret != 0 ) { printf("hstreams_app_init failed!\r\n"); exit(-1); }
    //malloc & initialize blocks of A/B/C on host and device
    for (int i = 0; i < totalblocks_A; ++i) {
        h_Ablock[i] = new MATRIX_TYPE[size_A/totalblocks_A];
        hStreams_app_create_buf((void*)h_Ablock[i], mem_size_Ablock); // <---- hStreams
        randomInit(h_Ablock[i], size_A/totalblocks_A);
    }
    for (int i = 0; i < totalblocks_B; ++i) {
        h_Bblock[i] = new MATRIX_TYPE[size_B/totalblocks_B];
        hStreams_app_create_buf((void*)h_Bblock[i], mem_size_Bblock); // <---- hStreams
        randomInit(h_Bblock[i], size_B/totalblocks_B);
    }
    // Create buffers on the card
    for (int i = 0; i < totalblocks_C; ++i) {
        h_Cblock[i] = new MATRIX_TYPE[size_C/totalblocks_C];
        hStreams_app_create_buf((void*)h_Cblock[i], mem_size_Cblock); // <---- hStreams
    }
    // Assemble full size matrices A & B for host compute check for comparison purposes
    for (int i = 0; i < kblocks; i++) {
        for (int k = 0; k < numRowsB/kblocks; k++) {
            for (int j = i*nblocks; j < (i+1)*nblocks; j++) {
                for (int l = 0; l < numColsB/nblocks; l++) {
                    Bindex = numColsB*(i*numRowsB/kblocks+k)+((j-i*nblocks)*numColsB/nblocks+l);
                    h_B[Bindex] = h_Bblock[j][l + k*numColsB/nblocks];
                }
            }
        }
    }
    for (int i = 0; i < mblocks; i++) {
        for (int k = 0; k < numRowsA/mblocks; k++) {
            for (int j = i; j <= i + (mblocks)*(kblocks-1); j = j + mblocks) {
                for (int l = 0; l < numColsA/kblocks; l++) {
                    Aindex = numColsA*(i*numRowsA/mblocks+k)+(((j-i)/mblocks)*numColsA/kblocks+l);
                    h_A[Aindex] = h_Ablock[j][l + k*numColsA/kblocks];
                }
            }
        }
    }
    HSTR_EVENT *eventAcpy = new HSTR_EVENT[totalblocks_A]; // <---- hStreams
    HSTR_EVENT *eventBcpy = new HSTR_EVENT[totalblocks_B]; // <---- hStreams
    HSTR_EVENT *eventCcpy = new HSTR_EVENT[totalblocks_C]; // <---- hStreams
    HSTR_EVENT *eventCset = new HSTR_EVENT[totalblocks_C]; // <---- hStreams
    for (int iter = 0; iter < nIter; iter++) { // do multiple runs on device & 1st use MKL slow
        int qindex; int cblock_index = 0; int countA = -1, countB = -1;
        div_t divresult1, divresult2;
        // Memset h_Cblock to zero initially
        for (int i = 0; i < totalblocks_C; ++i) {
            hStreams_app_memset(h_Cblock[i], 0, mem_size_Cblock, (i%max_log_str), &eventCset[i]); // <---- hStreams
        }
        while (countA < totalblocks_A-1 || countB < totalblocks_B-1) {
            if ((countA <= countB || countB == totalblocks_B-1) && (countA < totalblocks_A-1)) {
                countA++;
```
