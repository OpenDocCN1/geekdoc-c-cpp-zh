# 212
C-SIMPLER

dup2:
syntax of the subroutine dup2() is as follows:

```
int dup2(int oldfd, int newfd);

Where, oldfd, newfd denote the old and new file
descriptors respectively.
```

This system calls copies the oldfd to the newfd, which means that, both the file
descriptors point to the same file. For example:

```
# include <stdio.h>
# include <fcntl.h>
# include <unistd.h>

int main ()
{
 int fd1, fd2;
 fd1 = open("txt1.txt",O_RDONLY|O_CREATE, 0777);
 // here fd1 is duplicated to fd2.
dup2(fd1, fd2);
while(1)
{
}
n}
```

In this program, fd1 and fd2 hold the same reference. (i.e.) Both point to the text
document "txt1".

# POINTS TO REMEMBER

+   1. Reader should pay more attention to all the system calls.
2. Make files will save the time taken for execution.
3. Make files must be named as 'Make file' on 'Makefile'.
4. GCC is GNU C compiler.