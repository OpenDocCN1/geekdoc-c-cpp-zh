# CRASH CONSISTENCY: FSC AND JOURNALING

In systems, metadata journaling (akin to ordered journaling of ext3) is more popular than full data journaling. For example, Windows NTFS and XFS use some form of metadata journaling. Linux ext3 gives you the option of choosing either data, ordered, or unordered modes (in unordered mode, data can be written at any time). All these modes keep metadata consistent; they vary in their semantics for data.

Finally, note that forcing the data write to complete (Step 1) before issuing to the journal (Step 2) is not required for correctness, as indicated in the protocol above. Specifically, it would be fine to concurrently write data, the transaction-begin block, and journaled metadata; the only real requirement is that Steps 1 and 2 complete before the issuing of the journal block (Step 3).

# Tricky Case: Block Reuse

There are some interesting cases that make journaling more tricky, and are thus worth discussing. A number of them revolve block reuse; as Stephen Tweedie (one of the main forces ext3) says

> “What’s the hideous part of the system? It’s deleting files. Everything to do with delete you have nightmares around what happens if block gets deleted and reallocated.” [T00]

The particular example Tweedie gives is as follows. Suppose you are using some form of metadata journaling (and thus data blocks for files are not journaled). Let's say you have a directory called foo. The user adds an entry to foo (say by creating a file), and thus contents of foo (because directories are considered metadata) are written to the log; assume the location of the foo directory data is block 1000. The log contains something like this:

| Journal | TxB | I(foo) | D(foo) | TxE |
|---|---|---|---|---|
| | id=1 | ptr:1000 | final addr:1000 | id=1 |

At this point, the user deletes in the directory and the directory itself, freeing block creates a new file (say bar), which ends up reusing the same block (1000) that used to belong to foo. The inode of bar is committed to disk, as is its data; note, however because metadata journaling is in use, the inode of bar is committed to the journal; the newly-written data in block 1000 in the file is not journaled.

| Journal | TxB | I(foo) | D(foo) | TxE | TxB | I(bar) | TxE |
|---|---|---|---|---|---|---|---|
| | id=1 | ptr:1000 | final addr:1000 | id=1 | id=2 | ptr:1000 | id=2 |

© 2008–19, ARPAC-DUSSEAU

THREE
EASY
PIECES