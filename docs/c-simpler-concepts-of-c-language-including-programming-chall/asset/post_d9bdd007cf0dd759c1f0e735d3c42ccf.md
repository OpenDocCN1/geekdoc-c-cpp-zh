
# 202

# C-SIMPLER

```
% /proc/cpuinfo
processor : 0
vendor_id : GenuineIntel
cpu family : 6
model : 5
model name : Pentium II (Desutches)
stepping : 2
cpu MHz : 400.913520
cache size : 512 KB
fdiv_bug : no
hlt_bug : no
sep_bug : no
f0f_bug : no
coma_bug : no
fpu : yes
fpu_exception : yes
cpiduid level : 2
wp : yes
flags : vme pse tsc msr pae mce cx8 apic spec
mtr pge mca cmov pat36 mm fxsr
bogomips : 399.77
```

Figure 13.2: /proc with cpuinfo.

From here /proc is used extensively for getting details of file descriptors and process control block. Every process will have process id and it will be updated in /proc file system.

OS maintains a database called Process Control Block which has details of file descriptors. File descriptors are numbers allocated to all the files in Linux. Since everything is file in Linux, Input, Output and Error messages are even denoted by a number and that is referred as file descriptor. All the file descriptors are updated clearly in a table called file descriptor table in PCB. The structure of file descriptor table is referred below in Fig 13.3

| 0 - stdin |
| 1 - stdout |
| 2 - stderr |
| 3 - file 1 |
| 4 - file 2 |

Figure 13.3: File descriptor table.

# C PROGRAMMING IN UNIX/LINUX

From the picture one can understand 0 is fd for standard input (key board), 1 is for standard output (monitor) and 2 is the number allotted for standard error message. Since 0, 1 and 2 are allotted already newly created file will get number 2. For an instance if a file is created it will get 3 as the file descriptor and next file will be created 4. Theoretically discussing would not be sufficient.

Writing a small C in Linux with C programming will help the reader to understand the concept in a great way. The following C code aims in creating 2 files. After creation one can manually check the file descriptor table easily and check if the files have been allotted with numbers as expected. GNU tool kit in Linux helps to compile and execute C programs with GCC compilers. GCC is expanded as Gnu Compiler. The following C file prog1.c simply creates 2 files txt1.txt and txt2.txt.

```
// prog1.c - C code for creating 2 files.
// create is the system call used to create new files through code.
// While loop in code will execute the code continuously so that user can check
// /proc file system.

#include <stdio.h>
int main () {
    int fd1, fd2;
    printf("\n THIS WILL CREATE 2 FILES NOW");
    fd1 = create("txt1.txt", 0777);
    // create txt1.txt file through this system call, also file permissions
    // mentioned. Since every function in C will have a return value, this will also
    // have the same and here once the file is created, it will return an integer
    // which is being referred as file descriptor.
    fd2 = create("txt2.txt", 0777);
    while(1) {
    }
}
```

# 13.2.1. Execution procedure

User has to store the file with .c extension and once done the following command can be issued from prompt.

$ gcc -o prog1 prog1.c

Where:

- Gcc is Compiler
- Prog1 - Executable file name
- Prog1.c - File name.

If there is no compilation error, executable file as mentioned before fd_demo will be available for execution. The snapshot is in the following Fig 13.4 complete execution cycle has been followed.

```
ubuntu@ubuntu:~$ gcc -o prog1 prog1.c
ubuntu@ubuntu:~$ ./prog1 &
5720
ubuntu@ubuntu: /proc/cd cd 5720
ubuntu@ubuntu:/proc/cd 5720 ls
attr cpuset mountinfo pagemap wchan
aux cgroup limits root statm
clear_refs loginid sched status
cmdline fd maps oom_adj syscall
coredump_filter df oom_score task
ubuntu@ubuntu:/proc/cd/5720 fd
ubuntu@ubuntu:/proc/cd/5720 ls
0 1 2 3 4
```

