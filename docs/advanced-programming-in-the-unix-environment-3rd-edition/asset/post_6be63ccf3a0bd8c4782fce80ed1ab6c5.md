
1. Write *nrec* records to the database.
2. Read the *nrec* records back by key value.
3. Perform the following loop *nrec × 5* times.
   a. Read a random record.
   b. Every 37 times through the loop, delete a random record.
   c. Every 11 times through the loop, insert a new record and read the record back.
   d. Every 17 times through the loop, replace a random record with a new record. Every other one of these replacements is a record with the same size data; the alternate is a record with a longer data portion.
4. Delete all the records that this child wrote. Every time a record is deleted, ten random records are looked up.

The number of operations performed on the database is counted by the cnt_xxx variables in the DB structure, which were incremented in the functions. The number of operations differs from one child to the next, since the random-number generator used to select records is initialized in each child to the child’s process ID. A typical count of the operations performed in each child is shown in Figure 20.6.

| Operation | Calls to fcnt1 (per operation) — Coarse-grained locking | Calls to fcnt1 (per operation) — Fine-grained locking | Operation count (*nrec* = 2,000) |
|---|---:|---:|---:|
| db_store, DB_INSERT, no empty record, appended | 2 | 8 | 2,920 |
| db_store, DB_INSERT, empty record reused | 2 | 4 | 468 |
| db_store, DB_REPLACE, different data length, appended | 2 | 8 | 405 |
| db_store, DB_REPLACE, equal data length | 2 | 2 | 416 |
| db_store, record not found | 2 | 2 | 71 |
| db_fetch, record found | 2 | 2 | 32,873 |
| db_fetch, record not found | 2 | 2 | 2,966 |
| db_delete, record found | 2 | 4 | 3,388 |
| db_delete, record not found | 2 | 2 | 422 |

We performed about ten times more fetches than stores or deletions, which is probably typical of many database applications.

Each child is performing these operations (fetching, storing, and deleting) only with the records that the child wrote. The concurrency controls are being exercised because all the children are operating on the same database (albeit different records in the same database). The total number of records in the database increases in proportion to the number of children. (With one child, *nrec* records are originally written to the database. With two children, *nrec × 2* records are originally written, and so on.)

To test the concurrency provided by coarse-grained locking versus fine-grained locking and to compare the three types of locking (no locking, advisory locking, and mandatory locking), we ran three versions of the test program. The first version used the source code shown in Section 20.8, which we’ve called fine-grained locking. The second version changed the locking calls to implement coarse-grained locking, as described in Section 20.6. The third version had all locking calls removed, so we could measure the overhead involved in locking. We can run the first and second versions (fine-grained locking and coarse-grained locking) using either advisory or mandatory locking, by changing the permission bits on the database files. (In all the tests reported in this section, we measured the times for mandatory locking using only the implementation of fine-grained locking.)

All the timing tests in this section were done on an Intel Core-i5 system running Linux 3.2.0. This system has four cores, which allows up to four processes to run concurrently.

## Single-Process Results

Figure 20.7 shows the results when only a single child process ran, with an nrec of 2,000, 6,000, and 12,000.

| nrec | No locking: User | No locking: Sys | No locking: Clock | Advisory locking: Coarse-grained locking: User | Advisory locking: Coarse-grained locking: Sys | Advisory locking: Coarse-grained locking: Clock | Advisory locking: Fine-grained locking: User | Advisory locking: Fine-grained locking: Sys | Advisory locking: Fine-grained locking: Clock | Mandatory locking: Fine-grained locking: User | Mandatory locking: Fine-grained locking: Sys | Mandatory locking: Fine-grained locking: Clock |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 2,000 | 0.10 | 0.22 | 0.33 | 0.17 | 0.33 | 0.51 | 0.13 | 0.38 | 0.51 | 0.14 | 0.43 | 0.58 |
| 6,000 | 0.59 | 1.32 | 1.91 | 0.88 | 2.13 | 3.03 | 0.90 | 2.14 | 3.05 | 0.99 | 2.52 | 3.53 |
| 12,000 | 4.37 | 9.58 | 13.97 | 5.38 | 12.60 | 18.01 | 5.34 | 12.63 | 18.01 | 5.53 | 15.03 | 20.60 |

