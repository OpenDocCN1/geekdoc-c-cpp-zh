After a call to this function, the arrays to hold the data are shown in Figure 10-21.

![](bbox=[0.164, 0.171, 0.892, 0.39])

FIGURE 10-21 Arrays candidatesName, votesByRegion, and totalVotes after reading candidates' names

Function
sortCandidatesName

This function uses the selection sort algorithm to sort the array candidatesName. This function has two parameters: one corresponding to the array candidatesName and a second to pass the number of rows of the array candidatesName. Essentially, this function is:

```
```cpp
void sortCandidatesName(string cNames[], int noOfRows)
{
    int i, j;
    int min;

    //selection sort
    for (i = 0; i < noOfRows - 1; i++)
    {
        min = i;

        for (j = i + 1; j < noOfRows; j++)
            if (cNames[j] < cNames[min])
                min = j;

        cNames[i].swap(cNames[min]);
    }
}
```
```

After a call to this function, the arrays are shown in Figure 10-22.