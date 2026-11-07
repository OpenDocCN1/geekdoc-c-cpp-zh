
```cpp
void addRegionsVote(int vbRegion[][NO_OF_REGIONS],
                     int tVotes[], int noOfRows)
{
    int i, j;

    for (i = 0; i < noOfRows; i++)
        for (j = 0; j < NO_OF_REGIONS; j++)
            tVotes[i] += vbRegion[i][j];
}
```

We now describe the remaining functions required to get the desired output.

### Function printHeading

This function outputs the first four lines of input, so it contains certain output statements. The definition of this function is:

```cpp
void printHeading()
{
    cout << "-------- -------------Election Results----------" << endl;
    cout << "-----" << endl;
    cout << "Candidate                 Votes" << endl;
    cout << "Name       Region1   Region2   Region3" << endl;
    cout << "Region4    Total" << endl;
    cout << "--------  ------   -------   ------  "
         << "-------  ------" << endl;
}
```

### Function printResults

This function outputs the remaining lines of the output. Clearly, it must have access to each of the three arrays. We must also tell the function the number of rows in each array. (Note that each array has the same number of rows.) Thus, this function has four parameters. Suppose that the parameter cName corresponds to candidatesName, the parameter vbRegion corresponds to votesByRegion, and the parameter tVotes corresponds to totalVotes.

Further suppose that the variable sumVotes holds the total number of votes cast in the election, the variable largestVotes holds the largest number of votes received by a candidate, and the variable winLoc holds the index of the winning candidate in the array candidatesName. The algorithm for this function is:

- a. Initialize sumVotes, largestVotes, and winLoc to 0.
- b. For each row in each array:
  - i. `if (largestVotes < tVotes[i])`
    ```
    {
        largestVotes = tVotes[i];
        winLoc = i;
    }
    ```
  - ii. `sumVotes = sumVotes + tVotes[i];`
  - iii. Output the data from the corresponding rows of each array.
- c. Output the final lines of output.

The definition of this function is:

```cpp
void printResults(string cNames[],
                 int vbRegion[][NO_OF_REGIONS],
                 int tVotes[], int noOfRows)
{
    int i, j;
    int largestVotes = 0;
    int winLoc = 0;
    int sumVotes = 0;

    for (i = 0; i < noOfRows; i++)
    {
        if (largestVotes < tVotes[i])
        {
            largestVotes = tVotes[i];
            winLoc = i;
        }

        sumVotes = sumVotes + tVotes[i];

        cout << left;
        cout << setw(9) << cNames[i] << " ";
        cout << right;
        for (j = 0; j < NO_OF_REGIONS; j++)
            cout << setw(8) << vbRegion[i][j] << " ";
        cout << setw(6) << tVotes[i] << endl;
    }

    cout << endl << endl << "Winner: " << cNames[winLoc]
         << ", Votes Received: " << tVotes[winLoc]
         << endl << endl;
    cout << "Total votes polled: " << sumVotes << endl;
}
```

We now give the main algorithm.

Suppose that the variables in the function main are:

```cpp
string candidatesName[NO_OF_CANDIDATES]; //array to store the
                                           //candidate's name
int votesByRegion[NO_OF_CANDIDATES][NO_OF_REGIONS]; //array to
                                                    //hold the voting data by region
int totalVotes[NO_OF_CANDIDATES]; //array to hold the total votes
                                  //received by each candidate

ifstream infile; //input file variable
```

Furthermore, suppose that the candidates' names are in the file candData.txt, and the voting data is in the file voteData.txt.

## MAIN ALGORITHM:
### FUNCTION main

- 1. Declare the variables.
- 2. Open the input file candData.txt.
- 3. If the input file does not exist, exit the program.
- 4. Read the data from the file candData.txt into the array candidatesName.
- 5. Sort the array candidatesName.
- 6. Close the file candData.txt and clear the input stream.
- 7. Open the input file voteData.txt.
- 8. If the input file does not exist, exit the program.
- 9. Initialize the arrays votesByRegion and totalVotes.
- 10. Process the voting data and store the results in the array votesByRegion.
- 11. Calculate the number of total votes received by each candidate and store the results in the array totalVotes.
- 12. Print the heading.
- 13. Print the results.

