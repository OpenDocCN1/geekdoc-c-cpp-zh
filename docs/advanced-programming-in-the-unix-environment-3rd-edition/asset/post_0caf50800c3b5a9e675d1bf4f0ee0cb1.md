
```c
#include <unistd.h>
int getgroups(int gidsetsize, gid_t grouplist[]);
Returns: number of supplementary group IDs if OK, -1 on error

#include <grp.h>    /* on Linux */
#include <unistd.h> /* on FreeBSD, Mac OS X, and Solaris */
int setgroups(int ngroups, const gid_t grouplist[]);
#include <grp.h>    /* on Linux and Solaris */
#include <unistd.h> /* on FreeBSD and Mac OS X */
int initgroups(const char *username, gid_t basegid);
Both return: 0 if OK, -1 on error
```

Of these three functions, only getgroups is specified by POSIX.1. Because setgroups and initgroups are privileged operations, they are not part of POSIX.1. All four platforms covered in this book support all three functions, but on Mac OS X 10.6.8, basegid is declared to be of type int.

The getgroups function fills in the array grouplist with the supplementary group IDs. Up to gidsetsize elements are stored in the array. The number of supplementary group IDs stored in the array is returned by the function.

As a special case, if gidsetsize is 0, the function returns only the number of supplementary group IDs. The array grouplist is not modified. (This allows the caller to determine the size of the grouplist array to allocate.)

The setgroups function can be called by the superuser to set the supplementary group ID list for the calling process: grouplist contains the array of group IDs, and ngroups specifies the number of elements in the array. The value of ngroups cannot be larger than NGROUPS_MAX.

The setgroups function is usually called from the initgroups function, which reads the entire group file—with the functions getgrent, setgrent, and endgrent, which we described earlier—and determines the group membership for username. It then calls setgroups to initialize the supplementary group ID list for the user. One must be superuser to call initgroups, since it calls setgroups. In addition to finding all the groups that username is a member of in the group file, initgroups includes basegid in the supplementary group ID list; basegid is the group ID from the password file for username.

The initgroups function is called by only a few programs. The login(1) program, for example, calls it when we log in.

## 6.6 Implementation Differences

We’ve already discussed the shadow password file supported by Linux and Solaris. FreeBSD and Mac OS X store encrypted passwords differently. Figure 6.5 summarizes how the four platforms covered in this book store user and group information.

| Information | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
|---|---|---|---|---|
| account information | /etc/passwd | /etc/passwd | Directory Services | /etc/passwd |
| encrypted passwords | /etc/master.passwd | /etc/shadow | Directory Services | /etc/shadow |
| hashed password files? | yes | no | no | no |
| group information | /etc/group | /etc/group | Directory Services | /etc/group |

### Figure 6.5 Account implementation differences

On FreeBSD, the shadow password file is /etc/master.passwd. Special commands are used to edit it, which in turn generate a copy of /etc/passwd from the shadow password file. In addition, hashed versions of the files are generated: /etc/pwd.db is the hashed version of /etc/passwd, and /etc/spwd.db is the hashed version of /etc/master.passwd. These provide better performance for large installations.

On Mac OS X, however, /etc/passwd and /etc/master.passwd are used only in single-user mode (when the system is undergoing maintenance; single-user mode usually means that no system services are enabled). In multiuser mode—during normal operation—the Directory Services daemon provides access to account information for users and groups.

Although Linux and Solaris support similar shadow password interfaces, there are some subtle differences. For example, the integer fields shown in Figure 6.3 are defined as type int on Solaris, but as long int on Linux. Another difference is the account-inactive field: Solaris defines it to be the number of days since the user last logged in to the system after which the account will be automatically disabled, whereas Linux defines it to be the number of days after the maximum password age has been reached during which the password will still be accepted.

On many systems, the user and group databases are implemented using the Network Information Service (NIS). This allows administrators to edit a master copy of the databases and distribute them automatically to all servers in an organization. Client systems contact servers to look up information about users and groups. NIS+ and the Lightweight Directory Access Protocol (LDAP) provide similar functionality. Many systems control the method used to administer each type of information through the /etc/nsswitch.conf configuration file.

## 6.7 Other Data Files

We’ve discussed only two of the system’s data files so far: the password file and the group file. Numerous other files are used by UNIX systems in normal day-to-day operation. For example, the BSD networking software has one data file for the services provided by the various network servers (/etc/services), one for the protocols (/etc/protocols), and one for the networks (/etc/networks). Fortunately, the interfaces to these various files are like the ones we’ve already described for the password and group files.

The general principle is that every data file has at least three functions:

- 1. A get function that reads the next record, opening the file if necessary. These functions normally return a pointer to a structure. A null pointer is returned when the end of file is reached. Most of the get functions return a pointer to a static structure, so we always have to copy the structure if we want to save it.
- 2. A set function that opens the file, if not already open, and rewinds the file. We use this function when we know we want to start again at the beginning of the file.
- 3. An end entry that closes the data file. As we mentioned earlier, we always have to call this function when we’re done, to close all the files.

Additionally, if the data file supports some form of keyed lookup, routines are provided to search for a record with a specific key. For example, two keyed lookup routines are provided for the password file: getpwnam looks for a record with a specific user name, and getpwuid looks for a record with a specific user ID.

Figure 6.6 shows some of these routines, which are common to UNIX systems. In this figure, we show the functions for the password files and group file, which we discussed earlier in this chapter, and some of the networking functions. There are get, set, and end functions for all the data files in this figure.

| Description | Data file | Header | Structure | Additional keyed lookup functions |
|---|---|---|---|---|
| passwords | /etc/passwd | <pwd.h> | passwd | getpwnam, getpwuid |
| groups | /etc/group | <grp.h> | group | getgrnam, getgrgid |
| shadow | /etc/shadow | <shadow.h> | spwd | getspnam |
| hosts | /etc/hosts | <netdb.h> | hostent | getnameinfo, getaddrinfo |
| networks | /etc/networks | <netdb.h> | netent | getnetbyname, getnetbyaddr |
| protocols | /etc/protocols | <netdb.h> | protoent | getprotobyname, getprotobynumber |
| services | /etc/services | <netdb.h> | servent | getservbyname, getservbyport |

### Figure 6.6 Similar routines for accessing system data files

Under Solaris, the last four data files in Figure 6.6 are symbolic links to files of the same name in the directory /etc/inet. Most UNIX System implementations have additional functions that are like these, but the additional functions tend to deal with system administration files and are specific to each implementation.

## 6.8 Login Accounting

Two data files provided with most UNIX systems are the utmp file, which keeps track of all the users currently logged in, and the wtmp file, which keeps track of all logins and logouts. With Version 7, one type of record was written to both files, a binary record consisting of the following structure:
