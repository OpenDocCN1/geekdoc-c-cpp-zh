+   - Secure Storage (IUMSecureStorageGet, IUMSecureStoragePut) allows Trustlets that have the Secure Storage capability (described earlier in the "Trustlet policy metadata" section) to store arbitrarily sized blobs and to retrieve them, either based on their unique Trustlet instance or by sharing the same collaboration ID as another Trustlet.

# Trustlet-accessible system calls

The Secure Kernel attempts to minimize its attack surface and exposure, it only provides a subset (less than 50) of the hundreds of system calls that a normal (VTL 0) application can use. These system calls are the strict minimum necessary for compatibility with the system DLLs that Trustlets use (refer to the section "Trustlet structure to see these), as well as the specific services required to support the RPC runtime (Rpcrt4.dll) and ETW tracing.

+   - Worker Factory and Thread APIs support this Thread Pool API (used by RPC) and TLS Slots used by the Loader.

+   - Process Information API supports this TLS Slots and Thread Stack Allocation.

+   - Event, Semaphore, Wait, and Completion APIs support Thread Pool and Synchronization.

+   - Advanced Local Procedure Call (ALPC) APIs support these Local RPC over the ncrpc transport.

+   - System Information API supports reading Secure Boot information, and NUMA system information for Kernel32.dll and Thread scaling, performance, and subsets of time information.

+   - Token API provides minimal support for RPC impersonation.

+   - Virtual Memory Allocation APIs support these allocations by the User-Mode Heap Manager.

+   - Section APIs support the Loader (for DLL Images) as well as the Secure Section functionality (once created/exposedthrough secure system calls shown earlier).

+   - Trace Control API supports this ETW.

+   - Exception and Continue API supports this Structured Exception Handling (SEH).

It should be evident from this list that operations as Device I/O, whether or on physical devices, is possible (there is no CreateFile API, to begin with), and is also the case for Registry I/O. Nor the creation of processes, or any graphs of complex API usage (there is no Win32.sys driver in VTL 1). As such, Trustlets are to be isolated with back-ends (in VTL 1) of their complex front-ends (with VTL 0), having ALPC as a communication mechanism, and exposed secure sections would have to have been communicated through ALPC. In Chapter 7 (Security), we'll look in more detail into the implementation of a specific Trustlet—Lsalho.exe, which provides Credential Guard.