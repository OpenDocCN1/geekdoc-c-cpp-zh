# 11.1.2.4 Algorithm

The preceding operations can be organized into the following algorithm:

+   1. Read the name of the input file into *inputFileName*.
+   2. Open an *ifstream* named *inStream* to the file whose name is in *inputFileName*. (If this fails, display an error message and terminate execution.)
+   3. Initialize *count*, *minDay*, *maxDay* and *sum* to 0; *maximum* to the smallest possible (real) value; and *minimum* to the largest possible (real) value. (These initializations for *maximum* and *minimum* ensure that they will be updated to the first reading in 4e and 4f.)
+   4. Loop:
+      a. Read a value for *reading* from *inStream*.
+      b. If the end-of-file mark was read, exit the loop.
+      c. Increment *count*.
+      d. Add *reading* to *sum*.
+      e. If *reading* is less than *minimum* Set *minimum* to *reading* and *minDay* to *count*.
+      f. If *reading* is greater than *maximum* Set *maximum* to *reading* and *maxDay* to *count*.
+      End loop
+   5. Close *inStream*.
+   6. Prompt for and read the name of the output file into *outputFileName*.
+   7. Open an *ofstream* named *outStream* to the file whose name is in *outputFileName*. (If this fails, display an error message and terminate the algorithm.)
+   8. Write *count* to *outStream*.
+   9. If *count* is greater than zero Write *sum/count*, *minimum*, *minDay*, *maximum*, and *maxDay* to *outStream*.
+   10. Close *outStream*.

# 11.1.2.5 Coding

The program in Example 11.1 encodes the preceding algorithm. The file-processing features that it uses will be described in the following sections.