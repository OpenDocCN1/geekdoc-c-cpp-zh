

调用数据库库中执行 I/O 的函数<|message|>的用户进程被视为协作进程，因为它们使用字节范围锁定来提供并发访问。

## 20.6 并发

我们特意选择了两文件实现（一个索引文件和一个数据文件），因为这是一种常见的实现技术（它简化了文件中的空间管理）。它要求我们处理两个文件的锁定交互。但有多种方法可以处理这两个文件的锁定。

### 粗粒度锁定

最简单的锁定形式是使用两个文件之一作为整个数据库的锁，并要求调用者在操作数据库之前获得此锁。我们称之为粗粒度锁定。例如，我们可以说在索引文件的字节 0 上持有读锁的进程对整个数据库具有读访问权限。持有索引文件字节 0 上的写锁的进程对整个数据库具有写访问权限。我们可以使用正常的 UNIX 系统字节范围锁定语义来允许同时有任意数量的读者，但同时只能有一个写者。（参见图 14.3。）函数 db_fetch 和 db_nextrec 需要读锁，而 db_delete、db_store 和 db_open 都需要写锁。（db_open 需要写锁的原因是，如果文件正在创建，它必须在索引文件的前面写入空闲列表和哈希链。）

粗粒度锁定的问题在于它限制了并发。如果一个进程正在向一个哈希链添加记录，另一个进程应该能够读取不同哈希链上的记录。

### 细粒度锁定

我们增强粗粒度锁定以允许更多并发，并称之为细粒度锁定。我们首先要求读者或写者获得对给定记录的哈希链的读锁或写锁。我们允许在任何哈希链上同时有任意数量的读者，但在一个哈希链上只有一个写者。接下来，需要访问空闲列表（db_delete 或 db_store）的写者必须获得空闲列表上的写锁。最后，每当 db_store 将新记录追加到索引文件或数据文件的末尾时，它必须获得该文件部分上的写锁。

我们期望细粒度锁定比粗粒度锁定提供更多并发。在第 20.9 节中，我们展示了一些实际测量结果。在第 20.8 节中，我们展示了细粒度锁定的实现源代码，并讨论了实现锁定的细节。（粗粒度锁定只是我们所展示的锁定的简化。）

在源代码中，我们直接调用 read、readv、write 和 writev。我们不使用标准 I/O 库。虽然可以使用标准 I/O 库进行字节范围锁定，但需要仔细处理缓冲。我们不希望

fgets，例如，在 10 分钟前读入标准 I/O 缓冲区的数据返回，如果该数据在 5 分钟前已被另一个进程修改。

我们对并发的讨论基于数据库库的简单需求。商业系统通常有额外的要求。有关并发的更多详细信息，请参阅 Date [2004] 的第 16 章。

## 20.7 构建库

数据库库由两个文件组成：一个公共 C 头文件和一个 C 源文件。我们可以使用以下命令构建静态库

```
gcc -I../include -Wall -c db.c
ar rsv libapue_db.a db.o
```

想要链接 libapue_db.a 的应用程序也需要链接 libapue.a，因为我们在数据库库中使用了一些通用函数。

如果我们想构建数据库库的动态共享库版本，我们可以使用以下命令：

```
gcc -I../include -Wall -fPIC -c db.c
gcc -shared -Wl,-soname,libapue_db.so.1 -o libapue_db.so.1 \
-I../ -L../lib -lapue -lc db.o
```

生成的共享库 libapue_db.so.1 需要放置在动态链接器/加载器可以找到的公共目录中。或者，我们可以将其放置在私有目录中，并修改我们的 LD_LIBRARY_PATH 环境变量以将私有目录包含在动态链接器/加载器的搜索路径中。

> 用于构建共享库的步骤因平台而异。在这里，我们展示了如何在 Linux 系统上使用 GNU C 编译器执行此操作。

## 20.8 源代码

我们首先展示 apue_db.h 头文件。此头文件由库源代码和所有调用库的应用程序包含。

对于本文的其余部分，我们在几个方面偏离了之前示例的风格。首先，由于源代码示例通常较长，我们对行进行编号。这使得将讨论与相应的源代码联系起来变得更容易。其次，我们将源代码的描述立即放在源代码下方，放在同一页上。

> 这种风格受到了 John Lions 在其记录 UNIX 第 6 版操作系统源代码的书籍中的启发 [Lions 1977, 1996]。它简化了研究大量源代码的任务。

请注意，我们不费心对空白行进行编号。虽然这偏离了诸如 pr(1) 之类的工具的正常行为，但我们对空白行没有什么有趣的话要说。

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

[1–3] 我们使用 _APUE_DB_H 符号来确保头文件的内容只包含一次。DBHANDLE 类型表示对数据库的活动引用，并用于将应用程序与数据库的实现细节隔离开来。将此技术与标准 I/O 库向应用程序公开 FILE 结构的方式进行比较。

[4–10] 接下来，我们声明数据库库公共函数的原型。由于此头文件包含在想要使用库的应用程序中，因此我们在此处不声明库的私有函数的原型。

[11–24] 接下来定义可以传递给 db_store 函数的合法标志，然后是实现的根本限制。如果需要，可以更改这些限制以支持更大的数据库。

索引记录的最小长度由 IDXLEN_MIN 指定。这代表一个 1 字节的键、一个 1 字节的分隔符、一个 1 字节的起始偏移量、另一个 1 字节的分隔符、一个 1 字节的长度和一个终止换行符。（请回忆图 20.2 中的索引记录格式。）索引记录通常会大于 IDXLEN_MIN 字节，但这是最小的裸尺寸。

下一个文件是 `db.c`，即库的 C 源文件。为了简单起见，我们将所有函数包含在一个文件中。这样做的好处是我们可以通过将它们声明为 `static` 来隐藏私有函数。

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

我们包含 `apue.h`，因为我们使用了我们私有库中的一些函数。反过来，`apue.h` 包含了一些标准头文件，包括 `<stdio.h>` 和 `<unistd.h>`。我们包含 `<stdarg.h>`，因为 `db_open` 函数使用了 `<stdarg.h>` 声明的可变参数函数。

索引记录的大小由 `IDX_LEN_SZ` 指定。我们使用一些字符，例如冒号和换行符，作为数据库中的分隔符。我们使用空格字符作为删除记录时的“涂白”。

我们定义为常量的一些值也可以作为变量实现，只是实现会增加一些复杂性。例如，我们将哈希表的大小设置为 137 个条目。更好的技术是让调用者根据数据库的预期大小将此作为 `db_open` 的参数指定。然后我们必须将此大小存储在索引文件的开头。

