Contemporary tar on Linux is the Gnu version.

The tar (short for tape archive) utility was originally designed to save file systems on tape as a backup so that files could be recovered in the event of a system crash. It is primarily used now to pack a directory hierarchy as an ordinary disk file. That disk file can then be either saved for system backup purposes locally or remotely, or transmitted to someone via the Internet. It is also used commonly with a compression utility, such as gzip, via a command line option. Doing so saves disk space and transmission time. The saving in disk space results primarily from the fact that empty space within a cluster is not wasted. A brief description of the tar utility is as follows.

The Gnu version of tar has some important functional features and incorporates a more friendly syntax than a traditional UNIX tar. Therefore, for beginners, we only show the “long form” of the Gnu-style syntax because it is more intuitive and easy to understand. Once you get more familiar with tar, you may switch to the UNIX-style short form at your discretion.

System administrators normally use a cost-effective archival medium for archiving complete file system structures as backups, so that, when a system crashes for some reason, files can be recovered. Linux-based computer systems normally crash for reasons beyond the operating system’s control, such as a disk head crash because of a power surge. Linux rarely causes a system to crash because it is a well-designed, coded, and tested operating system. In a typical installation, backup is done every day during off hours (late night or early morning) when the system is not normally in use.

The general syntax of the tar command, shown with Gnu-style syntax as opposed to traditional UNIX-style syntax, is as follows:

# tar

```
Syntax:
    tar [operation mode] [operation mode options] [FILE...]
```

**Purpose:** Archive (copy in a particular format) files to or, restore files from, an archival medium (which can be an ordinary file). Directories are by default archived and restored recursively

**Output:** Archived or restored files or directory structures

# Main Operations and Operation Options in Gnu-Style Usage:

+   --append          Append files to the end of an archive
+   --concatenate     Append an archive to the end of another archive
+   --compare         Find differences between archive and file system
+   --create          Create a new tape and record archive files on it
+   --delete          Delete from the archive
+   --extract         Extract files from an archive
+   --help            Display a short option summary
+   --list            List the contents of an archive
+   --show-defaults   Show built-in defaults for options
+   --test-label      Test the archive volume label and then exit
+   --update          Append files that are newer than the versions in an archive
+   --usage           Display a list of available options
+   --version         Display program version and copyright information

# Common Options:

+   --preserve-permissions  Extract information about traditional file permissions
+   --acls                  Enable POSIX.1e ACL support
+   --gzip                  Filter the archive through gzip
+   --verbose               Verbosely list files processed
+   --file ARCHIVE.tar      Send archive to file named ARCHIVE.tar