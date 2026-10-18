```
```c
MPI_Win_lock_all(MPI_MODE_NOCHECK, win);
for (i=0;i<reps;i++) {
    for (j=0; j<n_partners; j++) {
        if (partners_map[j] == MPI_UNDEFINED) {
            MPI_Irecv (my_buf +offset, len, MPI_BYTE,
                       partner, i, MPI_COMM_WORLD, rq++);
            MPI_Isend (exch_buf + offset, len, MPI_BYTE,
                       partner, i, MPI_COMM_WORLD, rq++);
        } else {
            memcpy (my_buf + offset, partners_ptrs[j]+offset,
                    len);
        }
        offset += len;
    }
    if (n_node_partners > 0) {
        MPI_Win_sync(win);
        MPI_Barrier( shmcomm );
        MPI_Win_sync(win);
    }
    if (n_inter_partners > 0) {
        MPI_Waitall(2*n_inter_partners, reqs,
                    MPI_STATUS_IGNORE);
    }
}
MPI_Win_unlock_all(win);
```
```

# FIGURE 16.7

Communication scheme based on `MPI_Win_lock_all` and `MPI_Win_unlock_all`, which are called just once per test.