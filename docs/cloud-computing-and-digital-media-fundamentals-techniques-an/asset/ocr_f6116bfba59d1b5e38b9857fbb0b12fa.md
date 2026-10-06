# GPU and Cloud Computing for Music Information Retrieval ■ 89

# 4.3.3 Database Comparison by GPU

We now explain how to employ GPU for efficient comparison in QBSH. At start-up, the long song database is loaded into the global memory. Note that the database is not excessively large since only the pitch and duration are stored for each note of a song. To compress or stretch the input pitch vector, we simply launch $r$ threads for each scaling factor, where $r$ is 31 in our system. We move the scaled vectors back to the main memory and then to the GPUs' constant memory to speed up the access. We have investigated three different schemes for database comparison [5]:

+   1. In scheme 1, we launch $N$ threads to compare $N$ different songs in the database. Recall that there are many notes in a song for comparison, and we have $r$ versions of the input pitch vector, so the computational load of a thread is very heavy (heavy load threads) may not be suitable to run on GPUs.

+   2. In scheme 2, we launch $r$ threads for the comparison of one song. These $r$ threads are grouped into a block, for a total of $N$ blocks. Although the degree of parallelization is higher, the computation time is actually longer because each block contains only a few threads, leading to underutilized SPs.

+   3. In scheme 3, we still have $N$ blocks for $N$ songs, but now each block has $k$ threads. Computation tasks starting at different notes in a song are equally distributed to the $k$ threads. Since $k$ could be much larger than $r$ (e.g., 256 vs. 31), the SPs are more fully utilized in scheme 2. Moreover, since there are multiple threads for one song, we could obtain the minimum distance between the input pitch vector and the song in parallel by using these threads directly.

After obtaining the distance between the query input and each of the songs in the database, we then sort all the distances on the CPU to obtain the top-n list. Sorting using the GPU provided unsatisfactory performance results due to excessive access time requirements over the global memory.

# 4.3.4 Performance Analysis

We used the public corpus MIR-QBSH [6] for our experiments. In this corpus, the beginnings of the corresponding songs serve as the anchor positions for all queries. To test the accuracy of “anchor anywhere,” we duplicated the last fourth of each song in the database and prepended it to the beginning