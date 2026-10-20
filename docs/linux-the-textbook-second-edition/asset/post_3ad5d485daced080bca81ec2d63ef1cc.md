
# Command Arguments:
FILE...    Target, either an archive file, or file object to be archived

## 17.6.2.1 Archiving and Restoring Files Using tar

A normal Linux user can archive their own work if they want to. They would normally need to do this with file objects related to a project, so that they can transfer them to someone via e-mail, ssh, or via secondary storage media (USB thumb drive, DVD, or CD-ROM). Or perhaps they would want to retain their own file system objects as backups via the same methods.

The primary reason for making an archive is the convenience of dealing with (sending or receiving) a single file instead of a complete directory hierarchy. Without an archive, the sender might have to send several files and directories (a file structure) that the receiver would have to restore in their correct hierarchical structure. Without an archiving facility such as tar, depending on the size of the files and directory structure, the task of sending, receiving, and reconstructing the file structure can be time consuming.

In Chapter 7, Section 7.7, we discussed file compression by using the bzip2, gzip, gunzip, gzexe, xz, zcat, and zmore commands, and pointed out that compression saves disk space and transmission time. However, compressing small files normally does not result in much compression. Moreover, compressing files of one cluster in size (the minimum unit of disk storage; one or more sectors) or less does not help save disk space even if compression does result in smaller files, because the system ends up using one cluster to save the compressed file anyway. But if compression does result in a smaller file, you do save time in transmitting the compressed version. If the disk block size is 512 bytes and a cluster consists of more than two blocks, you can use the tar command to pack files together in one file, with a 512-byte tar header at the beginning of each file, as shown in Figure 17.7.

![](img/2a18e06cd9c6395e451f26126ecba1fd_576_0.png)

FIGURE 17.7 tar-packed file.

## 17.6.2.2 Eight Easy tars

In this section, we show eight of the simplest uses of the tar command. In subsequent sections, we expand upon these “easy tars” with more detailed example sessions run on our Linux system.

- 1. Creating an archive
This is the simplest command to create an archive file from a directory.

```
$ tar --create --verbose --file archive_name.tar directory_name
```

where
--create is the operation to create a new archive
--verbose is the operation to list the files being processed
--file is the operation that specifies that the file
archive_name.tar is the name of the archive file and
directory_name is the directory you want to archive

- 2. Creating an archive and preserving its ACL permissions
A simple variation on creating an archive is using an option to preserve ACLs that the directory has. ACLs are detailed fully in Section W26.9.2 at the book website.

```
$ tar --acls --create --verbose --file archive_name.tar directory_name
```

where
--acls is the option to preserve the ACLs that the directory has
--create is the operation to create a new archive
--verbose is the operation to list the files being processed
--file is the operation that specifies that the file archive_name.tar is the name of the archive file and
directory_name is the directory you want to archive

- 3. Extracting an archive
This is the simplest command to extract a directory from an archive file.

```
$ tar --extract --verbose --file archive_name.tar
```

where
--extract is the operation to extract a directory_name from an archive file
--verbose is the operation to list the files being processed
--file is the operation that specifies that the file archive_name.tar is the name of the archive file

In its simplest form, the directory which will be created from the archived file will have the same name as the archive file, minus the .tar extension.

- 4. Extracting an archive and restoring its ACL entries
A simple variation on extracting an archive is using an option to restore the preserved ACLs that the archive file has (if any).

```
$ tar --acls --extract --verbose --file archive_name.tar
```

where
--acls is the option to restore the preserved the ACLs that the archived file has
--extract is the operation to extract the archived file
--verbose is the operation to list the files being processed
--file is the operation that specifies that the file archive_name.tar is the name of the archive file

In this simplest form variation, the directory which will be created from the archived file will have the same name as the archive file, minus the .tar extension.

## 5. Listing the contents of an archive

This procedure allows you to view the contents of an archive file without extracting anything from it.

```
$ tar --list --verbose --file archive_name.tar
```

where
--list is the operation that lists the contents of the archive file
--verbose is the operation to list the files being processed
--file is the operation that specifies that the file archive_name.tar is the name of the archive file

## 6. Extracting a single file from an archive file

The following command extracts only a specific file from an archive file.

```
$ tar --extract --verbose --file archive_file.tar file_pathname
```

where
--extract is the operation to extract the single file
--verbose is the operation to list the files being processed
--file is the operation that specifies that the file archive_name.tar is the name of the archive file you are extracting from and
file_pathname is the complete pathname specification to the file you want to extract inside the archive

## 7. Extracting a single directory from an archive file

A variation on extracting just a single file from an archive, to extract a single directory, along with recursively extracting any of its subdirectories and files, is to specify the directory name that you want to extract as follows:

```
$ tar --extract --verbose --file archive_file.tar directory_pathname
```

where
--extract is the operation to extract a single file
--verbose is the operation to list the files being processed
--file is the operation that specifies that the file archive_name.tar is the name of the archive file you are extracting from and
directory_pathname is the complete pathname specification to the directory you want to extract inside the archive

## 8. Adding a file or directory to an existing archive using --append option

To add files to an existing archive, do the following:

```
$ tar -append -verbose --file archive_name.tar file_or_directory_name
```

where
--append is the operation to add the single file or directory to the archive
--verbose is the operation to list the files or directories being processed
--file is the operation that specifies that the file archive_name.tar is the name of the archive file you are adding files or directories to and
file_or_directory_name is the complete pathname specification to the file or directory you want to add inside the archive

## Exercise 17.13a and 17.13b

- A. Referring to the abbreviated man page shown earlier, or to the man page for tar on your Linux system, give a command that would create a gzipped archive of a directory named ziptest.
- B. Give a command that would extract the gzipped archive into another directory named ziptest2.

## 17.6.2.3 Creating an Archive with tar

As seen in the previous section, the most common use of the tar command is for archiving (also known as packing) a list of files and/or directories by using the --create or --append options. The --create option creates a new archive, whereas the --append option appends files at the end of the current archive.

In the example sessions presented in this and the following section, we use the directory structure shown in Figure 17.8. The following session shows that there are two directories under the unixbook directory called current and final. In addition, each of these directories contains six files (see Figure 17.8), displayed by the ls -l command.

```
$ cd unixbook
$ pwd
/users/sarwar/unixbook
$ ls -l
drwx------ 2 sarwar 512 Jul 22 13:21 current
drwx------ 2 sarwar 512 Jul 22 13:21 final
$ cd current
$ ls -l
-rw------ 1 sarwar 204288 Jul 19 13:06 ch07.doc
-rw------ 1 sarwar 87552 Jul 19 13:06 ch08.doc
-rw------ 1 sarwar 86016 Jul 19 13:06 ch09.doc
-rw------ 1 sarwar 121344 Jul 19 13:06 ch10.doc
-rw------ 1 sarwar 152576 Jul 19 13:06 ch11.doc
-rw------ 1 sarwar 347648 Jul 19 13:06 ch12.doc
$ cd ..
$ cd final
$ ls -l
-rw------ 1 sarwar 41984 Jul 19 13:06 ch1.doc
-rw------ 1 sarwar 54272 Jul 19 13:06 ch2.doc
```

![](img/2a18e06cd9c6395e451f26126ecba1fd_579_0.png)

FIGURE 17.8 Directory structure.
