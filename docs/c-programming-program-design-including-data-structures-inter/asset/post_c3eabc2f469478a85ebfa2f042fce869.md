
```cpp
const candidateType& candidateType::operator=
                              (const candidateType& right)
{
    if (this != &right)    // avoid self-assignment
    {
        firstName = right.firstName;
        lastName = right.lastName;

        for (int i = 0; i < NO_OF_REGIONS; i++)
            votesByRegion[i] = right.votesByRegion[i];

        totalVotes = right.totalVotes;
    }

    return *this;
}

const candidateType& candidateType::operator=
                              (const personType& right)
{
    firstName = right.getFirstName();
    lastName = right.getLastName();

    return *this;
}
```

## MAIN PROGRAM

Now that the class `candidateType` has been designed and implemented, we focus on designing the main program.

Because there are six candidates, we create a list, `candidateList`, containing six components of type `candidateType`. The first thing that the program should do is read each candidate’s name from the file `candData.txt` into the list `candidateList`. Then, we sort `candidateList`.

The next step is to process the voting data from the file `voteData.txt`, which holds the voting data. After processing the voting data, the program should calculate the total votes received by each candidate and print the data, as shown previously. Thus, the general algorithm is:

1. Read each candidate’s name into `candidateList`.
2. Sort `candidateList`.
3. Process the voting data.
4. Calculate the total votes received by each candidate.
5. Print the results.

The following statement creates the object `candidateList`.

```cpp
unorderedArrayListType<candidateType> candidateList(NO_OF_CANDIDATES);
```

Figure 18-40 shows the object `candidateList`. Every component of the array list is an object of type `candidateType`.

### fillNames

The first thing that the program must do is read the candidates’ names into `candidateList`. Therefore, we write a function to accomplish this task. The file `candidate.txt` is opened in the function `main`. The names of the input file and `candidateList` are, therefore, passed as parameters to the function `fillNames`. Because the member variable `list` of the object `candidateList` is protected, it cannot be accessed directly. We, therefore, create an object `temp` of type `candidateType` to store the candidates’ names and use the function `insertEnd` (of list) to store each candidate’s name in the object `candidateList`. The definition of the function `fillNames` follows:

```cpp
void fillNames(ifstream& inFile,
               unorderedArrayListType<candidateType>& cList)
{
    string firstN;
    string lastN;
    int i;
    candidateType temp;

    for (i = 0; i < NO_OF_CANDIDATES; i++)
    {
        inFile >> firstN >> lastN;
        temp.setName(firstN, lastN);
        cList.insertEnd(temp);
    }
}
```

Figure 18-42 shows the object `candidateList` after a call to the function `fillNames`.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1329_0.png)

**FIGURE 18-42** Object `candidateList` after a call to the function `fillNames`

### Sort Names

After reading the candidates’ names, we next sort the array list of the object `candidateList` using any of the (array-based) sorting algorithms discussed in this chapter. Because `candidateList` is an object of type `unorderedArrayListType`, we use the member function `sort` to sort `candidateList`. (For illustration purposes, we use selection sort in the function `sort`. In fact, you can use any array-based sorting algorithm discussed in this chapter.) The following statement accomplishes this task:

```cpp
candidateList.sort();
```

After this statement executes, `candidateList` is as shown in Figure 18-43.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1330_0.png)

**FIGURE 18-43** Object `candidateList` after the statement `candidateList.sort();` executes

### Process Voting Data

Processing the voting data is quite straightforward. Each entry in the file `voteData.txt` is of the form:

```
firstName lastName regionNumber numberOfVotes
```

After reading an entry from the file `voteData.txt`, we locate the row in the array list (of the object `candidateList`) corresponding to the specific candidate and update the entry specified by `regionNumber`.

