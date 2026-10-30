```
```c
412  /*
413   * Delete the current record specified by the DB structure.
414   * This function is called by db_store, after
415   * the record has been located by _db_find_and_lock.
416   */
417  static void
418  _db_delete(DB *db)
419  {
420      int     i;
421      char    *ptr;
422      off_t   freeptr, saveptr;
423
424      /*
425       * Set data buffer and key to all blanks.
426       */
427      for (ptr = db->datbuf, i = 0; i < db->datlen - 1; i++)
428          *ptr++ = SPACE;
429      *ptr = 0;   /* null terminate for _db_writedat */
430      ptr = db->idxbuf;
431      while (*ptr)
432          *ptr++ = SPACE;
433
434      /*
435       * We have to lock the free list.
436       */
437      if (writelock(db->idxfd, FREE_OFF, SEEK_SET, 1) < 0)
438          err_dump("_db_delete: write lock error");
439
440      /*
441       * Write the data record with all blanks.
442       */
443      _db_writedat(db, db->datbuf, db->datoff, SEEK_SET);
```
```

**[412–431]** The _db_delete function does all the work necessary to delete a record from the database. (This function is also called by db_store.) Most of the function just updates two linked lists: the free list and the hash chain for this key. When a record is deleted, we set its key and data record to blanks. This fact is used by db_nextrec, which we’ll examine later in this section.

**[432–440]** We call writelock to write lock the free list. This step prevents two processes that are deleting records at the same time, on two different hash chains, from interfering with each other. Since we’ll add the deleted record to the free list, which changes the free-list pointer, only one process at a time can be doing this.

We write the all-blank data record by calling _db_writedat. Note that there is no need for _db_writedat to lock the data file in this case. Since db_delete has write locked the hash chain for this record, we know that no other process is reading or writing this particular data record.