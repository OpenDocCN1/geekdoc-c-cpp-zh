ory leaves simply because it prints out the number of objects that exists in memory that match the related signature. You can pipe the results from findjsobjects into jsprint to display the contents of each of the objects.

Outside of mdb are several useful tools that will work on a core file created in SmartOS. These are usually found in /usr/proc/bin and include the following commands:

```
# pwd
/usr/proc/bin
# ls -l
total 13
lrwxrwxr-x 1 root 15 Jun 29 2013 pldd -> ../bin/pldd
lrwxrxr-x 1 root 16 Jun 29 2013 pfiles -> ../bin/pfiles
lrwxrxr-x 1 root 16 Jun 29 2013 pflags -> ../bin/pflags
lrwxrxr-x 1 root 14 Jun 29 2013 pmap -> ../bin/pmap
lrwxrxr-x 1 root 14 Jun 29 2013 prun -> ../bin/prun
lrwxrxr-x 1 root 14 Jun 29 2013 psig -> ../bin/psig
lrwxrxr-x 1 root 16 Jun 29 2013 pstack -> ../bin/pstack
lrwxrxr-x 1 root 15 Jun 29 2013 pstop -> ../bin/pstop
lrwxrxr-x 1 root 15 Jun 29 2013 ptime -> ../bin/ptime
lrwxrxr-x 1 root 15 Jun 29 2013 ptree -> ../bin/ptree
lrwxrxr-x 1 root 15 Jun 29 2013 pwait -> ../bin/pwait
lrwxrxr-x 1 root 14 Jun 29 2013 pwdx -> ../bin/pwdx
```

Of the above process tools, the pmap and pfiles are especially useful, pmap displays how much memory is occupied by the heap and buffers. pfiles is able to report on file descriptors by the process that created the core file. This can be useful for identifying when a ulimit isn't high enough. Sometimes, using pfiles can also help find where files aren't closed correctly or are left open. pflags is able to report on the original command that started the process.

# Summary

In this chapter we looked at different tooling to debug外し processes. These include specialty tools that were generated for the sole purpose of helping to identify issues in has processes. Using good for logging or tv you find can be helpful. For production issues, using core files or a REPL can also be useful. Any issue that exists in halt itself, is sure to file an issue in the github repo.