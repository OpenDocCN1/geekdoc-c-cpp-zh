int fflush(FILE *fp);
<stdio.h>
Returns: 0 if OK, EOF on error
p. 147

int fgetc(FILE *fp);
<stdio.h>
Returns: next character if OK, EOF on end of file or error
p. 150

int fgetpos(FILE *restrict fp, fpos_t *restrict pos);
<stdio.h>
Returns: 0 if OK, nonzero on error
p. 158

char *fgets(char *restrict buf, int n, FILE *restrict fp);
<stdio.h>
Returns: buf if OK, NULL on end of file or error
p. 152

int fileno(FILE *fp);
<stdio.h>
Returns: file descriptor associated with the stream, -1 on error
p. 164

void flockfile(FILE *fp);
<stdio.h>
p. 443

FILE *fmemopen(void *restrict buf, size_t size, const char *restrict type);
<stdio.h>
type: "r", "w", "a", "r+", "w+", "a+"
Returns: stream pointer if OK, NULL on error
p. 171

FILE *fopen(const char *restrict path, const char *restrict type);
<stdio.h>
type: "r", "w", "a", "r+", "w+", "a+"
Returns: file pointer if OK, NULL on error
p. 148

pid_t fork(void);
<unistd.h>
Returns: 0 in child, process ID of child in parent, -1 on error
p. 229

long fpathconf(int fd, int name);
<unistd.h>
name: _PC_ASYNC_IO, _PC_CHOWN_RESTRICTED, _PC_FILESIZEBITS, _PC_LINK_MAX, _PC_MAX_CANON, _PC_MAX_INPUT, _PC_NAME_MAX, _PC_NO_TRUNC, _PC_PATH_MAX, _PC_PIPE_BUF, _PC_PRIO_IO, _PC_SYMLINK_MAX, _PC_SYNC_IO, _PC_TIMESTAMP_RESOLUTION, _PC_2_SYMLINKS, _PC_VDISABLE
Returns: corresponding value if OK, -1 on error