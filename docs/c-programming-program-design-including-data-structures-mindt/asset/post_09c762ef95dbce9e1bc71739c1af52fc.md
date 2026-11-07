
![](img/b217c421655b51e7494cf3b89bb5432d_1391_0.png)

FIGURE 18-44 Object candidateList before processing entry Lisa Fisher 2 35

We make a copy of the row corresponding to Lisa Fisher (see Figure 18-45).

![](img/b217c421655b51e7494cf3b89bb5432d_1391_1.png)

FIGURE 18-45 Object temp

Next, the following statement updates the voting data for region 2. (Here, region = 2 and votes = 35.)

```cpp
temp.updateVotesByRegion(region, votes);
```

After this statement executes, the object temp is as shown in Figure 18-46.

![](img/b217c421655b51e7494cf3b89bb5432d_1392_0.png)

FIGURE 18-46 Object temp after `temp.updateVotesByRegion(region, votes);` executes

Now we copy the object `temp` into list (see Figure 18-47).

![](img/b217c421655b51e7494cf3b89bb5432d_1392_1.png)

FIGURE 18-47 candidateList after copying temp

Because the member list of candidateList is sorted, we can use the binary search algorithm to find the row position in list corresponding to the candidate whose votes need to be updated. Essentially, the definition of the function processVotes is as follows:

```cpp
void processVotes(ifstream& inFile,
                  unorderedArrayListType<candidateType>& cList)
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

## Add Votes

After processing the voting data, the next step is to find the total votes received by each candidate. This is done by adding the votes received in each region.

Now votesByRegion is a private member of candidateType, and list is a protected member of candidateList. Therefore, to add the votes for each candidate, we use the function retrieveAt to make a temporary copy of each candidate’s data, add the votes in the temporary object, and then copy the temporary object back into candidateList. The following function does this:

```cpp
void addVotes(orderedArrayListType<candidateType> & cList)
{
    candidateType temp;

    for (int i = 0; i < NO_OF_CANDIDATES; i++)
    {
        cList.retrieveAt(i, temp);
        temp.calculateTotalVotes();
        cList.replaceAt(i, temp);
    }
}
```

Figure 18-48 shows candidateList after adding the votes for each candidate—that is, after a call to the function `addVotes`.

![](img/b217c421655b51e7494cf3b89bb5432d_1394_0.png)

FIGURE 18-48 `candidateList` after a call to the function `addVotes`

## Printing Heading and Print Results

To complete the program, we include a function to print the heading, which outputs the first four lines of the output. The following function accomplishes this task:

```cpp
void printHeading()
{
    cout << "        --------------------Election Results-----"
         << "--------------------" << endl << endl;
    cout << "                         Votes" << endl;
    cout << "  Candidate Name   Region1   Region2   Region3"
         << "  Region4   Total" << endl;
    cout << "  --------  --------  -------  -------  -------"
         << "  -------  -------  " << endl;
}
```

We now describe the function `printResults`, which prints the results. Suppose that the variable `sumVotes` holds the total votes polled for the election, the variable `largestVotes` holds the largest number of votes received by a candidate, and the variable `winLoc` holds the index of the winning candidate in the array list. Further suppose that `temp` is an object of type `candidateType`. The algorithm for this function is as follows:

- 1. Initialize `sumVotes`, `largestVotes`, and `winLoc` to zero.
- 2. For each candidate:
  - a. Retrieve the candidate’s data into `temp`.
  - b. Print the candidate’s name and relevant data.
  - c. Retrieve the total votes received by the candidate and update `sumVotes`.
  - d.
    ```cpp
    if (largestVotes < temp.getTotalVotes())
    {
        largestVotes = temp.getTotalVotes();
        winLoc = i;
    }
    ```
- 3. Output the final lines of output.

We leave the definition of the function `printResults` as an exercise. (See Programming Exercise 18 at the end of this chapter.)

## PROGRAM LISTING (MAIN PROGRAM)

```cpp
//******************************************************************
// Author: D.S. Malik
//
// This program processes voting data for student council
// president's post. It outputs each candidate's name and the
// votes he or she received. The name of the winner is also printed.
//******************************************************************
#include <iostream>
#include <string>
#include <fstream>
#include "CandidateType.h"
#include "unorderedArrayListType.h"

using namespace std;

const int NO_OF_CANDIDATES = 6;

void fillNames(ifstream& inFile,
               unorderedArrayListType<candidateType>& cList);
void processVotes(ifstream& inFile,
                  unorderedArrayListType<candidateType>& cList);
void addVotes(unorderedArrayListType<candidateType>& cList);
void printHeading();
void printResults(const unorderedArrayListType<candidateType>& cList);
```

```cpp
int main()
{
    unorderedArrayListType<candidateType>
                         candidateList(NO_OF_CANDIDATES);

    candidateType temp;

    ifstream inFile;

    inFile.open("candData.txt");
    if (!inFile)
    {
        cout << "Input file (candData.txt) does not exist. "
             << "Program terminates!!" << endl;
        return 1;
    }

    fillNames(inFile, candidateList);

    candidateList.sort();

    inFile.close();
    inFile.clear();

    inFile.open("voteData.txt");
    if (!inFile)
    {
        cout << "Input file (voteData.txt) does not exist. "
             << "Program terminates!!" << endl;
        return 1;
    }

    processVotes(inFile, candidateList);

    addVotes(candidateList);

    printHeading();
    printResults(candidateList);

    return 0;
}
//Place the definitions of the functions fillNames, addVotes,
//processVotes, and printHeading here. Also, write and place
//the definition of the function printResults here.
```

**Sample Run:** After you have written the definitions of the functions of the class candidateType and of the function printResults and then run your program, it should produce the following output. (See Programming Exercise 18.)

----------------------Election Results----------------------

Votes

| Candidate Name | Region1 | Region2 | Region3 | Region4 | Total |
| --- | ---: | ---: | ---: | ---: | ---: |
| Sheila Bower | 23 | 70 | 133 | 267 | 493 |
| Danny Dillon | 25 | 71 | 156 | 97 | 349 |
| Lisa Fisher | 110 | 158 | 0 | 0 | 268 |
| Greg Goldy | 75 | 34 | 134 | 0 | 243 |
| Peter Lamba | 285 | 56 | 0 | 46 | 387 |
| Mickey Miller | 112 | 141 | 156 | 67 | 476 |

Winner: Sheila Bower, Votes Received: 493

Total votes polled: 2216

## Input Files

```text
candData.txt

Greg Goldy
Mickey Miller
Lisa Fisher
Peter Lamba
Danny Dillon
Sheila Bower
```

```text
voteData.txt

Greg Goldy 2 34
Mickey Miller 1 56
Lisa Fisher 2 56
Peter Lamba 1 78
Danny Dillon 4 29
Sheila Bower 4 78
Mickey Miller 2 63
Lisa Fisher 1 23
Peter Lamba 2 56
Danny Dillon 1 25
Sheila Bower 2 70
Peter Lamba 4 23
Danny Dillon 4 12
Greg Goldy 3 134
Sheila Bower 4 100
Mickey Miller 3 67
Lisa Fisher 2 67
Danny Dillon 3 67
Sheila Bower 1 23
Mickey Miller 1 56
Lisa Fisher 2 35
Sheila Bower 3 78
Peter Lamba 1 27
Danny Dillon 2 34
```
