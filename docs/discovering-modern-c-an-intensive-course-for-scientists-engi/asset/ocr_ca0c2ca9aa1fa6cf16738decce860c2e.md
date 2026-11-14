# B.5 Unix, Linux, and Mac OS

Unix systems like Linux and Mac OS provide a rich set of commands that allow us to realize many tasks with little or no programming. Some of the most important commands are:

+   - ps: List (my) running processes.
+   - kill id: Kill the process with id id; kill -9 id, force it with signal 9.
+   - top: List all processes and their resource use.
+   - mkdir dir: Make a new directory with name dir.
+   - rmdir dir: Remove an empty directory.
+   - pwd: Print the current working directory.
+   - cd dir: Change the working directory to dir.
+   - ls: List the files in the current directory (or dir).
+   - cp from to: Copy the file from to the file or directory to. If the file to exists, it is overwritten, unless we use cp -i from to which asks for permission.
+   - mv from to: Move the file from to directory to if such a directory exists; otherwise rename the file. If the file to exists, it is overwritten. With the flag -i, we are asked for our permission to overwrite files.
+   - rm files: Remove all the files in the list files. rm * removes everything—be careful.
+   - chmod mode files: Change the access rights for files.
+   - grep regex: Find the regular expression regex in the terminal input (or a specified file).
+   - sort: Sort the input.
+   - uniq: Filter duplicated lines.
+   - yes: Write y infinitely or my text with yes 'my text'.

The special charm of Unix commands is that they can be piped; i.e., the output of one program is the input of the next. When we have an installation install.sh for which we are certain that we will respond y to all questions, we can write:

```
yes | ./install.sh
```

Or when we want to know all words of length 7 composed of the letters t, i, o, m, r, k, and f:

```
grep -io '\<[tiomrkj]\{7\}\>' openthesaurus.txt |sort| uniq
```

This is how the author cheats in the game 4 Pics 1 Word—sometimes.