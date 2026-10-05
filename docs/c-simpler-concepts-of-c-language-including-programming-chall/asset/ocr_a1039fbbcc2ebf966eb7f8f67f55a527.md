# C PROGRAMMING IN UNIX/LINUX

Execution procedure remains the same as well as the create system call. A snap shot for the same is given below in Fig 13.6

```
ubuntu@ubuntu:~$ gcc -o prog1 prog1.c
ubuntu@ubuntu:~$ ./prog1
[2] 5753

ubuntu@ubuntu:~$ cd /proc
ubuntu@ubuntu:~$ cd /proc/5753
uubuntu@ubuntu:~$ ls /proc/5753 sma\
attr cpuuset i mountinfo pagemap wchan
auxvx cwd latency monitors personality stat
cgroup environ limits mounts rout sched statm
clear_refs exe laguid net
cmdline fd map status schedstat syscall
coredup_filter fd filter mmap doom_score task
ubuntu@ubuntu:~$ ls /proc/5753
ubuntu@ubuntu:~$ ls /proc/5753/
0 1 2 3 4
-rw-r---- ubuntu 64 2009-10-05 21:57 4 -> /home/ubuntu/txt2.txt
-rw-r---- ubuntu 64 2009-10-05 21:57 3 -> /home/ubuntu/txt1.txt
-rw-r---- ubuntu 64 2009-10-05 21:57 2 -> /dev/ptmx/0
-rw-r---- ubuntu 64 2009-10-05 21:57 1 -> /dev/ptmx/1
-rw-r---- ubuntu 64 2009-10-05 21:57 0 -> /dev/ptmx/0
```

Figure 13.6: File descriptor for open system call.

The next system call to be discussed is Write ( ). It is very simple to understand and here is the program presented for the same.

# 13.3.3. Write ( ) system call

The system call needs a file created already with write permissions. File creation can be done with create as discussed above. Opened file can be written into write system call. The file descriptor of the created file (to which the programmer writes) has to be passed as an argument to the write with the text to be written. The text can be kept in a char array, which is named as buffer here in the following code. Now that buffer along with size of the same also needs to be passed as arguments.

It will serve the purpose and writing it will be over. The file can be opened after execution and it will have "hello" written into it.

```
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int main ()
{
char buffer[5]="hello";
// hello is written into buffer, char array.
int fdl, ret;

fdl = create("txt1.txt", 0777);
// Create to create new file with RWX permissions.
ret = write(fdl, buffer,sizeof(buffer));
// Write has been performed here.

}}
```