The component `votesByRegion` is a private member of each component of the array list. Moreover, it is a private member of `candidateList`. The only way we can update the votes of a candidate is to make a copy of that candidate’s record into a temporary object, update the object, and then copy the temporary object back into `list` by replacing the old value with the new value of the temporary object. We can use the member function `retrieveAt` to make a copy of the candidate whose votes need to be updated. After updating the temporary object, we can use the member function `replaceAt` to copy the temporary object back into the list. Suppose the next entry read is:

```
Lisa Fisher 2 35
```

This entry says that Lisa Fisher received 35 votes from region 2. Suppose that before processing this entry, `candidateList` is as shown in Figure 18-44.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1331_0.png)

**FIGURE 18-44** Object `candidateList` before processing entry Lisa Fisher 2 35

We make a copy of the row corresponding to Lisa Fisher (see Figure 18-45).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1331_1.png)

**FIGURE 18-45** Object `temp`

Next, the following statement updates the voting data for region 2. (Here, region = 2 and votes are 35.)

```cpp
temp.updateVotesByRegion(region, votes);
```

After this statement executes, the object `temp` is as shown in Figure 18-46.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1332_0.png)

**FIGURE 18-46** Object `temp` after `temp.updateVotesByRegion(region, votes);` executes

Now we copy the object `temp` into `list` (see Figure 18-47).

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1332_1.png)

**FIGURE 18-47** `candidateList` after copying `temp`

Because the member list of `candidateList` is sorted, we can use the binary search algorithm to find the row position in `list` corresponding to the candidate whose votes need to be updated. Essentially, the definition of the function `processVotes` is:

```cpp
void processVotes(ifstream& inFile,
                  unorderedArrayListType<candidateType> & cList)
{
    string firstN;
    string lastN;
    int region;
    int votes;
    int candLocation;

    candidateType temp;

    inFile >> firstN >> lastN >> region >> votes;

    temp.setName(firstN, lastN);
    temp.setVotes(region, votes);

    while (inFile)
    {
        candLocation = cList.binSearch(temp);

        if (candLocation != -1)
        {
            cList.retrieveAt(candLocation, temp);
            temp.updateVotesByRegion(region, votes);
            cList.replaceAt(candLocation, temp);
        }

        inFile >> firstN >> lastN >> region >> votes;

        temp.setName(firstN, lastN);
        temp.setVotes(region, votes);
    }
}
```

### Add Votes

After processing the voting data, the next step is to find the total votes received by each candidate. This is done by adding the votes received in each region.

Now `votesByRegion` is a private member of `candidateType`, and `list` is a protected member of `candidateList`. Therefore, to add the votes for each candidate, we use the function `retrieveAt` to make a temporary copy of each candidate’s data, add the votes in the temporary object, and then copy the temporary object back into `candidateList`. The following function does this:

```cpp
void addVotes(unorderedArrayListType<candidateType>& cList)
{
    int i;

    candidateType temp;

    for (i = 0; i < NO_OF_CANDIDATES; i++)
    {
        cList.retrieveAt(i, temp);
        temp.calculateTotalVotes();
        cList.replaceAt(i, temp);
    }
}
```

Figure 18-48 shows `candidateList` after adding the votes for each candidate—that is, after a call to the function `addVotes`.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_1334_0.png)

**FIGURE 18-48** `candidateList` after a call to the function `addVotes`

### Print Heading and Print Results

To complete the program, we include a function to print the heading, which outputs the first four lines of the output. The following function accomplishes this task:

```cpp
void printHeading()
{
    cout << "--------------------Election Results--------" << endl;
    cout << "----------" << endl << endl;
    cout << "                 Votes" << endl;
    cout << "   Candidate Name    Region1  Region2  Region3 " << endl;
    cout << "   Region4    Total" << endl;
    cout << "--------- ----------- ----" << endl;
}
```

We now describe the function `printResults`, which prints the results. Suppose that the variable `sumVotes` holds the total votes polled for the election, the variable `largestVotes` holds the largest number of votes received by a candidate, and the variable `minLoc` holds the index of the winning candidate in the array `list`. Further
