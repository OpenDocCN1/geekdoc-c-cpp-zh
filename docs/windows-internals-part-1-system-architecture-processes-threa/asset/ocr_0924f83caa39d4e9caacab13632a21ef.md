One page protection attribute PAGE_ENCLAVE_THREAD_CONTROL, which indicates the memory is for a Thread Control Structure (TCS) defined by SGX. Each TCS represents a different thread that can execute independently within the enclave.

NtLoadEnclaveData validates parameters and calls MiCopyPagesIntoEnclave to do the actual work, which may require getting committed pages as described earlier.

# Initializing an enclave

Now that the enclave has been created and data has been transferred into it, there is another last step to perform actual code in the enclave can execute. InitializeEnclave must be called to notify SGX that the enclave is in its final state before execution can. InitializeEnclave requires two SGX-specific structures to be passed in (SIGSTRUCT and EINITTOKEN; see the SGX documentation for the details).

The function NtInitializeEnclave called by InitializeEnclave does some parameter validation and makes sure the enclave VAD has the correct attributes and then passed the structures to the SGX hardware. Note that an enclave can only be initialized once.

The final step would be to use the Intel assembly ENTER to start code execution (again, see the SGX documentation for the details).

# Proactive memory management (SuperFetch)

Traditional memory management in operating systems has focused on the demand-paging model discussed far, with some advances in clustering and prefetching so that disk I/O can be optimized at the time of the demand-paging fault. Client versions of Windows, however, include a significant improvement in the management of physical memory with the implementation of SuperFetch, a memory management scheme that ensures the least-recently accessed approach with historical file information and proactive memory management.

The standby list management in older versions of Windows had two limitations. First, the prioritization of pages relies only on the recent past behavior of processes and does not anticipate their future memory requirements. The data used for prioritization is limited to the list of pages owned by a process at any given point in time. These shortcomings can result in scenarios in which the memory-intensive system application is left unattached for a period of time, during which a memory-intensive application (doing work as an antivirus or a diskragmentation) and then subsequent interactive application (or launch) to be sluggish. The same thing can happen when a user purposely runs a data- and/or memory-intensive application and returns to other programs, which appear to be significantly less responsive.

This decline in performance occurs because the memory-intensive application forces the code and data that active applications had cached to be overwritten by the memory-intensive activities—perform sluggishly as they request their data and from disk. Client versions of Windows take a big step toward resolving these limitations with SuperFetch.