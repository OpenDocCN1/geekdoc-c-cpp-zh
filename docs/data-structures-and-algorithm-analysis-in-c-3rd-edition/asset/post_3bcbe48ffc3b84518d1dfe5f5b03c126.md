
| File Size (Mb) | Measure | Sort 1 | Sort 2 (2 blocks) | Sort 2 (4 blocks) | Sort 2 (16 blocks) | Sort 2 (256 blocks) | Sort 3 (2 blocks) | Sort 3 (4 blocks) | Sort 3 (16 blocks) |
|---|---|---|---|---|---|---|---|---|---|
| 1 | Time (sec) | 0.61 | 0.27 | 0.24 | 0.19 | 0.10 | 0.21 | 0.15 | 0.13 |
| 1 | Blocks | 4,864 | 2,048 | 1,792 | 1,280 | 256 | 2,048 | 1,024 | 512 |
| 4 | Time (sec) | 2.56 | 1.30 | 1.19 | 0.96 | 0.61 | 1.15 | 0.68 | 0.66* |
| 4 | Blocks | 21,504 | 10,240 | 9,216 | 7,168 | 3,072 | 10,240 | 5,120 | 2,048 |
| 16 | Time (sec) | 11.28 | 6.12 | 5.63 | 4.78 | 3.36 | 5.42 | 3.19 | 3.10 |
| 16 | Blocks | 94,208 | 49,152 | 45,056 | 36,864 | 20,480 | 49,152 | 24,516 | 12,288 |
| 256 | Time (sec) | 220.39 | 132.47 | 123.68 | 110.01 | 86.66 | 115.73 | 69.31 | 68.71 |
| 256 | Blocks | 1,769K | 1,048K | 983K | 852K | 589K | 1,049K | 524K | 262K |

Figure 8.11 A comparison of three external sorts on a collection of small records for files of various sizes. Each entry in the table shows time in seconds and total number of blocks read and written by the program. File sizes are in Megabytes. For the third sorting algorithm, on a file size of 4MB, the time and blocks shown in the last column are for a 32-way merge (marked with an asterisk). 32 is used instead of 16 because 32 is a root of the number of blocks in the file (while 16 is not), thus allowing the same number of runs to be merged at every pass.

- If possible, use additional disk drives for more overlapping of processing with I/O, and to allow for sequential file processing.

A good general text on file processing is Folk and Zoellick's File Structures: A Conceptual Toolkit [FZ98]. A somewhat more advanced discussion on key issues in file processing is Betty Salzberg's File Structures: An Analytical Approach [Sal88]. A great discussion on external sorting methods can be found in Salzberg's book. The presentation in this chapter is in the spirit of Salzberg's.

For details on disk drive modeling and measurement, see the article by Ruemmler and Wilkes, "An Introduction to Disk Drive Modeling," [RW94]. See Andrew S. Tanenbaum’s Structured Computer Organization [Tan06] for an introduction to computer hardware and organization. An excellent, detailed description of memory and hard disk drives can be found online at "The PC Guide," by Charles M. Kozierok [Koz05] (www.pcguide.com). The PC Guide also gives detailed descriptions of the Microsoft Windows and UNIX (Linux) file systems.

See "Outperforming LRU with an Adaptive Replacement Cache Algorithm" by Megiddo and Modha [MM04] for an example of a more sophisticated algorithm than LRU for managing buffer pools.

The snowplow argument comes from Donald E. Knuth’s Sorting and Searching [Knu98], which also contains a wide variety of external sorting algorithms.

## 8.7 Exercises

- 8.1 Computer memory and storage prices change rapidly. Find out what the current prices are for the media listed in Figure 8.1. Does your information change any of the basic conclusions regarding disk processing?

- 8.2 Assume a disk drive from the late 1990s is configured as follows. The total storage is approximately 675MB divided among 15 surfaces. Each surface has 612 tracks; there are 144 sectors/track, 512 bytes/sector, and 8 sectors/cluster. The disk turns at 3600 rpm. The track-to-track seek time is 20 ms, and the average seek time is 80 ms. Now assume that there is a 360KB file on the disk. On average, how long does it take to read all of the data in the file? Assume that the first track of the file is randomly placed on the disk, that the entire file lies on adjacent tracks, and that the file completely fills each track on which it is found. A seek must be performed each time the I/O head moves to a new track. Show your calculations.

- 8.3 Using the specifications for the disk drive given in Exercise 8.2, calculate the expected time to read one entire track, one sector, and one byte. Show your calculations.

- 8.4 Using the disk drive specifications given in Exercise 8.2, calculate the time required to read a 10MB file assuming
  - (a) The file is stored on a series of contiguous tracks, as few tracks as possible.
  - (b) The file is spread randomly across the disk in 4KB clusters.
  Show your calculations.

