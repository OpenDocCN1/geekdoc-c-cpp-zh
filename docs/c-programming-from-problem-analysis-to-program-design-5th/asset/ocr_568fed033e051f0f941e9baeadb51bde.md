```
```cpp
if (found)
    return mid;
else
    return -1;
}
```
```

This function processes the voting data. Clearly, it must have access to the arrays `candidatesName` and `votesByRegion`, as well as to the input file, `voteData.txt`. We also need to tell this function the number of rows in each array. Thus, the function `processVotes` has four parameters: one to access the input file `voteData.txt`, one corresponding to the array `candidatesName`, one corresponding to the array `votesByRegion`, and one to pass the number of rows in each array. The definition of this function is:

```
```cpp
void processVotes(ifstream& inp, string cNames[],
                  int vbRegion[][NO_OF_REGIONS],
                  int noOfRows)
{
    string candName;
    int region;
    int noOfVotes;
    int loc;

    inp >> candName >> region >> noOfVotes;

    while (inp)
    {
        loc = binSearch(cNames, noOfRows, candName);

        if (loc != -1)
            vbRegion[loc][region - 1] = vbRegion[loc][region - 1]
                                           + noOfVotes;
        inp >> candName >> region >> noOfVotes;
    }
}
```
```

# Calculate Total Votes (Function addRegionsVote)

After processing the voting data, the next step is to calculate the total votes for each candidate. Suppose that after processing the voting data, the arrays are as shown in Figure 10-27.