# 6.22.8 File functions

Three functions are available for low-level file handling.
ajSysFileWhich will search for a user-executable file in the current path whereas
ajSysFileWhichEnv will use a PATH from the environment that is provided by argument.
The functions returns ajTrue if the executable was found:

```
AjBool ajSysFileWhich (AjPStr* Pstr);
AjBool ajSysFileWhichEnv (AjPStr* Pstr, char* const env[]);
```

ajSysFileUnlink is used to safely delete a file or link:

```
AjBool ajSysFileUnlink (const AjPStr str);
```

# 6.22.9 C function wrappers

Various functions are provided that wrap (with some modifications) standard C functions. In most cases these are provided to overcome system-dependent limitations of the standard C functions. These functions have the prefix ajSysFunc and include:

```
char* ajSysFuncStrtok (const char* txt1, const char* txt2);
char* ajSysFuncStrtokR (const char* txt1, const char* txt2, char** Ptxt, AjPStr* Pbuf);
char* ajSysFuncFgets (char* buf, int n, FILE* fp);
char* ajSysFuncFopen (const char* txt, const char* flags);
FILE* ajSysFuncFdopen (ajint filedes, const char* mode);
```

# 6.22.10 Functions from ajutil.c/h

The following functions call the C function exit. The functions embExit* (defined in embexit.h/c), called from applications code to exit the application, make use of these functions:

```
/* Exits with a success code (zero) after cleanup routines */
__noreturn void ajExit (void);

/* Exits with an unsuccessful code without flushing files or clean-up. */
__noreturn void ajExitAbort (void);

/* Exits with an unsuccessful code without clean-up. */
__noreturn void ajExitBad (void);
```

ajExit() calls exit with a success code (zero) after calling clean-up routines which report on resource usage, etc.

ajExitAbort() calls exit with an unsuccessful code (EXIT_FAILURE defined in stdlib.h) without flushing any files. This is needed to exit from, for example, a failed