- 8.5 Assume that a disk drive is configured as follows. The total storage is approximately 1033MB divided among 15 surfaces. Each surface has 2100 tracks, there are 64 sectors/track, 512 bytes/sector, and 8 sectors/cluster. The disk turns at 7200 rpm. The track-to-track seek time is 3 ms, and the average seek time is 20 ms. Now assume that there is a 512KB file on the disk. On average, how long does it take to read all of the data on the file? Assume that the first track of the file is randomly placed on the disk, that the entire file lies on contiguous tracks, and that the file completely fills each track on which it is found. Show your calculations.

- 8.6 Using the specifications for the disk drive given in Exercise 8.5, calculate the expected time to read one entire track, one sector, and one byte. Show your calculations.

- 8.8 A typical disk drive from 2004 has the following specifications.³ The total storage is approximately 120GB on 6 platter surfaces or 20GB/platter. Each platter has 16K tracks with 2560 sectors/track (a sector holds 512 bytes) and 16 sectors/cluster. The disk turns at 7200 rpm. The track-to-track seek time is 2.0 ms, and the average seek time is 10.0 ms. Now assume that there is a 6MB file on the disk. On average, how long does it take to read all of the data on the file? Assume that the first track of the file is randomly placed on the disk, that the entire file lies on contiguous tracks, and that the file completely fills each track on which it is found. Show your calculations.

> ³To make the exercise doable, this specification is completely fictitious with respect to the track and sector layout. While sectors do have 512 bytes, and while the number of platters and amount of data per track is plausible, the reality is that all modern drives use a zoned organization to keep the data density from inside to outside of the disk reasonably high. The rest of the numbers are typical for a drive from 2004.

- 8.9 Using the specifications for the disk drive given in Exercise 8.8, calculate the expected time to read one entire track, one sector, and one byte. Show your calculations.

- 8.10 Using the disk drive specifications given in Exercise 8.8, calculate the time required to read a 10MB file assuming
  - (a) The file is stored on a series of contiguous tracks, as few tracks as possible.
  - (b) The file is spread randomly across the disk in 8KB clusters.
  Show your calculations.

- 8.11 At the end of 2004, the fastest disk drive I could find specifications for was the Maxtor Atlas. This drive had a nominal capacity of 73.4GB using 4 platters (8 surfaces) or 9.175GB/surface. Assume there are 16,384 tracks with an average of 1170 sectors/track and 512 bytes/sector.⁴ The disk turns at 15,000 rpm. The track-to-track seek time is 0.4 ms and the average seek time is 3.6 ms. How long will it take on average to read a 6MB file, assuming that the first track of the file is randomly placed on the disk, that the entire file lies on contiguous tracks, and that the file completely fills each track on which it is found. Show your calculations.

> ⁴Again, this track layout does not account for the zoned arrangement on modern disk drives.

- 8.12 Using the specifications for the disk drive given in Exercise 8.11, calculate the expected time to read one entire track, one sector, and one byte. Show your calculations.

- 8.13 Using the disk drive specifications given in Exercise 8.11, calculate the time required to read a 10MB file assuming
  - (a) The file is stored on a series of contiguous tracks, as few tracks as possible.
  - (b) The file is spread randomly across the disk in 8KB clusters. Show your calculations.

- 8.14 Prove that two tracks selected at random from a disk are separated on average by one third the number of tracks on the disk.

- 8.15 Assume that a file contains one million records sorted by key value. A query to the file returns a single record containing the requested key value. Files are stored on disk in sectors each containing 100 records. Assume that the average time to read a sector selected at random is 10.0 ms. In contrast, it takes only 2.0 ms to read the sector adjacent to the current position of the I/O head. The "batch" algorithm for processing queries is to first sort the queries by order of appearance in the file, and then read the entire file sequentially, processing all queries in sequential order as the file is read. This algorithm implies that the queries must all be available before processing begins. The "interactive" algorithm is to process each query in order of its arrival, searching for the requested sector each time (unless by chance two queries in a row are to the same sector). Carefully define under what conditions the batch method is more efficient than the interactive method.

- 8.16 Assume that a virtual memory is managed using a buffer pool. The buffer pool contains five buffers and each buffer stores one block of data. Memory accesses are by block ID. Assume the following series of memory accesses takes place:

  5 2 5 12 3 6 5 9 3 2 4 1 5 9 8 15 3 7 2 5 9 10 4 6 8 5

  For each of the following buffer pool replacement strategies, show the contents of the buffer pool at the end of the series, and indicate how many times a block was found in the buffer pool (instead of being read into memory). Assume that the buffer pool is initially empty.

  - (a) First-in, first out.
  - (b) Least frequently used (with counts kept only for blocks currently in memory, counts for a page are lost when that page is removed, and the oldest item with the smallest count is removed when there is a tie).
  - (c) Least frequently used (with counts kept for all blocks, and the oldest item with the smallest count is removed when there is a tie).
  - (d) Least recently used.
  - (e) Most recently used (replace the block that was most recently accessed).

- 8.17 Suppose that a record is 32 bytes, a block is 1024 bytes (thus, there are 32 records per block), and that working memory is 1MB (there is also additional space available for I/O buffers, program variables, etc.). What is the expected size for the largest file that can be merged using replacement selection followed by a single pass of multiway merge? Explain how you got your answer.