## PROGRAM LISTING

```cpp
//****************************************************************
// Author: D. S. Malik
//
// This program processes voting data for student council
// president's post. It outputs each candidate's name and the
// votes they received. The name of the winner is also printed.
//****************************************************************

#include <iostream>
#include <fstream>
#include <string>
#include <iomanip>

using namespace std;

const int NO_OF_CANDIDATES = 6;
const int NO_OF_REGIONS = 4;

void printHeading();
void initialize(int vbRegion[][NO_OF_REGIONS], int tVotes[],
                int noOfRows);

void getCandidatesName(ifstream& inp, string cNames[],
                       int noOfRows);

void sortCandidatesName(string cNames[], int noOfRows);

int binSearch(string cNames[], int noOfRows, string name);

void processVotes(ifstream& inp, string cNames[],
                  int vbRegion[][NO_OF_REGIONS],
                  int noOfRows);

void addRegionsVote(int vbRegion[][NO_OF_REGIONS],
                    int tVotes[], int noOfRows);

void printResults(string cNames[],
                  int vbRegion[][NO_OF_REGIONS],
                  int tVotes[], int noOfRows);

int main()
{
        //Declare variables; Step 1
        string candidatesName[NO_OF_CANDIDATES];
        int votesByRegion[NO_OF_CANDIDATES][NO_OF_REGIONS];
        int totalVotes[NO_OF_CANDIDATES];
        ifstream infile;

        infile.open("candData.txt");                         //Step 2
        if (!infile)                                          //Step 3
        {
                cout << "Input file (candData.txt) does "
                     << "not exist." << endl;
                return 1;
        }

        getCandidatesName(infile, candidatesName,
                          NO_OF_CANDIDATES);                  //Step 4
        sortCandidatesName(candidatesName,
                           NO_OF_CANDIDATES);                 //Step 5

        infile.close();                                       //Step 6
        infile.clear();                                       //Step 6

        infile.open("voteData.txt");                         //Step 7
        if (!infile)                                          //Step 8
        {
                cout << "Input file (voteData.txt) does "
                     << "not exist." << endl;
                return 1;
        }

        initialize(votesByRegion, totalVotes,
                   NO_OF_CANDIDATES);                    //Step 9
        processVotes(infile, candidatesName,
                     votesByRegion, NO_OF_CANDIDATES);   //Step 10
        addRegionsVote(votesByRegion, totalVotes,
                       NO_OF_CANDIDATES);                //Step 11
        printHeading();                                  //Step 12
        printResults(candidatesName,votesByRegion,
                     totalVotes, NO_OF_CANDIDATES);      //Step 13

        return 0;
}

//Place the definitions of the functions initialize,
//getCandidatesName, sortCandidatesName, binSearch,
//processVotes, addRegionsVote, printHeading, and
//printResults here.
```

### Sample Run
(After placing the definitions of all the functions, as described, into the program and executing.)

-------------------Election Results-------------------

**Votes**

| Candidate Name | Region1 | Region2 | Region3 | Region4 | Total |
|---|---|---|---|---|---|
| Ashley | 23 | 89 | 0 | 160 | 272 |
| Danny | 25 | 71 | 89 | 97 | 282 |
| Donald | 110 | 158 | 0 | 0 | 268 |
| Mia | 134 | 112 | 156 | 0 | 402 |
| Mickey | 56 | 63 | 67 | 89 | 275 |
| Peter | 207 | 56 | 0 | 46 | 309 |

Winner: Mia, Votes Received: 402

Total votes polled: 1808

### Input Files

**candData.txt**

- Mia
- Mickey
- Donald
- Peter
- Danny
- Ashley
