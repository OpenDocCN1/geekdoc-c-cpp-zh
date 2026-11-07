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
```

**Sample Run:** After you have written the definitions of the functions of the class candidateType and of the function printResults and then run your program, it should produce the following output. (See Programming Exercise 18.)