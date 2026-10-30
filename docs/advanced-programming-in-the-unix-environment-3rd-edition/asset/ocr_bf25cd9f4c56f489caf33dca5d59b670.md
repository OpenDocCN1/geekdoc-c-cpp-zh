```
struct sembuf {
    unsigned short  sem_num;  /* member # in set (0, 1, ..., nsems-1) */
    short           sem_op;   /* operation (negative, 0, or positive) */
    short           sem_flg;  /* IPC_NOWAIT, SEM_UNDO */
};
```

The nops argument specifies the number of operations (elements) in the array.

The operation on each member of the set is specified by the corresponding sem_op value. This value can be negative, 0, or positive. (In the following discussion, we refer to the “undo” flag for a semaphore. This flag corresponds to the SEM_UNDO bit in the corresponding sem_flg member.)

+   1. The easiest case is when sem_op is positive. This case corresponds to the returning of resources by the process. The value of sem_op is added to the semaphore’s value. If the undo flag is specified, sem_op is also subtracted from the semaphore’s adjustment value for this process.

+   2. If sem_op is negative, we want to obtain resources that the semaphore controls.
+   If the semaphore’s value is greater than or equal to the absolute value of sem_op (the resources are available), the absolute value of sem_op is subtracted from the semaphore’s value. This guarantees the resulting semaphore value is greater than or equal to 0. If the undo flag is specified, the absolute value of sem_op is also added to the semaphore’s adjustment value for this process.
+   If the semaphore’s value is less than the absolute value of sem_op (the resources are not available), the following conditions apply.

+   a. If IPC_NOWAIT is specified, semop returns with an error of EAGAIN.

+   b. If IPC_NOWAIT is not specified, the semcnt value for this semaphore is incremented (since the caller is about to go to sleep), and the calling process is suspended until one of the following occurs:

+   i. The semaphore’s value becomes greater than or equal to the absolute value of sem_op (i.e., some other process has released some resources). The value of semcnt for this semaphore is decremented (since the calling process is done waiting), and the absolute value of sem_op is subtracted from the semaphore’s value. If the undo flag is specified, the absolute value of sem_op is also added to the semaphore’s adjustment value for this process.

+   ii. The semaphore is removed from the system. In this case, the function returns an error of EIDRM.

+   iii. A signal is caught by the process, and the signal handler returns. In this case, the value of semcnt for this semaphore is decremented (since the calling process is no longer waiting), and the function returns an error of EINTR.

+   3. If sem_op is 0, this means that the calling process wants to wait until the semaphore’s value becomes 0.