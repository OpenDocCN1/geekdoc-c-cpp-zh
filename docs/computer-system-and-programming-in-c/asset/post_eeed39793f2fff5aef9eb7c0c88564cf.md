
## cat Command

The `cat` command lets you view text files. `cat` is short for concatenate. Note that the cat command echoes each line as soon as it has been typed in.

### Examples

- **(I) `cat /etc/passwd`**

  This command displays the `/etc/passwd` file on your screen.

- **(II) `cat /etc/profile`**

  This command displays the `/etc/profile` file on your screen. Notice that some of the contents of this file may scroll off of your screen.

- **(III) `cat file1 file2 file3 > file4`**

  This command combines the contents of the first three files into the fourth file.

## sort Command

The sort command is used to sort the contents of a file named `students_list`.

### Example

```
$cat > students_list
Abhi       20101
Revathi    20125
Preethi    20104
Ravi       20121
Ctrl-D
$
```

Using the sort command, the above list may be sorted alphabetically as shown below:

```
$sort students_list
Abhi       20101
Preethi    20104
Ravi       20121
Revathi    20125
```

## wc Command

The wc command is used to count the number of lines, words and characters in a file.

### Example

```
$wc students_list
5 10 53 students_list
```

Note that there are 5 lines, 10 words and 53 characters in the file. Also note that every line is terminated by pressing the Enter key, which is represented by an invisible new line character. These characters are also counted to get the number of characters as 53 instead of the actual number of characters as 48.

The wc command has the following options:

- (I) `wc -l` will display the number of lines in a file.

### Example

```
$wc -l students_list
```

The output of the above command is the number of lines in the `students_list` file.

- (II) `wc -w` will display the number of words in a file.

### Example

```
$wc -w students_list
```

The output of the above command is the number of words in the `students_list` file.

- (III) `wc -c` will display the number of characters in a file.

### Example

```
$wc -c students_list
```

The output of the above command is the number of characters in the `students_list` file.

## grep Command

The grep command is used to search and display a line for a given word or pattern in a given file name.

Consider the following example to display the register number of a student.

```
$grep Abhi students_list
Abhi 20101
```

## Filters

These refer to any command that can take input from standard input, perform some operations and write the results to standard output.

Consider the following example:

```
$who
cseabhi tty1 sep 29 13:01
itreva tty2 sep 29 14:15
ituser1 tty3 sep 29 15:45
$
```

The above list can be shortlisted to specific users and displayed in alphabetical order as shown below:

```
$who | grep it | sort
itreva tty2 sep 29 14:15
ituser1 tty3 sep 29 15:45
```

## LINUX OPERATING SYSTEM

Linux is a free open-source operating system based on UNIX. Linux was originally created by Linus Torvalds with the assistance of developers from around the globe. Linux is free to download, edit and distribute. Linux is a very powerful operating system and it is gradually becoming popular throughout the world.

### Advantages of Linux

The following are the advantages of Linux operating system:

- **Low Cost:** There is no need to spend time and a huge amount of money to obtain licenses since Linux and much of its software come with the GNU General Public License. There is no need to worry about any software that you use in Linux.

- **Stability:** Linux has high stability compared with other operating systems. There is no need to reboot the Linux system to maintain performance levels. Rarely does it freeze up or slow down. It has a continuous up-time of hundreds of days or more.

- **Performance:** Linux provides high performance on various networks. It has the ability to handle large numbers of users simultaneously.

- **Networking:** Linux provides a strong support for network functionality; client and server systems can be easily set up on any computer running Linux. It can perform tasks like network backup much faster than other operating systems.

- **Flexibility:** Linux is very flexible. Linux can be used for high performance server applications, desktop applications, and embedded systems. You can install only the needed components for a particular use. You can also restrict the use of specific computers.

- **Compatibility:** It runs all common Unix software packages and can process all common file formats.

- **Wider Choice:** There are a large number of Linux distributions which gives you a wider choice. Each organization develops and supports a different distribution. You can pick the one you like best; the core functions are the same.

