# 3.17 Summary

This chapter has described the basic I/O functions provided by the UNIX System. These are often called the unbuffered I/O functions because each read or write invokes a system call into the kernel. Using only read and write, we looked at the effect of various I/O sizes on the amount of time required to read a file. We also looked at several ways to flush written data to disk and their effect on application performance.

Atomic operations were introduced when multiple processes append to the same file and when multiple processes create the same file. We also looked at the data structures used by the kernel to share information about open files. We'll return to these data structures later in the text.

We also described the ioctl and fcntl functions. We return to both of these functions later in the book. In Chapter 14, we'll use fcntl for record locking. In Chapter 18 and Chapter 19, we'll use ioctl when we deal with terminal devices.

# Exercises

+   3.1 When reading or writing a disk file, are the functions described in this chapter really unbuffered? Explain.

+   3.2 Write your own dup2 function that behaves the same way as the dup2 function described in Section 3.12, without calling the fcntl function. Be sure to handle errors correctly.

+   3.3 Assume that a process executes the following three function calls:
+   fd1 = open(path, oflags);
+   fd2 = dup(fd1);
+   fd3 = open(path, oflags);
+   Draw the resulting picture, similar to Figure 3.9. Which descriptors are affected by an fcntl on fd1 with a command of F_SETFD? Which descriptors are affected by an fcntl on fd1 with a command of F_SETFL?

```
fd1 = open(path, oflags);
fd2 = dup(fd1);
fd3 = open(path, oflags);
```

+   3.4 The following sequence of code has been observed in various programs:
+   dup2(fd, 0);
+   dup2(fd, 1);
+   dup2(fd, 2);
+   if (fd > 2)
+       close(fd);
+   To see why the if test is needed, assume that fd is 1 and draw a picture of what happens to the three descriptor entries and the corresponding file table entry with each call to dup2. Then assume that fd is 3 and draw the same picture.

```
dup2(fd, 0);
dup2(fd, 1);
dup2(fd, 2);
if (fd > 2)
    close(fd);
```

+   3.5 The Bourne shell, Bourne-again shell, and Korn shell notation
+   digit1>&digit2
+   says to redirect descriptor digit1 to the same file as descriptor digit2. What is the difference between the two commands shown below? (Hint: The shells process their command lines from left to right.)
+   ./a.out > outfile 2>&1
+   ./a.out 2>&1 > outfile

```
digit1>&digit2
```

```
./a.out > outfile 2>&1
./a.out 2>&1 > outfile
```