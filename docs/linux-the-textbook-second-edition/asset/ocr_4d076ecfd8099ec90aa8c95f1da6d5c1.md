# Projects

# Project 1

Put a dispensable USB thumbdrive (one that you really don’t care about the data on) into your computer, and in the primary partition, create an ext4 file system on it. It is assumed that the USB thumbdrive already has a primary partition on it, which is usually preformatted. Use two different approaches. First, use the mkfs command. Then change the volume label to “USER_DATA” with the proper mke2fs command and then verify that change with the e2label command.

For a GUI-installed Linux system, use the Gparted graphical application on your Linux system to delete the partition you created with mke2fs and recreate it in Gparted. In each approach, mount the ext4 partition at a convenient location in your Linux file system, create some files on it, and then unmount it. Which approach is more useful for you?

Looking for more? Visit our sites for additional readings, recommended resources, and exercises.
CRC Press e-Resource: https://www.crcpress.com/9781138710085
Authors’ GitHub: https://github.com/bobk48/linuxthetextbook