- **Fast and Easy Installation:** Linux distributions come with user-friendly installation.

- **Better Use of Hard Disk:** Linux uses its resources well enough even when the hard disk is almost full.

- **Multitasking:** Linux is a multitasking operating system. It can handle many things at the same time.

- **Security:** Linux is one of the most secure operating systems. File ownership and permissions make Linux more secure.

- **Open Source:** Linux is an open source operating system. You can easily get the source code for Linux and edit it to develop your personal operating system.

Today, Linux is widely used for both basic home and office uses. It is the main operating system used for high performance business and in web servers. Linux has made a high impact in this world.

### Linux vs Windows

Linux is an open-source operating system. People can change codes and add programs to Linux OS which will help your computer better. Linux evolved as a reaction to the monopoly position of Windows. You cannot change any code for Windows OS. You cannot even see which processes do what and build your own extension. Linux wants the programmers to extend and redesign its OS. Linux users can edit its OS and design a new OS.

All flavors of Windows come from Microsoft. Linux comes from different companies like Lindows, Lycoris, Red Hat, SUSE, Mandrake, Knoppix, Slackware.

Linux is customizable but Windows is not. For example, NASLite is a version of Linux that runs off a single floppy disk and converts an old computer into a file server. This ultra small edition of Linux is capable of networking, file sharing and being a web server.

Linux is freely available for desktop or home use but Windows is expensive. For server use, Linux is cheap compared to Windows. Microsoft allows a single copy of Windows to be used on one computer. You can run Linux on any number of computers.

Linux has high security. You have to log on to Linux with a userid and password. You can log in as root or as a normal user. The root has full privileges.

Linux has a reputation for fewer bugs than Windows.

Windows must boot from a primary partition. Linux can boot from either a primary partition or a logical partition inside an extended partition. Windows must boot from the first hard disk. Linux can boot from any disk in the computer.

Windows uses a hidden file for its swap file. Typically this file resides in the same partition as the OS (advanced users can opt to put the file in another partition). Linux uses a dedicated partition for its swap file.

Windows separates directories with a back slash while Linux uses a normal forward slash.

Windows file names are not case sensitive. Linux file names are case sensitive. For example, `abc` and `aBC` are different files in Linux, whereas in Windows it would refer to the same file.

Windows and Linux have different concepts for their file hierarchy. Windows uses a volume-based file hierarchy while Linux uses a unified scheme. Windows uses letters of the alphabet to represent different devices and different hard disk partitions. For example, `c:`, `d:`, `e:`, etc. while in Linux `/` is the main directory.

Linux and Windows support the concept of hidden files. In Linux hidden files begin with `.`. For example, `.filename`.

In Linux each user will have a home directory and all his files will be saved under it, while in Windows the user saves his files anywhere in the drive. This makes it difficult to have backups for his contents. In Linux it is easy to have backups.

## WINDOWS OPERATING SYSTEM

Windows is a personal computer operating system from Microsoft that, together with some commonly used business applications such as Microsoft Word and Excel, has become a de facto “standard” for individual users in most corporations as well as in most homes.

The original 1985 version of Windows introduced to home and business PC users many of the graphical user interface (GUI) ideas that were developed at an experimental lab at Xerox and introduced commercially by Apple’s Lisa and Macintosh computers. Some of the well-known versions of Windows have included:

- Windows 286
- Windows 386
- Windows 3.0 and 3.11
- Windows 95
- Windows 98
- Windows NT
- Windows 2000
- Windows CE for use in small mobile computers
- Windows Me
- Windows XP
- Windows Vista
- Windows 7
- Windows 8

With the advent of the Internet, Microsoft has repositioned Windows as a kind of “window to the world,” and its efforts to take the lead in Web browsers have made Internet Explorer the most popular browser. Microsoft’s .NET initiative represents an attempt to become industry-dominant in furnishing products and services that facilitate the use of remote application services on the Web.

### Introduction to the Desktop

After you have started the computer, the area you are looking at is called the desktop. The desktop is usually different from one computer to another. This is because some
