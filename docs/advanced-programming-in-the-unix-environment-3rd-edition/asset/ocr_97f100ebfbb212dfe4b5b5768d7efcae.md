The oflag argument is a bitmask that specifies how the master device is to be opened, similar to the same argument used with open(2). Not all open flags are supported, however. With posix_openpt, we can specify O_RDWR to open the master device for reading and writing, and we can specify O_NOCTTY to prevent the master device from becoming a controlling terminal for the caller. All other open flags result in unspecified behavior.

Before a slave pseudo terminal device can be used, its permissions need to be set so that it is accessible to applications. The grantpt function does just this. It sets the user ID of the slave’s device node to the caller’s real user ID and sets the node’s group ID to an unspecified value, usually some group that has access to terminal devices. The permissions are set to allow read and write access to individual owners and write access to group owners (0620).

Implementations commonly set the group ownership of the slave PTY device to group tty. Programs that need permission to write to all active terminals on the system are set-group-ID to the group tty. Examples of such programs are wall(1) and write(1). Because the group write permission is enabled on slave PTY devices, these programs can write to them.

```
#include <stdlib.h>
int grantpt(int fd);
int unlockpt(int fd);

Both return: 0 on success, -1 on error
```

To change permission on the slave device node, grantpt might need to fork and exec a set-user-ID program (/usr/lib/pt_chmod on Solaris, for example). Thus, the behavior is unspecified if the caller is catching SIGCHLD.

The unlockpt function is used to grant access to the slave pseudo terminal device, thereby allowing applications to open the device. By preventing others from opening the slave device, applications setting up the devices have an opportunity to initialize the slave and master devices properly before they can be used.

Note that in both grantpt and unlockpt, the file descriptor argument is the file descriptor associated with the master pseudo terminal device.

The ptsname function is used to find the pathname of the slave pseudo terminal device, given the file descriptor of the master. This allows applications to identify the slave independent of any particular conventions that might be followed by a given platform. Note that the name returned might be stored in static memory, so it can be overwritten on successive calls.

```
#include <stdlib.h>
char *ptsname(int fd);

Returns: pointer to name of PTY slave if OK, NULL on error
```

Figure 19.8 summarizes the pseudo terminal functions in the Single UNIX Specification and indicates which functions are supported by the platforms discussed in this text.