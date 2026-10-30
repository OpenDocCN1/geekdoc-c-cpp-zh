```
27   /*
28   * Library's private representation of the database.
29   */
30 typedef struct {
31     int     idxfd;  /* fd for index file */
32     int     datfd;  /* fd for data file */
33     char    *idxbuf; /* malloc'ed buffer for index record */
34     char    *datbuf; /* malloc'ed buffer for data record*/
35     char    *name;   /* name db was opened under */
36     off_t   idxoff;  /* offset in index file of index record */
37                 /* key is at (idxoff + PTR_SZ + IDXLEN_SZ) */
38     size_t  idxlen;  /* length of index record */
39                 /* excludes IDXLEN_SZ bytes at front of record */
40                 /* includes newline at end of index record */
41     off_t   datoff;  /* offset in data file of data record */
42     size_t  datlen;  /* length of data record */
43                 /* includes newline at end */
44     off_t   ptrval;  /* contents of chain ptr in index record */
45     off_t   ptroff;  /* chain ptr offset pointing to this idx record */
46     off_t   chainoff; /* offset of hash chain for this index record */
47     off_t   hashoff;  /* offset in index file of hash table */
48     DBHASH  nhash;    /* current hash table size */
49     COUNT   cnt_delok;   /* delete OK */
50     COUNT   cnt_delerr;  /* delete error */
51     COUNT   cnt_fetchok; /* fetch OK */
52     COUNT   cnt_fetcher; /* fetch error */
53     COUNT   cnt_nextrec; /* nextrec */
54     COUNT   cnt_stor1;   /* store: DB_INSERT, no empty, appended */
55     COUNT   cnt_stor2;   /* store: DB_INSERT, found empty, reused */
56     COUNT   cnt_stor3;   /* store: DB_REPLACE, diff len, appended */
57     COUNT   cnt_stor4;   /* store: DB_REPLACE, same len, overwrote */
58     COUNT   cnt_storerr; /* store error */
59 } DB;
```

[27–48] The DB structure is where we keep all the information for each open database. The DBHANDLE value that is returned by db_open and used by all the other functions is really just a pointer to one of these structures, but we hide that from the callers.

Since we store pointers and lengths as ASCII in the database, we convert these to numeric values and save them in the DB structure. We also save the hash table size even though it is fixed, just in case we decide to enhance the library to allow callers to specify the size when the database is created (see Exercise 20.7).

[49–59] The last ten fields in the DB structure count both successful and unsuccessful operations. If we want to analyze the performance of our database, we can write a function to return these statistics, but for now we only maintain the counters.