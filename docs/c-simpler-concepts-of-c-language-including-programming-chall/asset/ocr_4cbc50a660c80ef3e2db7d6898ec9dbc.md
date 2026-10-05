# 204

# C-SIMPLER

If there is no compilation error, executable file as mentioned before fd_demo will be available for execution. The snap shot is I the following Fig 13.4 complete execution cycle has been followed.

```
ubuntu@ubuntu:~$ gcc -o prog1 prog1.c
ubuntu@ubuntu:~$ ./prog1 &
5720
ubuntu@ubuntu: /proc/cd cd 5720
ubuntu@ubuntu:/proc/cd 5720 ls
attr cpuset io mountinfo pagemap smaps wchan
auxvx cwd latency mounts root statm
cgroup environ limits mountstats
clear_refs exe loginid net sched status
cmdline fd maps oom_adj schedstat syscall
coredoredump_filter dfmno oom_score sessionid task
ubuntu@ubuntu:/proc/cd/5720 fd
ubuntu@ubuntu:/proc/cd/5720 ls
0 1 2 3 4
```

```
-lrwxrwxrwx-- 1 ubuntu ubuntu 64 2009-10-05 21:52 4 -> /home/ubuntu/txt.txt
-lrwxrwxrwx-- 1 ubuntu ubuntu 64 2009-10-05 21:52 3 -> /home/ubuntu/txt.txt
-lrwxrwxrwx-- 1 ubuntu ubuntu 64 2009-10-05 21:52 2 -> /dev/pts/0
-lrwxrwxrwx-- 1 ubuntu ubuntu 64 2009-10-05 21:52 1 -> /dev/pts/0
-lrwxrwxrwx-- 1 ubuntu ubuntu 64 2009-10-05 21:52 0 -> /dev/pts/0
```

Figure 13.4: Execution Snapshot.

# 13.3. BASIC SYSTEM CALLS

There are many / Linux system calls available inbuilt for the Users. What is a system call? Is it as good as in C programming. It can be compared with Printf in C programming. Why is this called system call and not functions? Functions are specific to the programming language. System calls are specific to the operating systems. The system calls that are going to be discussed will be available only with Linux and not with windows. Since these are OS, system calls will be the apt name for. Reader will be exposed to few important system calls and Inter Process Communication methodologies will be discussed.

It would be to always from the simplest to the greatest best understanding.

# 13.3.1. Creat system call: (creat and not create)

This is used for creation of files. Creat will need file name to be specified, along with the permissions. Every function / system call will have a return value. Same is the story for create. When this system call is invoked, it will return an integer value and that is called as file descriptor. As already discussed, standard input (keyboard) is represented with the file descriptor (fd) as 0, standard output (monitor) is represented with 1, and when a new file is created, it will standard error is denoted with 2 as file descriptor. So when a new file is created, it will the file descriptor allotted as fd. Successive files will gets the successive numbers as 4, 5, etc.