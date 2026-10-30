
The user processes that call the functions in the database library to perform I/O are considered cooperating processes, since they use byte-range locking to provide concurrent access.

## 20.6 Concurrency

We purposely chose a two-file implementation (an index file and a data file) because that is a common implementation technique (it simplifies space management in the files). It requires us to handle the locking interactions of both files. But there are numerous ways to handle the locking of these two files.

### Coarse-Grained Locking

The simplest form of locking is to use one of the two files as a lock for the entire database and to require the caller to obtain this lock before operating on the database. We call this coarse-grained locking. For example, we can say that the process with a read lock on byte 0 of the index file has read access to the entire database. A process with a write lock on byte 0 of the index file has write access to the entire database. We can use the normal UNIX System byte-range locking semantics to allow any number of readers at one time, but only one writer at a time. (Recall Figure 14.3.) The functions db_fetch and db_nextrec require a read lock, and db_delete, db_store, and db_open all require a write lock. (The reason db_open requires a write lock is that if the file is being created, it has to write the empty free list and hash chains at the front of the index file.)

The problem with coarse-grained locking is that it limits concurrency. If a process is adding a record to one hash chain, another process should be able to read a record on a different hash chain.

### Fine-Grained Locking

We enhance coarse-grained locking to allow more concurrency and call this fine-grained locking. We first require a reader or a writer to obtain a read lock or a write lock on the hash chain for a given record. We allow any number of readers at one time on any hash chain but only a single writer on a hash chain. Next, a writer needing to access the free list (either db_delete or db_store) must obtain a write lock on the free list. Finally, whenever it appends a new record to the end of either the index file or the data file, db_store has to obtain a write lock on that portion of the file.

We expect fine-grained locking to provide more concurrency than coarse-grained locking. In Section 20.9, we show some actual measurements. In Section 20.8, we show the source code for our implementation of fine-grained locking and discuss the details of implementing locking. (Coarse-grained locking is merely a simplification of the locking that we show.)

In the source code, we call read, readv, write, and writev directly. We do not use the standard I/O library. Although it is possible to use byte-range locking with the standard I/O library, careful handling of buffering is required. We don’t want an

fgets, for example, to return data that was read into a standard I/O buffer 10 minutes ago if the data was modified by another process 5 minutes ago.

Our discussion of concurrency is predicated on the simple needs of the database library. Commercial systems often have additional requirements. See Chapter 16 of Date [2004] for additional details on concurrency.

## 20.7 Building the Library

The database library consists of two files: a public C header file and a C source file. We can build a static library using the commands

```
gcc -I../include -Wall -c db.c
ar rsv libapue_db.a db.o
```

Applications that want to link with libapue_db.a will also need to link with libapue.a, since we use some of our common functions in the database library.

If, on the other hand, we want to build a dynamic shared library version of the database library, we can use the following commands:

```
gcc -I../include -Wall -fPIC -c db.c
gcc -shared -Wl,-soname,libapue_db.so.1 -o libapue_db.so.1 \
-I../ -L../lib -lapue -lc db.o
```

The resulting shared library, libapue_db.so.1, needs to be placed in a common directory where the dynamic linker/loader can find it. Alternatively, we can place it in a private directory and modify our LD_LIBRARY_PATH environment variable to include the private directory in the search path of the dynamic linker/loader.

> The steps used to build shared libraries vary among platforms. Here, we have shown how to do it on a Linux system with the GNU C compiler.

## 20.8 Source Code

We start by showing the apue_db.h header. This header is included by the library source code and all applications that call the library.

For the remainder of this text, we depart from the style of the previous examples in several ways. First, because the source code example is longer than usual, we number the lines. This makes it easier to link the discussion with the corresponding source code. Second, we place the description of the source code immediately below the source code on the same page.

> This style was inspired by John Lions in his book documenting the UNIX Version 6 operating system source code [Lions 1977, 1996]. It simplifies the task of studying large amounts of source code.

