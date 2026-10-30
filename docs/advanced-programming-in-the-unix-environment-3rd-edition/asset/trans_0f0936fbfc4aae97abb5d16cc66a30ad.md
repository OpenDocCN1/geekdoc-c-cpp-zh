

```
27   /*
28   * 库内部对数据库的表示。
29   */
30 typedef struct {
31     int     idxfd;  /* 索引文件的文件描述符 */
32     int     datfd;  /* 数据文件的文件描述符 */
33     char    *idxbuf; /* 为索引记录分配的缓冲区 */
34     char    *datbuf; /* 为数据记录分配的缓冲区 */
35     char    *name;   /* 打开数据库时使用的名称 */
36     off_t   idxoff;  /* 索引文件中索引记录的偏移量 */
                 /* 键位于 (idxoff + PTR_SZ + IDXLEN_SZ) 处 */
37     size_t  idxlen;  /* 索引记录的长度 */
                 /* 不包括记录开头的 IDXLEN_SZ 个字节 */
                 /* 包括索引记录末尾的换行符 */
38     off_t   datoff;  /* 数据文件中数据记录的偏移量 */
39     size_t  datlen;  /* 数据记录的长度 */
                 /* 包括末尾的换行符 */
40     off_t   ptrval;  /* 索引记录中链指针的内容 */
41     off_t   ptroff;  /* 指向此索引记录的链指针偏移量 */
42     off_t   chainoff; /* 此索引记录对应的哈希链偏移量 */
43     off_t   hashoff;  /* 哈希表在索引文件中的偏移量 */
44     DBHASH  nhash;    /* 当前哈希表的大小 */
45     COUNT   cnt_delok;   /* 删除成功 */
46     COUNT   cnt_delerr;  /* 删除失败 */
47     COUNT   cnt_fetchok; /* 获取成功 */
48     COUNT   cnt_fetcher; /* 获取失败 */
49     COUNT   cnt_nextrec; /* nextrec */
50     COUNT   cnt_stor1;   /* 存储：DB_INSERT，无空闲空间，追加 */
51     COUNT   cnt_stor2;   /* 存储：DB_INSERT，找到空闲空间，重用 */
52     COUNT   cnt_stor3;   /* 存储：DB_REPLACE，长度不同，追加 */
53     COUNT   cnt_stor4;   /* 存储：DB_REPLACE，长度相同，覆盖 */
54     COUNT   cnt_storerr; /* 存储失败 */
55 } DB;
```

[27–48] DB 结构用于保存每个已打开数据库的全部信息。`db_open` 返回的 `DBHANDLE` 值，以及其他所有函数使用的 `DBHANDLE` 值，实际上只是指向这些结构之一的指针；不过，我们会对调用者隐藏这一点。

由于我们在数据库中以 ASCII 形式存储指针和长度，因此需要将它们转换为数值，并保存在 DB 结构中。尽管哈希表大小是固定的，我们仍然会保存该值，以防将来决定增强这个库，允许调用者在创建数据库时指定哈希表大小（参见练习 20.7）。

[49–59] DB 结构中最后十个字段用于统计操作成功和失败的次数。如果我们想分析数据库的性能，可以编写一个函数来返回这些统计信息；不过目前我们只维护这些计数器。

```
60  /*
61   * 内部函数。
62   */
63 static DB     *_db_alloc(int);
64 static void   _db_dodelete(DB *);
65 static int    _db_find_and_lock(DB *, const char *, int);
66 static int    _db_findfree(DB *, int, int);
67 static void   _db_free(DB *);
68 static DBHASH _db_hash(DB *, const char *);
69 static char   *_db_readat(DB *);
70 static off_t  _db_readdx(DB *, off_t);
71 static off_t  _db_readptr(DB *, off_t);
72 static void   _db_writedat(DB *, const char *, off_t, int);
73 static void   _db_writeidx(DB *, const char *, off_t, int, off_t);
74 static void   _db_writeptr(DB *, off_t, off_t);

/*
 * 打开或创建数据库。参数与 open(2) 相同。
 */
DBHANDLE
db_open(const char *pathname, int oflag, ...)
{
    DB        *db;
    int       len, mode;
    size_t    i;
    char      asciiptr[PTR_SZ + 1],
              hash[(NHASH_DEF + 1) * PTR_SZ + 2];
              /* +2 表示换行符和空字符 */
    struct stat statbuff;

/*
 * 分配 DB 结构及其所需的缓冲区。
 */
    len = strlen(pathname);
    if ((db = _db_alloc(len)) == NULL)
        err_dump("db_open: _db_alloc error for DB");
```

[60–74] 我们将所有可由用户调用的（公开）函数命名为以 `db_` 开头，将所有内部（私有）函数命名为以 `_db_` 开头。公开函数已在库的头文件 `apue_db.h` 中声明。我们将内部函数声明为 `static`，这样它们就只能被同一文件（即包含库实现的文件）中的函数访问。