**Figure 20.7**  Single child, varying *nrec*, different locking techniques

The last 12 columns give the corresponding times in seconds. In all cases, the user CPU time plus the system CPU time approximately equals the clock time. This set of tests was CPU limited and not disk limited.

The six columns under “Advisory locking” are almost equal for each row. This makes sense because for a single process; there is no difference between coarse-grained locking and fine-grained locking, except for the extra calls to `fcntl`.

Comparing no locking with advisory locking, we see that adding the locking calls increases the system CPU time by 32% to 73%. Even though the locks are never used (since only a single process is running), the system call overhead in the calls to `fcntl` adds time. Also note that the user CPU time is about the same for all four versions of locking. Since the user code is almost equivalent (except for the number of calls to `fcntl`), this makes sense.

The final point to note from Figure 20.7 is that mandatory locking increases the system CPU time by 13% to 19% compared to advisory locking. Since the number of locking calls is the same for advisory fine-grained locking and mandatory fine-grained locking, the additional system call overhead must be from the reads and writes.

grained locking to fine-grained locking. On the system used for these tests, coarse-grained locking is the same as fine-grained locking for one process, but becomes more expensive (by about 30%) with multiple processes.

We would like the clock time to decrease from coarse-grained to fine-grained locking, which it does as soon as we start using multiple processes. However, we expect the system time to remain higher for fine-grained locking for any number of processes, because we are issuing more fcntl calls with fine-grained locking than with coarse-grained locking. If we total the number of fcntl calls in Figure 20.6, we have an average of 87,858 for coarse-grained locking and 115,520 for fine-grained locking. We expect this increase of 31% more calls to fcntl to result in increased system time for fine-grained locking. Therefore, the decrease in system time for fine-grained locking with two processes, and the relatively small increase with more than two processes, is puzzling.

There are two reasons for this behavior. First, recall from Figure 20.7 that there is no significant difference between coarse-grained locking times and fine-grained locking times when there is no contention for the locks. This shows that the CPU overhead of the extra fcntl calls doesn’t affect the performance of the test program. The second reason is that with coarse-grained locking, we hold locks for longer periods of time, thus increasing the likelihood that other processes will block on a lock. With fine-grained locking, the locking is done over shorter intervals, so there is less chance that processes will block. If we count the number of times fcntl blocks, we will see that processes block more frequently with coarse-grained locking. For example, with four processes, coarse-grained locking blocks almost five times more frequently than with fine-grained locking. The extra work that processes need to do to put themselves to sleep and wake up more often with coarse-grained locking increases the system time, reducing the difference in system times between the two locking approaches.

The final column in Figure 20.8, labeled “Δ Sys,” is the percentage increase in the system CPU time from advisory fine-grained locking to mandatory fine-grained locking. These percentages show that mandatory locking adds significantly (between 20% and 76%) to the system time as concurrency increases.

Since the user code for all these tests is almost identical (there are some additional fcntl calls for both advisory fine-grained and mandatory fine-grained locking), we expect the user CPU times to be the same across any row.

The first time we ran these tests, we measured the user times for coarse-grained locking to be almost twice as long as the times for fine-grained locking when multiple processes competed for the locks. Because the two versions of the database are the same, except for the number of calls to fcntl, this made no sense. After investigating, we discovered that because there was more contention with coarse-grained locking, processes were waiting longer, and the operating system decided to reduce the CPU clock frequency to save power. With fine-grained locking, there was more activity, so the system increased the CPU clock frequency. This (artificially) made the coarse-grained locking tests run more slowly than the fine-grained tests. After disabling the frequency scaling feature, we measured the performance of the test without this bias, and the difference in user times was much smaller.

The values in the first row of Figure 20.8 are similar to those for an nrec of 2,000 in Figure 20.7. This corresponds to our expectation.
