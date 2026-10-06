
# ISO/IEC 14882:2017(E)

(6.1.2) Otherwise, if the specific error indicates that p can be resolved then the attributes cannot be determined, returns file_status(file_type::unknown).

(6.1.3) Otherwise, returns file_status(file_type::none).

[Note: These semantics distinguish between p known not to exist, p existing but not being able to determine its attributes, and there is an error that prevents even if p exists. These distinctions are important to use cases. -- end note]

(6.2) Otherwise,

(6.2.1) If the attributes indicate a regular file, as by POSIX S_REG, returns file_status(file_type::regular, prms). [Note: file_type::regular implies appropriate <stream> operations would succeed, assuming no hardware, permission, or file system errors. Lack of file_type does not necessarily imply <stream> operations would fail in a directory. -- end note]

(6.2.2) Otherwise, if the attributes indicate a directory, as by POSIX S_ISDIR, returns file_status(file_type::directory, prms). -- end note]

(6.2.3) Otherwise, if the attributes indicate a special file, as by POSIX S_ISBLK, returns file_status(file_type::block, prms).

(6.2.4) Otherwise, if the attributes indicate a character file special, as by POSIX S_ISCHR, returns file_status(file_type::character, prms).

(6.2.5) Otherwise, if the attributes indicate a pipe or fifo file, as by POSIX S_IFIFO, returns file_status(file_type::fifo, prms).

(6.2.6) Otherwise, if the attributes indicate a socket, as by POSIX S_ISSOCK, returns file_status(file_type::socket, prms).

(6.2.7) Otherwise, if the attributes indicate an implementation-defined type (type 30.10.10), returns file_status(file_type::_A, prms).

(6.2.8) Otherwise, returns file_status(file_type::unknown, prms).

7 Remarks: If a symbolic link is encountered during pathname resolution, pathname resolution continues using the contents of the symbolic link.

## 30.10.15.36 Status known

```cpp
bool file_status(file_status s) noexcept
// Returns: s.type() == file_type::none;
```

## 30.10.15.37 Symbolic link

```cpp
file_symlink_status(const path& p, error_code& ec) noexcept
```

Effects: Same as status(), above, except that the attributes of p are determined as if using POSIX stat() to obtain a POSIX struct.

2 Let prms denote the result of (m & mask); where m is determined as by converting the st_mode of the obtained struct to type prms.

3 Returns: Same as status(), above, except that the attributes indicate a symbolic link, as if by POSIX S_ISLNK, returns file_status(file_type::symlink, prms). The signature with argument ec returns file_status(file_type::none) if an error occurs.

4 Remarks: Pathname resolution terminates if p names a symbolic link.

5 Throws: As specified in 30.10.7.

## 30.10.15.38 Temporary directory path

```cpp
path temp_directory_path();
path temp_directory_path(error_code ec);
```

1 Returns: An unspecified directory suitable for temporary files. An error will be reported if exists(p) is false or is_directory(p) is false, where p is the path to be returned. The signature with argument ec returns path() if an error occurs.

2 Throws: As specified in 30.10.7.

3 Example: For POSIX-based operating systems, an implementation might return the path supplied by the first environment variable found in the TMPDIR, TMP, TEMP, TMPDIR, or if none of these are found, "tmp".
For Windows-based operating systems, an implementation might return the path reported by the Windows GetTempPath function. — example ec

## 30.10.15.39 Weakly canonical

```cpp
path weakly_canonical(const path p);
path weakly_canonical(const path p, error_code ec);
```

1 Returns: p with symlinks resolved and the result monitored (30.10.4).

2 Effects: Using status(p) or status(p), respectively, to determine, return a path composed by the result of calling canonical() without a base argument and with a path argument composed of the leading elements of p that, if any. For the first form, canonical() is called without a base argument and an error_code argument is returned by the elements of p that do not exist. For the second form, canonical() is called with ec as an error_code argument, and path() is returned at the first error occurrence, if any.

3 Postconditions: The returned path is in normal form (30.10.4).

4 Remarks: Implementations should avoid unnecessary normalization such as when canonical has already been on the entirety of p.

5 Throws: As specified in 30.10.7.

## 30.11.1 C libraries

### Header <cstdio> synopsis

```cpp
#define NULL        see 21.2.3
#define IOBFS       see below
#define TOLSEF      see below
#define IONBF       see below
#define BUFFSIZE    see below
#define EOF         see below
#define FOPEN_MAX   see below
#define FILENAME_MAX see below
#define L_tnam      see below
#define SEEK_CTR    see below
#define SEEK_END    see below
#define SEEK_SET    see below
#define TMP_MAX     see below
#define stderr      see below
#define stdin       see below
#define stdout      see below
```

```cpp
namespace stdd {
    size_t t = see 21.2.4;
    using FILE = see below;
    using fpos_t = see below;

    int remove(const char* filename);
    int rename(const char* old, const char* new);
    int tmpfile();
    int int(const char* s);
    int fclose(FILE* stream);
    int fflush(FILE* stream);
    int fopen(const char* filename, const char* mode);
    int freopen(const char* filename, const char* mode);
    void setbuf(FILE* stream, char* buf);
    int fprintf(FILE* stream, const char* format);
    int fputs(FILE* stream, char* s);
    int sprintf(FILE* stream, const char* format);
    int scanf(FILE* stream, const char* format);
    int vfprintf(FILE* stream, const char* format);
    int vprintf(FILE* stream, const char* format);
    int vscanf(FILE* stream, const char* format);
    int getc(FILE* stream);
    char getcs(FILE* stream, char* s);
    int putc(int c, FILE* stream);
    int puts(const char* s);
    int ungetc(FILE* stream, int c);
    size_t fread(void* ptr, size_t size, size_t n, FILE* stream);
    int fpos(FILE* stream, fpos_t* pos);
    int fseek(FILE* stream, long offset, int whence);
    long intell(FILE* stream);
    void rewind(FILE* stream);
    void clearerr(FILE* stream);
    int feof(FILE* stream);
    int error(FILE* stream);
    void perror(const char* s);
}
```

> The contents of the header <stdio> are the same as the C standard library <stdio.h>.
