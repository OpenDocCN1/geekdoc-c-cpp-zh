# INTERLUDE: FILES AND DIRECTORIES 493

> TIP: THINK CAREFULLY ABOUT NAMING
Naming is an important aspect of computer systems [SK09]. In UNIX systems, virtually everything that you can think of is named through the file system. Beyond just files, devices, pipes, and processes [K84] can be found in what looks like a plain old file system. This uniformity of naming eases your conceptual model of the system, and makes the system simpler and more modular. Whenever creating a system or interface, think carefully about what names you are using.

Directories and files can have the same name as long as they are in different locations in the file-system tree, there are two files named bar.txt, /foo/bar.txt and /bar/bar.txt.
You may also notice that the file name in this example has two parts: bar and txt, separated by a period. The first part is an arbitrary name, whereas the second part of the file name is usually used to indicate the type of the file, whether it is C code (e.g., .c) or an image (e.g., .jpg), or a music file (e.g., .mp3). However, this is just a convention: there is no enforcement that the data contained in a file named.c is C source code.
Thus, we can see one great thing provided by the file system: convention to name all the files we are interested in. Names are important in systems as the first step to accessing any resource is able to name it. In UNIX systems, the file system provides a unified way to access files on disk, USB stick, CD-ROM, many other devices, and in fact many other things, all located under the single directory.

# 39.2 The System Interface

Let's discuss the file system interface in more detail. We'll start with the basics of creating, accessing, and deleting files. You might think this is straightforward, but along the way we'll discover the mysterious call that is used to remove files, known as unlink(). Hopefully, by the end of this chapter, this mystery won't be so mysterious to you!

# 39.3 Creating Files

We'll start with the most basic of operations: creating a file. This can be accomplished with the open system call; by calling open() and passing the O_CREAT flag, a program can create a new file. Here is some example code to create a file called "foo" in the current directory:

```
int fd = open("foo", O_CREAT|O_WRONLY|O_TRUNC, S_IRUSR|S_IWUSR);
```

© 2008–19, ARPACI-DUSSEAU

THREE
EASY
PECES