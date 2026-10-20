2. Copying a single local file in compressed form, with the operation feedback presented in human-readable form, from the source backup.tar (in the current working directory) to the destination directory /home/mansoor/backup1 which you have permissions on.

```
$ rsync -zvh backup.tar /home/mansoor/backup1
```

3. Using rsync to copy an entire source directory contents from the directory named syncdir locally to a destination directory locally named /usr/home/bob/USBint. The slash at the end of the designated source means “copy the contents of this directory,” not “copy the directory by name”

```
$ rsync -av syncdir/ /usr/home/bob/USBint
```

4. Copying a single source directory /home/bob/backups in compressed form, with the operation feedback presented in human-readable form, to the destination directory /home/mansoor/backups which you have permissions on

```
$ rsync -avzh /home/bob/backups /home/mansoor/backups/
```

5. Copying a single source directory /home/bob/backups, and its files and subdirectory structure, in compressed form, to the destination directory /home/mansoor/backups which you have permissions on

```
$ rsync -zvr /home/bob/backups /home/mansoor/backups
```

6. Doing a dry-run, where you remove the source files and compress the transmitted file object

```
$ rsync --dry-run --remove-source-files -zvh backup.tar /tmp/backups/backup.tar
```

Remote examples:

7. Copying a single directory, named Music, from the local machine to a remote machine at 192.168.0.8 into mansoor's home

```
$ rsync -avz Music mansoor@192.168.0.8:/home/mansoor/
```

8. Copying an entire local directory, named syncdir2, using ssh, to a remote machine at 192.168.0.7 and into the OS X-style directory /Users/b/Linux3e

```
$ rsync -av -e ssh syncdir2 bob@192.168.0.7:/Users/b/Linux3e
```

9. Copying a remote directory to a local directory

```
$ rsync -avzh root@192.168.0.100:/home/bob/backups /home/mansoor/temp
```

10. Copying just the contents of the remote directory /home/mansoor/Linux2e updating (sometimes called “syncing”) with the --existing option, only the existing files at the destination. If the source has new files, which are not on the destination, these new files are not put on the destination.

```
$ rsync -avz --existing mansoor@192.168.1.2:/home/mansoor/Linux2e/ .
```