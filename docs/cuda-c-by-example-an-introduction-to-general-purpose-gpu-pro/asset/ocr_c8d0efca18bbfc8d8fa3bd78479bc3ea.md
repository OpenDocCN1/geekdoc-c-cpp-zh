```
HANDLE_ERROR( cudaMemcpy( a, dev_a,
                    size * sizeof( *a ),
                    cudaMemcpyDeviceToHost ) );
}
HANDLE_ERROR( cudaEventRecord( stop, 0 ) );
HANDLE_ERROR( cudaEventSynchronize( stop ) );
HANDLE_ERROR( cudaEventElapsedTime( &elapsedTime,
                    start, stop ) );
HANDLE_ERROR( cudaFreeHost( a ) );
HANDLE_ERROR( cudaFree( dev_a ) );
HANDLE_ERROR( cudaEventDestroy( start ) );
HANDLE_ERROR( cudaEventDestroy( stop ) );
return elapsedTime;
}
```

As you can see, the buffer allocated by cudaHostAlloc() is used in the same way as a buffer allocated by malloc(). The other change from using malloc() lies in the last argument, the value cudaHostAllocDefault. This last argument stores a collection of flags that we can use to modify the behavior of cudaHostAlloc() in order to allocate other varieties of pinned host memory. In the next chapter, we'll see how to use the other possible values of these flags, but for now we're content to use the default, page-locked memory so we pass cudaHostAllocDefault in order to get the default behavior. To free a buffer that was allocated with cudaHostAlloc(), we have to use cudaFreeHost(). That is, every malloc() needs a free(), and every cudaHostAlloc() needs a cudaFreeHost().

The body of main() proceeds not unlike what you would expect.

```
#include "../common/book.h"

#define SIZE (10*1024*1024)

int main( void ) {
    float    elapsedTime;
    float    MB = (float)100*SIZE*sizeof(int)/1024/1024;
```