```
int setvbuf(FILE *restrict fp, char *restrict buf, int mode, size_t size);
<stdio.h>
mode: _IOFBF, _IOLBF, _IONBF
Returns: 0 if OK, nonzero on error
p. 146
```

```
void *shmat(int shmid, const void *addr, int flag);
<sys/shm.h>
flag: SHM_RND, SHM_RDONLY
Returns: pointer to shared memory segment if OK, -1 on error
p. 574
```

```
int shmctl(int shmid, int cmd, struct shmid_ds *buf);
<sys/shm.h>
cmd: IPC_STAT, IPC_SET, IPC_RMID, SHM_LOCK (Linux 3.2.0, Solaris 10), SHM_UNLOCK (Linux 3.2.0, Solaris 10)
Returns: 0 if OK, -1 on error
p. 573
```

```
int shmdt(const void *addr);
<sys/shm.h>
Returns: 0 if OK, -1 on error
p. 574
```

```
int shmget(key_t key, size_t size, int flag);
<sys/shm.h>
flag: IPC_CREAT, IPC_EXCL
Returns: non-negative shared memory ID if OK, -1 on error
p. 572
```

```
int shutdown(int sockfd, int how);
<sys/socket.h>
how: SHUT_RD, SHUT_WR, SHUT_RDWR
Returns: 0 if OK, -1 on error
p. 592
```

```
int sig2str(int signo, char *str);
<signal.h>
Returns: 0 if OK, -1 on error
Platforms: Solaris 10
p. 380
```

```
int sigaction(int signo, const struct sigaction *restrict act, struct sigaction *restrict oact);
<signal.h>
Returns: 0 if OK, -1 on error
p. 350
```

```
int sigaddset(sigset_t *set, int signo);
<signal.h>
Returns: 0 if OK, -1 on error
p. 344
```