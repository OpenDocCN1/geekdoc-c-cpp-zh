| Function | Prototype | Header | Description |
|---|---|---|---|
| fsetpos() | int fsetpos(FILE *flw, const fpos_t *pos); | stdio.h | positioning pos * |
| ftell() | long int ftell(FILE *flw); | stdio.h | positioning from zero |
| fwrite() | size_t fwrite(const void *pt, size_t tam,size_t n, FILE *flw); | stdio.h | writing to the file |
| getc() | int getc(FILE *flw); | stdio.h | reading characters |
| getch() | int getch(void); | conio.h | reading characters |
| getchar() | int getchar(void) | stdio.h | reading characters |
| getche() | int getche(void) | conio.h | reading characters |
| getenv() | char *getenv(const char *name); | stdlib.h | environmental information |
| gets() | char *gets(char *s); | stdio.h | string read |
| gmtime() | struct tm *gmtime(const time_t *hor); | time.h | Greenwich Mean Time |
| inp() | int inp(int n); | conio.h | door byte |
| isalnum | int isalnum(int c); | ctype.h | character test (A-Z, a-z, 0-9) |
| isalpha() | int isalpha(int c); | ctype.h | test (A-Z, a-z) |
| iscntrl() | int iscntrl(int c); | ctype.h | test (0-31 or 127) |
| isdigit() | int isdigit(int c); | ctype.h | test (0-9) |
| isgraph() | int isgraph(int c); | ctype.h | test (minus 32) |
| islower() | int islower(int c); | ctype.h | test (a-z) |
| isprint() | int isprint(int c); | ctype.h | test (32-126) |
| ispunct() | int ispunct(int c); | ctype.h | test (32-47,58-63, 91-96,123-126) |
| isspace() | int isspace(int c); | ctype.h | teste (se espaço) |
| isupper() | int isupper(int c); | ctype.h | teste (A-Z) |
| isxdigit() | int isxdigit(int c); | ctype.h | teste (0-9,A-F,a-f) |
| kbhit() | int kbhit(void); | conio.h | character test (if