```
-lrwxrwxr-- 1 ubuntu 64 2009-10-05 21:52 4 -> /home/ubuntu/txt.txt
-lrwxrwxr-- 1 ubuntu 64 2009-10-05 21:52 3 -> /home/ubuntu/txt.txt
-lrwxrwxr-- 1 ubuntu 64 2009-10-05 21:52 2 -> /dev/pts/0
-lrwxrwxr-- 1 ubuntu 64 2009-10-05 21:52 1 -> /dev/pts/0
-lrwxrwxr-- 1 ubuntu 64 2009-10-05 21:52 0 -> /dev/pts/0
```

Figure 13.4: Execution Snapshot.

# 13.3. BASIC CALLS

There are many system calls available for Users. What is a system call? Is it as good as C programming? Why is this called system call and not functions? Functions are specific to the language. System calls are specific to the operating systems. The system calls that are going to be discussed are available only with Linux and not with windows. Since these are OS, system calls will be the simplest understanding.

# 13.3.1. Creat system call: (creat and not create)

This is used for creation of files. Creat will need file name to be specified, along with permissions. Every system call will have a return value. When this system call is invoked, it will return an integer and that is called file descriptor. As already discussed, standard input (keyboard) is represented with 0, standard output (monitor) is represented with 1, and when a new file is created, standard error is denoted with 2. So when a new file is created, it will be allotted fd. Successive files get successive numbers as 4, 5, etc.

And 077 is Read, Write and Execute permission for the users. It can be anything with the wish of the developer. This concept of file permissions has been discussed earlier. Please refer to some clarifications.

```
#include <stdio.h>

int main() {
    int fd1, fd2; // To collect the return values from create
    printf("\n Creating 2 files");
    fd1 = create("txt1.txt", 0777);
    // File txt1.txt with permissions 777 is created here and
    // return value is collected in fd1, which is referred as
    // as file descriptor. It should be 3.
    fd2 = create("txt2.txt", 0777);
    // File txt2.txt with permissions 777 is created here and
    // return value is collected in fd2, which is referred as
    // as file descriptor. It should be 4.
    while (1) // Just to keep the programming running in the
        // background to check the file descriptor table after
        execution;
}
```

Procedure for the execution of program:

1. Save the file as prog1.c
2. Compile it with gcc -o prog1 prog1.c where prog1 is the executable name.
3. Run it in the background with ./prog1 &
4. & represents that the program is in background.

Now to check if the files are created and the File Descriptor table is updated with the new entries, following steps are to:

1. Once run in the background with ./prog1 & there will be a process thrown immediately. A snapshot is presented with the details.
2. In this case 5720 is the process id.
3. Now navigate to /proc with cd /proc where /proc is the file system which has details of all the processes and it will be updated on the fly. All the processes will be updated in the proc file system.
4. Navigate to the /proc file system and search for presence of 5720 (This number will be different for the reader, when tried).
5. Then do 5720. Do listing, a directory called fd will be present and navigating through it will get the complete details of fd table.
6. Do a listing with ls. Command will show series of number as 0 1 2 3 4. To get a detailed listing, do ls -l where the new files will be seen and will be allotted fd number as 3 and 4. Following snapshot (Fig 13.5) will stand as a reference for above conveyed explanations.

# 13.3.2. Open ( ) system call

This call will serve two purposes; one is to open the file that has been created. If the mentioned file is not created already, it will create it and then get opened.

A simple program will help the reader to understand the functionality. The header file's information can be collected from MAN page. Man open with the system call.

```
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

{
    int fd1, fd2;

    // For getting the return value from open
    printf("\n Creating 2 files");
    fd1 = open("txt1.txt", O_RDONLY|CREATE, 0777);

    // open will open the file txt1.txt if already available, if not
    // o_create flag will make sure the file is created during
    // execution with mentioned permissions. Also the fd table will
    // be updated accordingly.
    fd2 = open("txt2.txt", O_RDONLY|CREATE, 0777);

    // Reader can see that O_RDONLY is mentioned in the call. It is
    // to specify the opening mode. It can be O_WRONLY or O_RDWR.
    while(1)
    {
    }
}
```
