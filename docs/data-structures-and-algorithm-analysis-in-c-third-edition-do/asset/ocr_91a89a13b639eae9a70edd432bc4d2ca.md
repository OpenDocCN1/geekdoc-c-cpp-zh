# 8.6 Further Reading

303

| File Size (Mb) | Sort 1 | Sort 2 Memory size (in blocks) | Sort 3 Memory size (in blocks) |
|---|---|---|---|---|---|---||
| | | 2 | 4 | 16 | 256 | 2 | 4 | 16 |
| 1 | 0.61 | 0.27 | 0.24 | 0.19 | 0.10 | 0.21 | 0.15 | 0.13 |
| | 4,864 | 2,048 | 1,792 | 1,280 | 256 | 2,048 | 1,024 | 512 |
| 4 | 2.56 | 1.30 | 0.96 | 0.61 | 1.15 | 0.68 | 0.66* |
| | 21,504 | 10,320 | 9,216 | 7,072 | 10,320 | 5,120 | 2,048 |
| 16 | 11.28 | 6.12 | 5.47 | 3.36 | 5.42 | 3.19 | 3.10 |
| | 94,208 | 49,152 | 45,056 | 36,834 | 20,480 | 49,152 | 24,516 | 12,288 |
| 256 | 220.39 | 132.47 | 123.68 | 110.01 | 86.66 | 115.73 | 69.31 | 68.71 |
| | 1,769 | 1,048 | 983 | 852K | 589K | 1,049K | 524K | 262K |

**Figure 8.1** comparison of external sorts on a collection of small records for various sizes. Each entry in the table shows time in seconds and total number of blocks read and written by the program. File sizes are in Megabytes. For the third sorting algorithm, on a file size of 4MB, the time and blocks shown in the last column are for a 32-way merge (marked with an asterisk). 32 is used instead of 16 because 32 is a root of the number of blocks in the file (while 16 is not), thus allowing the same number of runs to be merged at every pass.

+   * If possible, use additional disks for overlapping processing with I/O, and to allow for sequential processing

# 8.6 Further Reading

A good general text on file processing is Folk and Zoellick's *File Structures: A Conceptual Toolkit* [FZ98]. A somewhat more advanced discussion on key issues in file processing is Betty Salzberg's *File Structures: An Analytical Approach* [Sal88]. A great discussion on external sorting methods can be found in Salzberg's book.

For disk drive modeling and measurement, see the article by Rueller and Willey, "Introduction to Disk Drive Modeling" [RW94]. See Andrew S. Tanenbaum's *Structured Computer Organization* [Tan06] for introduction to computer hardware and organization. An excellent, detailed description of memory and hard disks can be found online at "The PC Guide," by Charles. Kozok [Koz05] (www.pcguide.com). The PC Guide also gives detailed descriptions of the Microsoft Windows and UNIX (Linux) file systems.

"Outperforming LRU with an Adaptive Replacement Cache Algorithm" by Migiddo and Modha [MM04] for an example of a more sophisticated algorithm than LRU for managing buffer pools.

The following argument comes from Donald Knuth's *Sorting and Searching* [Knu98], which also contains a wide variety of external sorting algorithms.