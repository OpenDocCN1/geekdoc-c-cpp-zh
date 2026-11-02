Suppose that your changes are based on revision 2 (.r2), while the latest revision is .r3. In this case, the update has created four files: list_main.c.r2 contains the revision your changes are based on, while list_main.c.r3 contains the latest revision. The file list_main.c.mine contains your working file which was named list_main.c, before the update was performed. Finally, list_main.c now contains a "mix" of your working file and the latest revision. The parts where conflicts have been found are indicated between extra lines of the form

```
<<<<<<< .mine
{text of your working file}
=======
{text of the latest reversion}
>>>>>>> .r3
```

Now you can edit the file list_main.c and create a consistent version. Usually, you have to speak to the author of the latest revision to resolve the conflicts most efficiently and to satisfy all authors. In the resulting file all auxiliary lines containing <<<<<<<, ======= and >>>>>>> should be removed. Then you have to tell subversion that you have resolved the conflicts using the resolved command. This will remove all auxiliary files. Then you can commit:

```
Gene:list>emacs list_main.c
Gene:list>svn resolved list_main.c
Resolved conflicted state of 'list_main.c'
Gene:list>ls
list.c list.h list_main.c list_mergesort.c list_remove_element.c
Gene:list>svn commit -m "element 8"
Sending       list_main.c
Transmitting file data .
Committed revision 4.
```

You can have a look at the past revision history using the command log. Also the messages describing the changes are shown, for example: