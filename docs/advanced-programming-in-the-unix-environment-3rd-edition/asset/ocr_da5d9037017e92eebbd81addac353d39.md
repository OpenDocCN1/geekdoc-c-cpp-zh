void **_exit**(int status);  
`<unistd.h>`  
This function never returns

void **exit**(int status);  
`<stdlib.h>`  
This function never returns

int **faccessat**(int *fd*, const char **path*, int *mode*, int *flag*);  
`<unistd.h>`  
*mode*: R_OK, W_OK, X_OK, F_OK  
*flag*: AT_EACCESS  
Returns: 0 if OK, −1 on error

int **fchdir**(int *fd*);  
`<unistd.h>`  
Returns: 0 if OK, −1 on error

int **fchmod**(int *fd*, mode_t *mode*);  
`<sys/stat.h>`  
*mode*: S_IS[UG]ID, S_ISVTX,  
        S_IR[WX] | S_I[USR|GRP|OTH]  
Returns: 0 if OK, −1 on error

int **fchmodat**(int *fd*, const char **path*, mode_t *mode*, int *flag*);  
`<sys/stat.h>`  
*mode*: S_IS[UG]ID, S_ISVTX,  
        S_IR[WX] | S_I[USR|GRP|OTH]  
*flag*: AT_SYMLINK_NOFOLLOW  
Returns: 0 if OK, −1 on error

int **fchown**(int *fd*, uid_t *owner*, gid_t *group*);  
`<unistd.h>`  
Returns: 0 if OK, −1 on error

int **fchownat**(int *fd*, const char **path*, uid_t *owner*,  
        gid_t *group*, int *flag*);  
`<unistd.h>`  
*flag*: AT_SYMLINK_NOFOLLOW  
Returns: 0 if OK, −1 on error

int **fclose**(FILE **fp*);  
`<stdio.h>`  
Returns: 0 if OK, EOF on error