```
// Merges blocks from one file to another.
// Precondition: inFile is an external file that contains
// numberOfBlocks sorted blocks organized into runs of
// runSize blocks each.
// Postcondition: outFile contains the merged runs of
// inFile. Both files are closed.
// Calls: mergeRuns.
mergeFile(inFile: File, outFile: File,
    runSize: integer, numberOfBlocks: integer)

PrepareFile for input
PrepareOutputFile for output

for (next = 1 to numberOfBlocks with increments of 2 *runSize)
n    // Invariant: Runs in outFile are ordered
    mergeRuns(inFile, outFile, next)
Close inputFile and outFile

// Merges two consecutive runs in a file.
// Precondition: fromFile is an external file of sorted runs
// open for input, toFile is an external file of sorted runs
// open for output, start is the block number of the first
// run on fromFile to be merged, this run contains size
// blocks:
    // Run 1: Block start to start + size - 1
    // Run 2: Block start to start + (2 * size) - 1
// Postcondition: The merged runs fromFile are applied
// toFile. The files remain open.
mergeRuns(fromFile: File, toFile: File,
    start: integer, size: integer)

// Initialize the buffer for runs 1 and 2
in1.readBlock(fromFile, first block of Run 1)
in2.readBlock(fromFile, first block of Run 2)

// Merge until one of run is finished. Whenever an
// input buffer is exhausted, the next block is read.
// Whenever the output buffer is full, it is written.
while (neither run is finished)
    // Invariant: out and each block in toFile are ordered
    Select the smaller "leading edge" of in1 and in2,
    place it in the next position of out
    if (out is full)
        out.writeBlock(toFile, next block of toFile)
    if (in1 is exhausted and blocks remain in Run 1)
        in1.readBlock(fromFile, next block of Run 1)
    if (in2 is exhausted and blocks remain in Run 2)
        in2.readBlock(fromFile, next block of Run 2)

// Assertion: Exactly one of the runs is complete
// Append the remainder of the unfinished input
// buffer to the output buffer and write it
```