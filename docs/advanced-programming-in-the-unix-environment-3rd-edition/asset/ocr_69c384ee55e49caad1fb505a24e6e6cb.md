char *getenv(const char *name);
<stdlib.h>
Returns: pointer to value associated with name, NULL if not found
p. 210

uid_t geteuid(void);
<unistd.h>
Returns: effective user ID of calling process
p. 228

gid_t getgid(void);
<unistd.h>
Returns: real group ID of calling process
p. 228

struct group *getgrent(void);
<grp.h>
Returns: pointer if OK, NULL on error or end of file
p. 183

struct group *getgrgid(gid_t gid);
<grp.h>
Returns: pointer if OK, NULL on error
p. 162

struct group *getgrnam(const char *name);
<grp.h>
Returns: pointer if OK, NULL on error
p. 182

int getgroups(int gidsetsize, gid_t grouplist[]);
<unistd.h>
Returns: number of supplementary group IDs if OK, -1 on error
p. 184

struct hostent *gethostent(void);
<netdb.h>
Returns: pointer if OK, NULL on error
p. 597

int gethostname(char *name, int namelen);
<unistd.h>
Returns: 0 if OK, -1 on error
p. 188

char *getlogin(void);
<unistd.h>
Returns: pointer to string giving login name if OK, NULL on error
p. 275