Note that we do not bother to number blank lines. Although this departs from the normal behavior of such tools as pr(1), we have nothing interesting to say about blank lines.

```
```c
#ifndef _APUE_DB_H
#define _APUE_DB_H

typedef    void *  DBHANDLE;

DBHANDLE   db_open(const char *, int, ...);
void       db_close(DBHANDLE);
char      *db_fetch(DBHANDLE, const char *);
int        db_store(DBHANDLE, const char *, const char *, int);
int        db_delete(DBHANDLE, const char *);
void       db_rewind(DBHANDLE);
char      *db_nextrec(DBHANDLE, char *);

/*
 * Flags for db_store().
 */
#define DB_INSERT     1    /* insert new record only */
#define DB_REPLACE    2    /* replace existing record */
#define DB_STORE      3    /* replace or insert */

/*
 * Implementation limits.
 */
#define IDXLEN_MIN    6    /* key, sep, start, sep, length, \n */
#define IDXLEN_MAX 1024    /* arbitrary */
#define DATLEN_MIN    2    /* data byte, newline */
#define DATLEN_MAX 1024    /* arbitrary */

#endif /* _APUE_DB_H */
```
```

[1–3] We use the _APUE_DB_H symbol to ensure that the contents of the header file are included only once. The DBHANDLE type represents an active reference to the database and is used to isolate applications from the implementation details of the database. Compare this technique with the way the standard I/O library exposes the FILE structure to applications.

[4–10] Next, we declare the prototypes for the database library’s public functions. Since this header is included by applications that want to use the library, we don’t declare the prototypes for the library’s private functions here.

[11–24] The legal flags that can be passed to the db_store function are defined next, followed by fundamental limits of the implementation. These limits can be changed, if desired, to support bigger databases.

The minimum index record length is specified by IDXLEN_MIN. This represents a 1-byte key, a 1-byte separator, a 1-byte starting offset, another 1-byte separator, a 1-byte length, and a terminating newline character. (Recall the format of an index record from Figure 20.2.) An index record will usually be larger than IDXLEN_MIN bytes, but this is the bare minimum size.

The next file is `db.c`, the C source file for the library. For simplicity, we include all functions in a single file. This has the advantage that we can hide private functions by declaring them as `static`.

```
```c
#include "apue.h"
#include "apue_db.h"
#include <fcntl.h>      /* open & db_open flags */
#include <stdarg.h>
#include <errno.h>
#include <sys/uio.h>     /* struct iovec */

/*
 * Internal index file constants.
 * These are used to construct records in the
 * index file and data file.
 */
#define IDX_LEN_SZ    4    /* index record length (ASCII chars) */
#define SEP           ':'  /* separator char in index record */
#define SPACE         ' '  /* space character */
#define NEWLINE       '\n' /* newline character */

/*
 * The following definitions are for hash chains and free
 * list chain in the index file.
 */
#define PTR_SZ        7    /* size of ptr field in hash chain */
#define PTR_MAX  9999999  /* max file offset = 10**PTR_SZ - 1 */
#define NHASH_DEF    137   /* default hash table size */
#define FREE_OFF       0   /* free list offset in index file */
#define HASH_OFF PTR_SZ_SZ /* hash table offset in index file */

typedef unsigned long DBHASH; /* hash values */
typedef unsigned long COUNT;  /* unsigned counter */
```
```

We include `apue.h` because we use some of the functions from our private library. In turn, `apue.h` includes several standard headers, including `<stdio.h>` and `<unistd.h>`. We include `<stdarg.h>` because the `db_open` function uses the variable-argument functions declared by `<stdarg.h>`.

The size of an index record is specified by `IDX_LEN_SZ`. We use some characters, such as colon and newline, as delimiters in the database. We use the space character as “white out” when we delete a record.

Some of the values that we have defined as constants could also be made variable, with some added complexity in the implementation. For example, we set the size of the hash table to 137 entries. A better technique would be to let the caller specify this as an argument to `db_open`, based on the expected size of the database. We would then have to store this size at the beginning of the index file.
