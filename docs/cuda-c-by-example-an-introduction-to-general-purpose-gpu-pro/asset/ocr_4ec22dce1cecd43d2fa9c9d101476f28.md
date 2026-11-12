```
if (count != ELEMENTS)
    printf( "%d elements found in hash table. Should be %ld\n",
            count, ELEMENTS );
else
    printf( "All %d elements found in hash table.\n", count );

free( table.pool );
free( table.entries );
}
```

Since we chose to reuse our CPU implementation of verify_table(), we need a function to copy the table from GPU memory to host memory. There are three steps to this function, two relatively obvious steps and a third, trickier step. The first two steps involve allocating host memory for the hash table data and performing a copy of the GPU data structures into this memory with cudaMemcpy(). We have done this many times previously, so this should come as no surprise.

```
void copy_table_to_host( const Table &table, Table &hostTable ) {
    hostTable.count = table.count;
    hostTable.entries = (Entry**)calloc( table.count,
                                        sizeof( Entry*) );
    hostTable.pool = (Entry*)malloc( ELEMENTS *
                                    sizeof( Entry ) );

    HANDLE_ERROR( cudaMemcpy( hostTable.entries, table.entries,
                              table.count * sizeof( Entry*),
                              cudaMemcpyDeviceToHost ) );
    HANDLE_ERROR( cudaMemcpy( hostTable.pool, table.pool,
                              ELEMENTS * sizeof( Entry ),
                              cudaMemcpyDeviceToHost ) );
}
```

The tricky portion of this routine involves the fact that some of the data we have copied are pointers. We cannot simply copy these pointers to the host because they are addresses on the GPU; they will no longer be valid pointers on the host. However, the relative offsets of the pointers will still be valid. Every GPU pointer