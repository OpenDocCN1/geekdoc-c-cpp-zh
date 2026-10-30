
```c
262    while (offset != 0) {
263        nextoffset = _db_readidx(db, offset);
264        if (strcmp(db->idxbuf, key) == 0)
265            break;        /* found a match */
266        db->ptroff = offset; /* offset of this (unequal) record */
267        offset = nextoffset; /* next one to compare */
268    }
269    /*
270     * offset == 0 on error (record not found).
271     */
272    return(offset == 0 ? -1 : 0);
273  }

274  /*
275   * Calculate the hash value for a key.
276   */
277  static DBHASH
278  _db_hash(DB *db, const char *key)
279  {
280      DBHASH      hval = 0;
281      char        c;
282      int         i;

283      for (i = 1; (c = *key++) != 0; i++)
284          hval += c * i;    /* ascii char times its 1-based index */
285      return(hval % db->nhash);
286  }
```

**[262–268]** In the while loop, we go through each index record on the hash chain, comparing keys. We call `_db_readidx` to read each index record. It populates the `idxbuf` field with the key of the current record. If `_db_readidx` returns zero, we’ve reached the last entry in the chain.

**[269–273]** If offset is zero after the loop, we’ve reached the end of a hash chain without finding a matching key, so we return −1. Otherwise, we found a match (and exited the loop with the break statement), so we return success (0). In this case, the `ptroff` field contains the address of the previous index record, `datoff` contains the address of the data record, and `datlen` contains the size of the data record. As we make our way through the hash chain, we save the previous index record that points to the current index record. We’ll use this when we delete a record, since we have to modify the chain pointer of the previous record to delete the current record.

**[274–286]** `_db_hash` calculates the hash value for a given key. It multiplies each ASCII character times its 1-based index and divides the result by the number of hash table entries. The remainder from the division is the hash value for this key. Recall that the number of hash table entries is 137, which is a prime number. According to Knuth [1998], prime hashes generally provide good distribution characteristics.

```c
317     /*
318      * Position index file and record the offset.  db_nextrec
319      * calls us with offset==0, meaning read from current offset.
320      * We still need to call lseek to record the current offset.
321      */
322     if ((db->idxoff = lseek(db->idxfd, offset,
323             offset == 0 ? SEEK_CUR : SEEK_SET)) == -1)
324         err_dump("_db_readidx: lseek error");
325
326     /*
327      * Read the ascii chain ptr and the ascii length at
328      * the front of the index record.  This tells us the
329      * remaining size of the index record.
330      */
331     iov[0].iov_base = asciiptr;
332     iov[0].iov_len  = PTR_SZ;
333     iov[1].iov_base = asciilen;
334     iov[1].iov_len  = IDXLEN_SZ;
335     if ((i = readv(db->idxfd, &iov[0], 2)) != PTR_SZ + IDXLEN_SZ) {
336         if (i == 0 && offset == 0)
337             return(-1);       /* EOF for db_nextrec */
338         err_dump("_db_readidx: readv error of index record");
339     }
340
341     /*
342      * This is our return value; always >= 0.
343      */
344     asciiptr[PTR_SZ] = 0;       /* null terminate */
345     db->ptrval = atol(asciiptr); /* offset of next key in chain */
346     asciilen[IDXLEN_SZ] = 0;     /* null terminate */
347     if ((db->idxlen = atoi(asciilen)) < IDXLEN_MIN ||
348         db->idxlen > IDXLEN_MAX)
349         err_dump("_db_readidx: invalid length");
```

**[317–324]** We start by seeking to the index file offset provided by the caller. We record the offset in the DB structure, so even if the caller wants to read the record at the current file offset (by setting offset to 0), we still need to call lseek to determine the current offset. Since an index record will never be stored at offset 0 in the index file, we can safely overload the value of 0 to mean “read from the current offset.”

**[325–338]** We call readv to read the two fixed-length fields at the beginning of the index record: the chain pointer to the next index record and the size of the variable-length index record that follows.

**[339–347]** We convert the offset of the next record to an integer and store it in the ptrval field (this will be used as the return value for this function). Then we convert the length of the index record into an integer and save it in the idxlen field.

