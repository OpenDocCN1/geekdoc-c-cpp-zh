308

Chap. 8 File Processing and External Sorting

(e) Get enough memory to decode the buffer pool size.

Write a simulation to analyze this problem.

8.2 Pictures are typically stored as an array, row by row, on disk. Consider the case where the picture has 16 colors. Thus, each pixel can be represented as 4 bits. If you allow 8 bits per pixel, no processing is required to unpack the pixels (because a pixel corresponds to a byte, the lowest level of addressing on most machines). If you pack two pixels per byte, space is saved but the pixels must be unpacked. Which takes more time to read from disk and access every pixel of the image: 8 bits per pixel, or 4 bits per pixel with 2 pixels per byte? Program both and compare the times.

8.3 Implement a disk-based buffer pool class based on the LRU replacement strategy. Disk blocks are marked consecutively from the beginning of the file with the first block numbered as 0. Assume that blocks are 4096 bytes in size, with the first 4 bytes used to store the block ID corresponding to that block. Use the first BufferPool abstract class given in Section 8.3 as the basis for your implementation.

8.4 Implement an external sort based on replacement selection and merging described in this chapter. Test your program both on files with small records and on large records. For which size do you find that sorting would be worthwhile?

8.5 Implement a Quicksort for large files by replacing all array access in the normal Quicksort application with a virtual array implemented using a buffer pool. That is, whenever a record in the array would be read or written by Quicksort, use a call to a buffer pool function instead. Compare the running time of this implementation with implementations for external sorting based on mergesort in this chapter.

8.6 Section suggests that an easy modification to the 2-way merges is to read in a large chunk of data into memory, sort it with Quicksort, and write it out for initial runs. Then, a standard 2-way merge is used in a series of passes to merge the runs. However, this makes use of only two blocks of merging memory at a time. Each block is essentially random access, because the various files are read in an unknown order, even each of the input and output files is processed sequentially. A potential improvement would be, on the merge passes, to divide working memory into four equal sections. One section is allocated to each of the two input files and output files. All reads during merge passes would be in full sections, rather than single blocks. While the total number of blocks read and written would be the same as a regular 2-way Mergesort, it is possible that this speed processing a series of blocks that are logically adjacent in the varying input and output files would be read/written each time. Implement this variation, and compare its running time against