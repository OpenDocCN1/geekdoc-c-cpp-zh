```
```c
720  /*
721   * Rewind the index file for db_nextrec.
722   * Automatically called by db_open.
723   * Must be called before first db_nextrec.
724   */
725  void
726  db_rewind(DBHANDLE h)
727  {
728      DB        *db = h;
729      off_t      offset;
730      offset = (db->nhash + 1) * PTR_SZ;  /* +1 for free list ptr */
731
732      /*
733       * We’re just setting the file offset for this process
734       * to the start of the index records; no need to lock.
735       * +1 below for newline at end of hash table.
736       */
737      if ((db->idxoff = lseek(db->idxfd, offset, SEEK_SET)) == -1)
738          err_dump("db_rewind: lseek error");
739  }
740
741  /*
742   * Return the next sequential record.
743   * We just step our way through the index file, ignoring deleted
744   * records.  db_rewind must be called before this function is
745   * called the first time.
746   */
747  char *
748  db_nextrec(DBHANDLE h, char *key)
749  {
750      DB        *db = h;
751      char       c;
752      char       *ptr;
```
```

[720–738] The `db_rewind` function is used to reset the database to the “beginning”; we set the file offset for the index file to point to the first record in the index file (immediately following the hash table). (Recall the structure of the index file from Figure 20.2.)

[739–750] The `db_nextrec` function returns the next record in the database. The return value is a pointer to the data buffer. If the caller provides a non-null value for the key parameter, the corresponding key is copied to this address. The caller is responsible for allocating a buffer big enough to store the key. A buffer whose size is `IDXLEN_MAX` bytes is large enough to hold any key.

Records are returned sequentially, in the order that they happen to be stored in the database file. Thus, the records are not sorted by key value. Also, because we do not follow the hash chains, we can come across records that have been deleted, but we will not return these to the caller.