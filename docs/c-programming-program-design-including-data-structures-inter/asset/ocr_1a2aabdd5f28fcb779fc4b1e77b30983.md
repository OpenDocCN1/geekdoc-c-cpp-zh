# EXAMPLE 5-25

Consider the following data:

```
101
John Smith
65 78 65 89 25 98 -999
102
Peter Gupta
87 34 89 99 26 78 64 34 -999
103
Buddy Friend
283 99 98 97 26 78 100 63 87 23 -999
104
Doctor Miller
62 35 78 99 12 93 19 -999
...
```

The number -999 at the end of a line acts as a sentinel and therefore is not part of the data.

Assume that this is the data of certain candidates seeking the student council’s presidential seat.

For each candidate, the data is in the following form:

+   ID
+   Name
+   Votes

The objective is to find the total number of votes received by the candidate. We assume that the data is input from the file Exp_5_25.txt of unknown size. We also assume that the input file has been opened using the input file stream variable infile.

Because the input file is of an unspecified length, we use an EOF-controlled while loop. For each candidate, the first data item is the ID of type int and on a line by itself; the second data item is the name, which may consist of more than one word; and the third line contains the votes received from the various departments.

To read the ID, we use the extraction operator >>; to read the name, we use the stream function getline. Notice that after reading the ID, the reading marker is after the ID and the character after the ID is the newline character. Therefore, after reading the ID, the reading marker is after the ID and before the newline character (of the line containing the ID).

The function getline reads until the end of the line. Therefore, if we read the name immediately after reading the ID, then what is stored in the variable name is the newline character (after the ID). It follows that to read the name, we must read and discard the newline character after the ID, which we can accomplish using the stream function get. Therefore, the statements to read the ID and name are as follows:

```
infile >> ID;          //read the ID
infile.get(ch);        //read the newline character after the ID
getline(infile, name); //read the name
```