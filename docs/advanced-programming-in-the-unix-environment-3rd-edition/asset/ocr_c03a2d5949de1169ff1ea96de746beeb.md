that it was not blank, and then read the data record, which could be erased by _db_dodelete between the calls to _db_readidx and _db_readdat in db_nextrec.

20.2 Assume that db_nextrec calls _db_readidx, which reads the key into the index buffer for the process. This process is then stopped by the kernel, and another process runs. This other process calls db_delete, and the record being read by the other process is deleted. Both its key and its data are rewritten in the two files as all blanks. The first process resumes and calls _db_readdat (from db_nextrec) and reads the all-blank data record. The read lock by db_nextrec allows it to do the read of the index record, followed by the read of the data record, as an atomic operation (with regard to other cooperating processes using the same database).

20.3 With mandatory locking, other readers and writers are affected. Other reads and writes are blocked by the kernel until the locks placed by _db_writeidx and _db_writedat are removed.

20.5 By writing the data record before the index record, we protect ourselves from generating a corrupt record if the process should be killed in between the two writes. If the process were to write the index record first, but be killed before writing the data record, then we'd have a valid index record that pointed to invalid data.

# Chapter 21

21.5 Here are some hints. There are two places to check for queued jobs: the printer spooling daemon's queue and the network printer's internal queue. Take care to prevent one user from being able to cancel someone else's print job. Of course, the superuser should be able to cancel any job.

21.7 We don't need to prod the daemon, because we don't need to reread the configuration file until we need to print a file. The printer_thread function checks whether it needs to reread the configuration file before each attempt to send a job to the printer.

21.9 We need to null-terminate the string we write to the job file (recall that strlen doesn't include the terminating null byte when it calculates the length of a string). There are two simple approaches: either we can add 1 to the number of bytes we write, or we can use the dprintf function instead of calling sprintf and write.