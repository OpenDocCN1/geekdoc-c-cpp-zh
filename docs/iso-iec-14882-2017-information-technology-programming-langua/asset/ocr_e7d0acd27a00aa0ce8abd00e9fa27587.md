# ISO/IEC 14882:2017(E)

4 Remarks: Pathname resolution terminates if p names a symbolic link.

5 Throws: As specified in 30.10.7.

# 30.10.15.38 Temporary directory path

```
path temp_directory_path();
path temp_directory_path(error_code ec);
```

1 Returns: An unspecified directory suitable for temporary files. An error will be reported if exists(p) is false or is_directory(p) is false, where p is the path to be returned. The signature with argument ec returns path() if an error occurs.

2 Throws: As specified in 30.10.7.

3 Example: For POSIX-based operating systems, an implementation might return the path supplied by the first environment variable found in the TMPDIR, TMP, TEMP, TMPDIR, or if none of these are found, "tmp".
For Windows-based operating systems, an implementation might return the path reported by the Windows GetTempPath function. — example ec

# 30.10.15.39 Weakly canonical

```
path weakly_canonical(const path p);
path weakly_canonical(const path p, error_code ec);
```

1 Returns: p with symlinks resolved and the result monitored (30.10.4).

2 Effects: Using status(p) or status(p), respectively, to determine, return a path composed by the result of calling canonical() without a base argument and with a path argument composed of the leading elements of p that, if any. For the first form, canonical() is called without a base argument and an error_code argument is returned by the elements of p that do not exist. For the second form, canonical() is called with ec as an error_code argument, and path() is returned at the first error occurrence, if any.

3 Postconditions: The returned path is in normal form (30.10.4).

4 Remarks: Implementations should avoid unnecessary normalization such as when canonical has already been on the entirety of p.

5 Throws: As specified in 30.10.7.

# 30.11.1 C libraries

# Header <cstdio> synopsis

```
#define NULL see 21.2.3
#define IOBFS see below
#define TOLSEF see below
#define IONBF see below
#define BUFFSIZE see below
#define EOF see below
#define FOPEN_MAX see below
#define FILENAME_MAX see below
#define L_tnam see below
#define SEEK_CTR see below
#define SEEK_END see below
#define SEEK_SET see below
#define TMP_MAX see below
#define stderr see below
```

§ 30.11.1 ©ISO/IEC 2017 – All rights reserved 1288