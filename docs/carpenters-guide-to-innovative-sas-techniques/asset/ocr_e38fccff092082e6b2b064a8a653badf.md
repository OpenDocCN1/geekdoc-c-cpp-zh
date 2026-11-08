The system option THREADS is used to allow SAS to take advantage of multiple CPUs. Although some of the documentation refers to the option in the singular, it needs to be THREADS. When multi-threads are used, a note is added to the LOG.

A number of Base SAS procedures, as well as several in SAS/STAT®, support multi-threaded operations. Additionally, support can also be found in some SAS Enterprise Miner® procedures and in some SAS/ACCESS® engines. Base procedures which have multi-threaded capabilities include: SORT, MEANS, SUMMARY, SQL, TABULATE, and REPORT.

Although the use of multiple threads will generally improve processing thru-put, this does not necessarily have to be the case. Since resources are used not only to create and maintain the threads, but also to coordinate the information flow between threads, it is possible that the use of these resources can outweigh the advantage of the multiple threads. It is important for you to test your environment with and without threads to determine which is the better performance. You should test with both THREADS and NOTHREADS and, depending on your data and code, determine which is more efficient.

When more than two CPUs are present on the system, you may not want all of them to be available for use by SAS. The system option, CPUCOUNT, is used to control how many of the available CPUs can be used by SAS.

# SEE ALSO

Additional information on multi-threading can be found on the SAS R&D site  
[http://support.sas.com/rnd/scalability/procs/index.html](http://support.sas.com/rnd/scalability/procs/index.html).