[75–93] `db_open` 函数的参数与 `open(2)` 相同。如果调用者要创建数据库文件，可选的第三个参数用于指定文件权限。`db_open` 函数会打开索引文件和数据文件，并在必要时初始化索引文件。该函数首先调用 `_db_alloc` 来分配并初始化 DB 结构。

```
94  db->nhash   = NHASH_DEF; /* 哈希表大小 */
95  db->hashoff = HASH_OFF; /* 哈希表在文件中的偏移量 */
96  strcpy(db->name, pathname);
97  strcat(db->name, ".idx");
98
98  if (oflag & O_CREAT) {
99      va_list ap;
100
101      va_start(ap, oflag);
102      mode = va_arg(ap, int);
103      va_end(ap);
104
105      /*
106       * 打开索引文件和数据文件。
107       */
108      db->idxfd = open(db->name, oflag, mode);
109      strcpy(db->name + len, ".dat");
110      db->datfd = open(db->name, oflag, mode);
111  } else {
112      /*
113       * 打开索引文件和数据文件。
114       */
115      db->idxfd = open(db->name, oflag);
116      strcpy(db->name + len, ".dat");
117      db->datfd = open(db->name, oflag);
118  }
119
120  if (db->idxfd < 0 || db->datfd < 0) {
121      _db_free(db);
122      return(NULL);
123  }
```

[94–97] 我们继续初始化 DB 结构。调用者传入的路径名指定了数据库文件名的前缀。我们在其后附加后缀 `.idx`，以生成数据库索引文件的名称。

[98–108] 如果调用者要创建数据库文件，我们会使用 `<stdarg.h>` 中的可变参数函数来获取可选的第三个参数。随后使用 `open` 创建并打开索引文件和数据文件。请注意，数据文件名与索引文件名具有相同的前缀，但后缀为 `.dat`。

[109–116] 如果调用者没有指定 `O_CREAT` 标志，则表示要打开现有的数据库文件。在这种情况下，我们只需调用带两个参数的 `open`。

[117–120] 如果打开或创建任一数据库文件时发生错误，我们就调用 `_db_free` 清理 DB 结构，然后向调用者返回 `NULL`。如果一个文件成功打开而另一个失败，`_db_free` 会负责关闭已打开文件的文件描述符，稍后就会看到这一点。

```
121 if ((oflag & (O_CREAT | O_TRUNC)) == (O_CREAT | O_TRUNC)) {
122 /*
123  * 如果创建了数据库，就必须对其进行初始化。
124  * 对整个文件加写锁，以便我们能够原子地执行
125  * stat、检查文件大小和初始化操作。
126 */
127 if (writew_lock(db->idxfd, 0, SEEK_SET, 0) < 0)
128     err_dump("db_open: writew_lock error");
129
130 if (fstat(db->idxfd, &statbuff) < 0)
131     err_sys("db_open: fstat error");
132
133 if (statbuff.st_size == 0) {
134 /*
135  * 我们必须创建一个包含 (NHASH_DEF + 1) 个链
136  * 指针的列表，并将它们的值设为 0。多出的 1 个
137  * 指针是位于哈希表之前的空闲链表指针。
138 */
139 sprintf(asciiptr, "%*d", PTR_SZ, 0);
```

[121–130] 如果正在创建数据库，我们就会遇到加锁操作。设想两个进程几乎同时尝试创建同一个数据库。假设第一个进程调用 `fstat` 后被内核阻塞，而此时 `fstat` 已经返回。第二个进程调用 `db_open`，发现索引文件的长度为 0，于是初始化空闲链表和哈希链。随后，第二个进程向数据库写入一条记录。此时第二个进程被阻塞，而第一个进程从 `fstat` 调用之后继续执行。第一个进程发现索引文件大小为 0（因为 `fstat` 是在第二个进程初始化索引文件之前调用的），于是初始化空闲链表和哈希链，从而抹掉第二个进程存入数据库的记录。要避免这种情况，必须使用锁。我们使用第 14.3 节中的宏 `readw_lock`、`writew_lock` 和 `un_lock`。

[131–137] 如果索引文件的大小为 0，说明我们刚刚创建了它，因此需要初始化其中的空闲链表指针和哈希链指针。请注意，我们使用格式字符串 `%*d` 将数据库指针从整数转换为 ASCII 字符串。（稍后在 `_db_writeidx` 和 `_db_writeptr` 中也会使用这种格式。）该格式会让 `sprintf` 使用参数 `PTR_SZ` 作为下一个参数的最小字段宽度；在此处，下一个参数是 0（由于正在创建新数据库，我们将指针初始化为 0）。这样生成的字符串至少有 `PTR_SZ` 个字符（左侧以空格填充）。在 `_db_writeidx` 和 `_db_writeptr` 中，我们会传入指针值而不是 0，但会先验证指针值不大于 `PTR_MAX`，以确保写入数据库的每个指针字符串恰好占用 `PTR_SZ`（7）个字符。

