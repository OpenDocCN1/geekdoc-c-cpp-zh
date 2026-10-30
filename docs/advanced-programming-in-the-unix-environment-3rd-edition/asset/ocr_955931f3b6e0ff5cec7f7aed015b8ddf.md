Note that this function returns a pointer to the value of a name=value string. We should always use getenv to fetch a specific value from the environment, instead of accessing environ directly.

Some environment variables are defined by POSIX.1 in the Single UNIX Specification, whereas others are defined only if the XSI option is supported. Figure 7.7 lists the environment variables defined by the Single UNIX Specification and notes which implementations support the variables. Any environment variable defined by POSIX.1 is marked with •; otherwise, it is part of the XSI option. Many additional implementation-dependent environment variables are used in the four implementations described in this book. Note that ISO C doesn’t define any environment variables.

| Variable | POSIX.1 | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 | Description |
|---|---|---|---|---|---|---|
| COLUMNS | • | • | • | • | • | terminal width |
| DATEMSK | XSI | • | • | • | • | getdate(3) template file pathname |
| HOME | • | • | • | • | • | home directory |
| LANG | • | • | • | • | • | name of locale |
| LC_ALL | • | • | • | • | • | name of locale |
| LC_COLLATE | • | • | • | • | • | name of locale for collation |
| LC_CTYPE | • | • | • | • | • | name of locale for character classification |
| LC_MESSAGES | • | • | • | • | • | name of locale for messages |
| LC_MONETARY | • | • | • | • | • | name of locale for monetary editing |
| LC_NUMERIC | • | • | • | • | • | name of locale for numeric editing |
| LC_TIME | • | • | • | • | • | name of locale for date/time formatting |
| LINES | • | • | • | • | • | terminal height |
| LOGNAME | • | • | • | • | • | login name |
| MSGVERB | XSI | • | • | • | • | fmtmsg(3) message components to process |
| NLSPATH | • | • | • | • | • | sequence of templates for message catalogs |
| PATH | • | • | • | • | • | list of path prefixes to search for executable file |
| PWD | • | • | • | • | • | absolute pathname of current working directory |
| SHELL | • | • | • | • | • | name of user’s preferred shell |
| TERM | • | • | • | • | • | terminal type |
| TMPDIR | • | • | • | • | • | pathname of directory for creating temporary files |
| TZ | • | • | • | • | • | time zone information |

Figure 7.7 Environment variables defined in the Single UNIX Specification

In addition to fetching the value of an environment variable, sometimes we may want to set an environment variable. We may want to change the value of an existing variable or add a new variable to the environment. (In the next chapter, we’ll see that we can affect the environment of only the current process and any child processes that we invoke. We cannot affect the environment of the parent process, which is often a shell. Nevertheless, it is still useful to be able to modify the environment list.) Unfortunately, not all systems support this capability. Figure 7.8 shows the functions that are supported by the various standards and implementations.