```c
348  /*
349   * Now read the actual index record. We read it into the key
350   * buffer that we malloced when we opened the database.
351  */
352  if ((i = read(db->idxfd, db->idxbuf, db->idxlen)) != db->idxlen)
353      err_dump("_db_readidx: read error of index record");
354  if (db->idxbuf[db->idxlen-1] != NEWLINE)  /* sanity check */
355      err_dump("_db_readidx: missing newline");
356  db->idxbuf[db->idxlen-1] = 0;    /* replace newline with null */
357  /*
358   * Find the separators in the index record.
359   */
360  if ((ptr1 = strchr(db->idxbuf, SEP)) == NULL)
361      err_dump("_db_readidx: missing first separator");
362  *ptr1++ = 0;                 /* replace SEP with null */
363  if ((ptr2 = strchr(ptr1, SEP)) == NULL)
364      err_dump("_db_readidx: missing second separator");
365  *ptr2++ = 0;                 /* replace SEP with null */
366  if (strchr(ptr2, SEP) != NULL)
367      err_dump("_db_readidx: too many separators");
368  /*
369   * Get the starting offset and length of the data record.
370   */
371  if ((db->datoff = atol(ptr1)) < 0)
372      err_dump("_db_readidx: starting offset < 0");
373  if ((db->datlen = atol(ptr2)) <= 0 || db->datlen > DATLEN_MAX)
374      err_dump("_db_readidx: invalid length");
375  return(db->prival);     /* return offset of next key in chain */
376 }
```

[348–356] We read the variable-length index record into the idxbuf field in the DB structure. The record should be terminated with a newline, which we replace with a null byte. If the index file is corrupt, we terminate and drop core by calling err_dump.

[357–367] We separate the index record into three fields: the key, the offset of the corresponding data record, and the length of the data record. The strchr function finds the first occurrence of the specified character in the given string. Here we look for the character that separates fields in the record (SEP, which we define to be a colon).

[368–376] We convert the data record offset and length into integers and store them in the DB structure. Then we return the offset of the next record in the hash chain. Note that we do not read the data record; that task is left to the caller. In the db_fetch function, for example, we don't read the data record until _db_find_and_lock has read the index record that matches the key that we're looking for.

```c
377
/*
378     * Read the current data record into the data buffer.
379     * Return a pointer to the null-terminated data buffer.
380     */
381 static char *
382 _db_readdat(DB *db)
383 {
384     if (lseek(db->datfd, db->datoff, SEEK_SET) == -1)
385         err_dump("_db_readdat: lseek error");
386     if (read(db->datfd, db->datbuf, db->datlen) != db->datlen)
387         err_dump("_db_readdat: read error");
388     if (db->datbuf[db->datlen-1] != NEWLINE)   /* sanity check */
389         err_dump("_db_readdat: missing newline");
390     db->datbuf[db->datlen-1] = 0; /* replace newline with null */
391     return(db->datbuf);     /* return pointer to data record */
392 }

/*
394     * Delete the specified record.
395     */
396 int
397 db_delete(DBHANDLE h, const char *key)
398 {
399     DB      *db = h;
400     int     rc = 0;         /* assume record will be found */
401     if (_db_find_and_lock(db, key, 1) == 0) {
402         _db_dodelete(db);
403         db->cnt_delok++;
404     } else {
405         rc = -1;            /* not found */
406         db->cnt_delerr++;
407     }
408     if (un_lock(db->ixfd, db->chainoff, SEEK_SET, 1) < 0)
409         err_dump("db_delete: un_lock error");
410     return(rc);
411 }
```

[377–392] The _db_readdat function populates the datbuf field in the DB structure with the contents of the data record, expecting that the datoff and datlen fields will have been properly initialized already.

[393–411] The db_delete function is used to delete a record given its key. We use _db_find_and_lock to determine whether the record exists in the database. If it does, we call _db_dodelete to do the work needed to delete the record. The third argument to _db_find_and_lock controls whether the chain is read locked or write locked. Here we are requesting a write lock, since we will potentially change the list. Since _db_find_and_lock returns with the lock still held, we need to unlock it, regardless of whether the record was found.
