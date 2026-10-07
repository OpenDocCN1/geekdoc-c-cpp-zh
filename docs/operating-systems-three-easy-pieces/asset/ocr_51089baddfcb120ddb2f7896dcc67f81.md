# Homework (Simulation)

This section introduces ffs.py, a simple FS simulator you can use to understand better how FFS-based file and directory allocation work. Run See the README for details on how to run the simulator.

# Questions

+   1. Examine the file in.largefile, and then run the simulator with flag -f in.largefile -L 4. What will the resulting allocation look like? Run with -c to check.
2. Now with -L 30, what do you expect to see? Once again, turn on -c to see if you were right. You can also use -s to see exactly which blocks were allocated to the file /
3. Now we compute some statistics about the file. The first thing is we call span, which is the max distance between any two blocks of file or between the index and any data block. Calculate the span of Run ffs.py -f in.largefile -L 4 -c to see what it is. With the -L 100, What difference do you expect in files as the large-file allocation changes from low values to high values?
4. Now let's look at a new input, in.manyfiles. How do you think the FFS policy will lay these files? (you can run with -v to see what files are created, or just cat in.manyfiles). Run the simulator with -c to see if you were right.
5. A metric to evaluate is called dispan. This metric calculates the spread of files within a particular directory, specifically the max distance between the index and data blocks of all files in the directory and the data block of the directory itself. Run with in.manyfiles and -T flag, and calculate the dispan of the three directories. Run with -c to check. How good of a job does this do?
6. Change the size of the index block to 5 (-I). How do you think this will change the layout of the files? Run with -c to see if you were right. Does it affect the dispan?
7. Which group should FFS place a new directory in? The default (simulator) policy looks for groups with the most free inodes. For example, if you run with -A 2, when allocating a new directory, the simulator will show /fs.in-manyfiles -I 5 -A 2 -c to see how allocation changes with this strategy. How does it affect dispan? Why might this be the policy?
8. One last policy we will explore relates to file fragmentation. Run ffs.py -f in.fragmented -v and see if you can predict the files that remain allocated. Run with -c to confirm what you are interested in This is about the data layout of file: / Why is it problematic?
9. A new policy, which we call contiguous allocation (-C), tries to ensure that each file is allocated contiguously. Specifically, with -C n, the file system tries to ensure that each block is free within a group before allocating it. Run ffs.py -f in.fragmented -v -C 2 -c to see the difference. How does layout change as the parameter to -C increases? Finally, how does -C affect lifespan and dispan?