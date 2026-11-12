Now that we know each of the fields available to us, we can expand on the ambitious “Do something...” section and implement something marginally less trivial:

```
#include "../common/book.h"

int main( void ) {
    cudaDeviceProp prop;

    int count;
    HANDLE_ERROR( cudaGetDeviceCount( &count ) );
    for ( int i=0; i< count; i++ ) {
        HANDLE_ERROR( cudaGetDeviceProperties( &prop, i ) );
        printf( " --- General Information for device %d ---\\n", i );
        printf( "Name:  %s\\n", prop.name );
        printf( "Compute capability:  %d.%d\\n", prop.major, prop.minor );
        printf( "Clock rate:  %d\\n", prop.clockRate );
        printf( "Device copy overlap:  " );
        if ( prop.deviceOverlap )
            printf( "Enabled\\n" );
        else
            printf( "Disabled\\n" );
        printf( "Kernel execution timeout :  " );
        if ( prop.kernelExecTimeoutEnabled )
            printf( "Enabled\\n" );
        else
            printf( "Disabled\\n" );

        printf( " --- Memory Information for device %d ---\\n", i );
        printf( "Total global mem:  %ld\\n", prop.totalGlobalMem );
        printf( "Total constant Mem:  %ld\\n", prop.totalConstMem );
        printf( "Max mem pitch:  %ld\\n", prop.memPitch );
        printf( "Texture Alignment:  %ld\\n", prop.textureAlignment );
}
```