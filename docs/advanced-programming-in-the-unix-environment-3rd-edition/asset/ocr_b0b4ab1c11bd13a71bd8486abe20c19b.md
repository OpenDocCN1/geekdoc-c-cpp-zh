Both functions return a pointer to a passwd structure that the functions fill in. This structure is usually a static variable within the function, so its contents are overwritten each time we call either of these functions.

These two POSIX.1 functions are fine if we want to look up either a login name or a user ID, but some programs need to go through the entire password file. Three functions can be used for this purpose: getpwent, setpwent, and endpwent.

```
#include <pwd.h>

struct passwd *getpwent(void);

Returns: pointer if OK, NULL on error or end of file

void setpwent(void);
void endpwent(void);
```

These three functions are not part of the base POSIX.1 standard. They are defined as part of the XSI option in the Single UNIX Specification. As such, all UNIX systems are expected to provide them.

We call getpwent to return the next entry in the password file. As with the two POSIX.1 functions, getpwent returns a pointer to a structure that it has filled in. This structure is normally overwritten each time we call this function. If this is the first call to this function, it opens whatever files it uses. There is no order implied when we use this function; the entries can be in any order, because some systems use a hashed version of the file /etc/passwd.

The function setpwent rewinds whatever files it uses, and endpwent closes these files. When using getpwent, we must always be sure to close these files by calling endpwent when we’re through. Although getpwent is smart enough to know when it has to open its files (the first time we call it), it never knows when we’re through.

# Example

Figure 6.2 shows an implementation of the function getpwnam.

```
#include <pwd.h>
#include <stddef.h>
#include <string.h>

struct passwd *
getpwnam(const char *name)
{
    struct passwd *ptr;
    setpwent();
    while (((ptr = getpwent()) != NULL))
        if (strcmp(name, ptr->pw_name) == 0)
            break;      /* found a match */
    endpwent();
    return(ptr);    /* ptr is NULL if no match found */
}
```

Figure 6.2 The getpwnam function