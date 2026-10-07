
# INTERLUDE: FILES AND DIRECTORIES

TIP: BE WARY OF POWERFUL COMMANDS
The program rm provides us with a great example of powerful commands, and how sometimes too much power can be a bad thing. For example, to remove a bunch of files at once, you can type something like:

```
prompt rm *
```

where the * will match all files in the current directory. But sometimes you also want to delete the directories too, and in fact all of their contents. You can do this by telling rm to recursively descend into each directory, and remove its contents:

```
prompt rm -rf *
```

Where you get into trouble with this small string of characters when you issue the command, accidentally, from the root directory of a file system removing every file and directory from it. Oops! Thus, remember the double-edged sword of powerful commands; while they give you the ability to do a lot of work with a small number of keystrokes, they can also quickly and readily do a great deal of harm.

# 39.12 Reading Directories

Now that we have created a directory, we might wish to read one out. Indeed, that is exactly what the program ls does. Let's write our own little ls and see how it is done.

Instead of just opening a directory as if it were a file, we must use a new set of calls. Below is an example that prints the contents of a directory. The program uses three calls, opendir(), readdir(), and closedir(), to get the job done, and you can see how the interface is; we use a simple loop to read one directory at a time, and print out the name and index of each file in the directory.

```c
int main(int argc, char *argv[]) {
    DIR *dp = opendir("./");
    assert(dp != NULL);
    struct dire *d;
    while ((d = readdir(dp)) != NULL) {
        printf("%lu %s\n", (unsigned long) d->d_ino,
               d->d_name);
    }
    closedir(dp);
    return 0;
}
```

# INTERLUDE: FILES AND DIRECTORIES

The declaration below shows the information available within each directory entry in the struct data:

```c
struct dire {
    char            d_name[256]; // filename
    ino_t           d_ino;      // inode number
    off_t           d_off;      // offset to next
    unsigned short d_recl;      // length of this record
    unsigned char d_type;       // type of file
};
```

Because directories are light (basically, just mapping the name to the inode number with a few other details), a program may want to stat() each file to get more information, such as its length or other information. Indeed, this is exactly what ls does when you pass it the -i flag; try to see for yourself.

# 39.13 Deleting Directories

Finally, you can delete a directory with a call to rmdir() (which is used by file deletion). However, removing directories is more dangerous, as you could potentially delete a large amount of data with a single command. Thus, rmdir() has the requirement that the directory be non-empty (i.e., only has "." entries) before it is deleted. If you try to delete a directory, the call to rmdir() will simply fail.

# 39.14 Hard Links

We now come back to the mystery of removing a file is performed via link(), by understanding how to make an entry in the file system tree. The link() system takes two arguments, an old pathname and a new one; when you "link" a new name to an old one you essentially create another way to refer to the same file. The command-line program ln is used to do this, as we see in this example:

```
prompt> echo hello > file
prompt> cat file
hello
prompt> ln file file2
prompt> cat file2
hello
```

# INTERLUDE: FILES AND DIRECTORIES

Here we created a file with the word “hello” in it, and called it file. We then created a hard link to that file using the ln program. After this, we can examine the file by either opening file or file2. The link() works because it simply creates another name in the directory you are creating and refers it to the same inode number (i.e., the name) of the original file. The file is not copied in any way; rather you now have two human-readable names (file and file2) that both refer to the same file. We can even see this in the directory, by printing out the inode number of each file:

```
prompt> ls -i file2
6715084 file
6715084 file2
prompt>
```

By passing the -i to ls, it prints out the inode number of each file (as well as the file name). And thus you can see what link really has done: just make a new reference to the same inode number (6715084 in this example). By now you might be starting to see how unlink() works. When you call unlink(), you are really doing two things. First, you are removing the structure (the inode) that will track all relevant information about the file, including its size, its blocks on disk, and so forth. Second, you are unlinking a human-readable name from that file and putting it into a directory. After creating a hard link to a file, to the file system there is no difference between the file name (file) and the newly created file (file2); they are both links to the underlying metadata about the file, which is found in inode number 6715084.

Thus, to remove a file from the file system, we can call unlink(). In the example above, we could for example remove the file named file, and still access the file without difficulty.

```
prompt> rm file
removed 'file'
prompt> cat file2
hello
```

The reason this works is when the file system links it, it checks a reference count within the inode number (sometimes the link count) allows the file system to track how many different file names have been linked to this particular inode. When unlink() is called, it removes the “link” between the human-readable name (the file that is being deleted) and the given node number, and decrements the reference count; only when the reference count reaches zero does the file system also free the node and related data blocks, and truly "delete" the file.

> Note again how creative the authors of this book are. We have also used to call a hamster “Cat” (true story). However, she died, and we now have a hamster “Hammy”. Update: Hammy is now dead too. The pets are piling up.

# 39.15 Symbolic Links

There is one other type of link that is really useful: the symbolic link. Beyond this similarity, symbolic links are different from hard links. The first difference is that a symbolic link is actually a file itself, of a different type. To create a link, you can use the -s flag. Here is an example:

```
prompt> echo hello > file
prompt> ln -s file file2
prompt> cat file2
hello
```

The reason that file2 is 4 bytes is because the symbolic link is formed by the pathname of the linked-file as the data of the link file. Because we've linked to a named file, our link file file2 is small (4 bytes). If we link to a longer pathname, our link file would be bigger:

```
prompt> echo hello >longerfilename
prompt> ln -s longerfilename file3
prompt> ls -al longerfilename file3
-rw-r--r-- 1 remzi remzi 6 May 3 19:17 longerfilename
lrwxr-wx 1 remzi remzi 15 May 3 19:17 file3 -> longerfilename
```

Finally, by the way symbolic links are created, they leave the possibility for what is known as a dangling reference:

```
prompt> echo hello > file
prompt> ln -s file file2
prompt> cat file2
hello
prompt> rm file
prompt> cat file2
cat: file2: No such file or directory
```
