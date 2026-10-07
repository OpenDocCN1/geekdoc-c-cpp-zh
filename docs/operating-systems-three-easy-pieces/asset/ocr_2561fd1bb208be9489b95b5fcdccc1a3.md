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

```
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

OPERATING SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG