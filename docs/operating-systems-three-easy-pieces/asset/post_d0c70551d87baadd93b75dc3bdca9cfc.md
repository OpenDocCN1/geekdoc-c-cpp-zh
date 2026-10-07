
# 542

# LOCALITY AND FAST FILE SYSTEM

unrealistically small numbers), and that the three directories (the root directory /,a, and /b) and four files (/a/c, /a/d, /a/e, /b/f) are placed within them the PFS policies. Assume the regular files are each two blocks in size, and that the directories have just a single block of data. For this figure, we use the obvious symbols for each file or directory (i.e., / for the root directory, a for /a, f for /b/f, and so forth).

| group inodes | data |
| :--- | :--- |
| 0 / | ------/ |
| 1 acde |------accdee---- |
| 2 bf | ------bff------ |
| 3 | ---------------- |
| 4 | ---------------- |
| 5 | ---------------- |
| 6 | ---------------- |
| 7 | ---------------- |

Note that the PFS policy does two positive things: the data blocks of each file are near each file's inode, and files in the same directory are near another (/a/c, /a/d, and /a/e are all in Group 1, and directory /b and its file /b/f are near another in Group 2.

In contrast, let's look now at an inode allocation policy that simply inodes across groups, trying to ensure that no group's inode table fills up quickly. The final allocation might thus look something like this:

| group inodes | data |
| :--- | :--- |
| 0 / | -------------/ |
| 1 a | ------a---- |
| 2 b | ------b---- |
| 3 c | ------cc---- |
| 4 d | ------dd---- |
| 5 e | ------ee---- |
| 6 f | ------ff---- |
| 7 | ---------------- |

As you can see from the figure, while this policy does keep file and (directory) near its respective inode, files within a directory are arbitrarily spread around the directory, and thus name-based locality is not preserved. Access to files /a/c, /a/d, and /a/e now spans three groups instead of one the PFS approach.

The PFS heuristics are based on extensive studies of filesystem traffic or otherwise practically nuanced; rather, they are based on old-fashioned common sense (isn't that CS stands for all?)¹. Files in a directory are often together: imagining a bunch of files and linking them into a single executable. Be-

> Some people refer to common sense as horse sense, especially people who work with horses. However, we have a feeling that this idiom may last as the "mechanized horse", a.k.a. the car, gains in popularity. What will they invent next? A flying machine!!!

OPERATING SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG

# LOCALITY AND THE FAST FILE SYSTEM

![](img/133d518e3f69f4caaead32c569ae6c49_580_0.png)

Figure 41.1: FFS Locality For SEER Traces

cause namespace-based locality exists, FFS will often improve performance, making sure that seeks between related files are nice and short.

# 41.5 Measuring File Locality

To understand whether these heuristics make sense, let's analyze some traces of file system access and see if there is namespace locality. For some reason, there doesn't seem to be a good study of this topic in the literature.

Specifically, we'll use the SEER traces [K94] and analyze how "far away" accesses were from one another in the directory. For example, if file f is opened, and then re-opened in the tree (before any other files are opened), the distance between these two opens in the directory tree is zero (as they are the same). If a file f in directory (i.e., dir/f) is opened, by an open of file g in the same directory (i.e., dir/g), the distance between the two accesses is one, as they share the same directory but are not the same. Our distance metric measures how far up the tree you have to travel to find the common ancestor of two files; the closer they are in the tree, the lower metric.

Figure 41.1 shows the locality observed in the SEER traces over all workstations in the SEER cluster over the entirety of it. The graph plots the difference metric along the x-axis, and shows the cumulative percentage of file opens that were of that difference along the y-axis. Specifically, for the SEER traces marked ("Trace" in the graph), you can see that about 7% of file accesses were to the file that was opened premiously, and that nearly 40% of file accesses were either the same file or to one in the same directory (i.e., a difference of zero or one). Thus, the FFS locality assumption seems to make sense (at least for traces).

Interestingly, another 25% or so of file accesses were to files that had a distance of two. This type of locality occurs fashion when the user has structured a set of related directories in a multi-level fashion and constantly joins them. For example, if a user has a src directory and builds object files (.o files) within an obj directory, and both of these directories are sub-directories of a main directory, a common pattern will be proj/src/foo.c followed by proj/obj/foo.o. The distance between these two accesses is two, as proj is the common ancestor. FFS does not capture this type of locality in its policies, and thus more seeking will occur between accesses.

For comparison, the graph shows locality for a “Random” trace. The graph plots the difference metric along the x-axis, and shows the cumulative percentage of file opens that were of that difference along the y-axis. Specifically, for the SEER traces marked ("Trace" in the graph), you can see that about 7% of file accesses were to the file that was opened premiously, and that nearly 40% of file accesses were either the same file or to one in the same directory (i.e., a difference of zero or one). Thus, the FFS locality assumption seems to make sense (at least for traces).

# LOCALITY AND THE FAST FILE SYSTEM

# 544

# LOCALITY AND THE FAST FILE SYSTEM

As you can see from the figure, while this policy does keep file and (directory) near its respective inode, files within a directory are arbitrarily spread around the directory, and thus name-based locality is not preserved. Access to files /a/c, /a/d, and /a/e now spans three groups instead of one the PFS approach.

The PFS heuristics are based on extensive studies of filesystem traffic or otherwise practically nuanced; rather, they are based on old-fashioned common sense (isn't that CS stands for all?)¹. Files in a directory are often together: imagining a bunch of files and linking them into a single executable. Be-

> Some people refer to common sense as horse sense, especially people who work with horses. However, we have a feeling that this idiom may last as the "mechanized horse", a.k.a. the car, gains in popularity. What will they invent next? A flying machine!!!

OPERATING SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG

![](img/133d518e3f69f4caaead32c569ae6c49_580_0.png)

Figure 41.1: FFS Locality For SEER Traces

cause namespace-based locality exists, FFS will often improve performance, making sure that seeks between related files are nice and short.

# 41.5 Measuring File Locality

To understand whether these heuristics make sense, let's analyze some traces of file system access and see if there is namespace locality. For some reason, there doesn't seem to be a good study of this topic in the literature.

Specifically, we'll use the SEER traces [K94] and analyze how "far away" accesses were from one another in the directory. For example, if file f is opened, and then re-opened in the tree (before any other files are opened), the distance between these two opens in the directory tree is zero (as they are the same). If a file f in directory (i.e., dir/f) is opened, by an open of file g in the same directory (i.e., dir/g), the distance between the two accesses is one, as they share the same directory but are not the same. Our distance metric measures how far up the tree you have to travel to find the common ancestor of two files; the closer they are in the tree, the lower metric.

Figure 41.1 shows the locality observed in the SEER traces over all workstations in the SEER cluster over the entirety of it. The graph plots the difference metric along the x-axis, and shows the cumulative percentage of file opens that were of that difference along the y-axis. Specifically, for the SEER traces marked ("Trace" in the graph), you can see that about 7% of file accesses were to the file that was opened premiously, and that nearly 40% of file accesses were either the same file or to one in the same directory (i.e., a difference of zero or one). Thus, the FFS locality assumption seems to make sense (at least for traces).

Interestingly, another 25% or so of file accesses were to files that had a distance of two. This type of locality occurs fashion when the user has structured a set of related directories in a multi-level fashion and constantly joins them. For example, if a user has a src directory and builds object files (.o files) within an obj directory, and both of these directories are sub-directories of a main directory, a common pattern will be proj/src/foo.c followed by proj/obj/foo.o. The distance between these two accesses is two, as proj is the common ancestor. FFS does not capture this type of locality in its policies, and thus more seeking will occur between accesses.

For comparison, the graph shows locality for a “Random” trace. The graph plots the difference metric along the x-axis, and shows the cumulative percentage of file opens that were of that difference along the y-axis. Specifically, for the SEER traces marked ("Trace" in the graph), you can see that about 7% of file accesses were to the file that was opened premiously, and that nearly 40% of file accesses were either the same file or to one in the same directory (i.e., a difference of zero or one). Thus, the FFS locality assumption seems to make sense (at least for traces).

# 4.6 Large-File Exception

In order to achieve high performance, the system must minimize the number of seeks. The most effective way to do this is to increase the amount of data transferred with each seek. This is achieved by using larger chunks. If a file is large, it can be broken into several chunks, and each chunk can be placed in a different group. However, if the chunks are too small, the system will have to perform many seeks to read the file. If the chunks are too large, the system may run out of space in a group and be forced to place the remaining file elsewhere. The goal is to find an optimal chunk size that is small enough to fit in many groups, but large enough to maximize the transfer-to-seek ratio.

Let's do an example: assume that the average positioning time (i.e. seek and rotation) for a disk is 10 ms. Assume that the disk transfers at 40 MB/s. If your goal is to spend half your time seeking and achieve 50% of performance, then you would need to spend 10 ms transferring data. The question becomes: how big a chunk have to be in order to spend 10 ms in transfer? Easy just our old file method, in particular the dimensional analysis mentioned in the chapter on disks [AD14]:

| $40\text{ MB}$ | $1024\text{ KB}$ | $1\text{ sec}$ | | $409.6\text{ KB}$ | (41.1) |
|---|---|---|---|---|---|
| $\text{sec}$ | $1\text{ MB}$ | $1000\text{ pe}$ | | |

Basically what this says is: if you transfer at 40 MB/s, you need to transfer 409.6 KB every time you seek in order to spend your your seeking and half your transferring. Similarly, you can compute the size of the chunk you need to achieve 90% of peak bandwidth (turns out it is about 3.6MB), or even 99% of peak bandwidth (40.6MB!). As you can see, the closer you want to get to, the bigger these chunks get (see Figure 41.2 for a plot of these values).

FFS does not use this type of calculation to spread large files across groups, however. Instead, it took a simple approach, based on the
