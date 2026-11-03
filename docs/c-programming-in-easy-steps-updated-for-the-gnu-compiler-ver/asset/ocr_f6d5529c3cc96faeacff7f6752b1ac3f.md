**void abort( void )** Causes the program to end abnormally

**void exit( int status )** Causes the program to end normally. The value of status is returned to the system. Optionally, EXIT_SUCCESS and EXIT_FAILURE can be used to specify the status values

**int atexit( void ( *fcn ) ( void ) )** Registers the fcn function to be called when the program terminates. atexit() returns a non-zero value if unsuccessful

**int system( const char *s )** Passes the string s to the environment for processing. The return value is implementation-dependent

**char *getenv( const char *name )** Returns the environment string associated with name, or NULL if no string is associated with name in that environment. The details are implementation-dependent

**void *bsearch( const void *key , const void *base , size_t n , size_t size , int ( *cmp ) ( const void *keyval , const void *datum ) )** Searches base[0]...base[ n-1 ] for an item that matches key. It returns a pointer to the matching item if successful, otherwise it returns a NULL value. Items in the array base must be in ascending order

**void qsort( void *base , size_t n , size_t size , int ( *cmp ) ( const void * , const void * ) )** Sorts into ascending order an array base[0]...base[ n-1 ] of objects of size size. The comparison function cmp() is the same as that in the bsearch function

**int abs( int n )** Returns the absolute value of int n

**long labs( long n )** Returns the absolute value of long n

**div_t ldiv( long num , long denom )** Divides num by denom and stores the result as members of a structure of type ldiv_t. Its quot member stores the quotient result and its rem member stores the remainder result