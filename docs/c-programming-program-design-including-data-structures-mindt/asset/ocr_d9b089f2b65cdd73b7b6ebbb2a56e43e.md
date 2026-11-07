```
```cpp
class candidateListType:
        public unorderedArrayListType<candidateType>
{
public:
        candidateListType(int size = 0);
        //constructor
        void processVotes(string fName, string lName, int region,
                          int votes);
        //Function to update the number of votes for
        //a particular candidate for a particular region.
        //The name of the candidate, the region number, and
        //the number of votes are passed as parameter.
        void addVotes();
        //Function to find the total number of votes
        //received by each candidate.
        void printResult();
        //Function to output the voting data.
};
```
```

Because the class `candidateListType` is derived from the class `unorderedArrayListType`, and list is a protected member of the class `unorderedArrayListType` (inherited from the class `arrayListType`), list can be directly accessed by a member of the class `candidateListType`.

Write the definitions of the member functions of the class `candidateListType`. Rewrite and run your program using the class `candidateListType`.