The first thing that the program must do is read the candidates’ names into `candidateList`. Therefore, we write a function to accomplish this task. The file `candData.txt` is opened in the function `main`. The names of the input file and `candidateList` are, therefore, passed as parameters to the function `fillNames`. Because the member variable list of the object `candidateList` is protected, it cannot be accessed directly. We, therefore, create an object temp of type `candidateType` to store the candidates’ names and use the function `insertEnd` (of list) to store each candidate’s name in the object `candidateList`. The definition of the function `fillNames` is as follows:

```
```cpp
void fillNames(ifstream& inFile,
               unorderedArrayListType<candidateType>& cList)
{
    string firstN;
    string lastN;
    candidateType temp;

    for (int i = 0; i < NO_OF_CANDIDATES; i++)
    {
        inFile >> firstN >> lastN;
        temp.setName(firstN, lastN);
        cList.insertEnd(temp);
    }
}
```
```

Figure 18-42 shows the object `candidateList` after a call to the function `fillNames`.