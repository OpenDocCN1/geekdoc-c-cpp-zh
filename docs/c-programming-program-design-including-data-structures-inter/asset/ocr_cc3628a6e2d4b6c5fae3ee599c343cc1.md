```
```cpp
candidateType()
{
    //Default constructor.
    //Postcondition: Candidate's name is initialized to
    //               blanks, the number of votes in each
    //               region, and the total votes are
    //               initialized to 0.

    //Overload the relational operators.
    bool operator==(const candidateType& right) const;
    bool operator!=(const candidateType& right) const;
    bool operator<(const candidateType& right) const;
    bool operator<=(const candidateType& right) const;
    bool operator>(const candidateType& right) const;
    bool operator>=(const candidateType& right) const;

private:
    int votesByRegion[NO_OF_REGIONS];    //array to store the
                                         //votes received in
                                         //each region
    int totalVotes;                      //variable to store the total votes
};
```
```

Figure 18-39 shows the UML diagram of the class candidateType.

![](bbox=[0.171, 0.527, 0.925, 0.889])

**FIGURE 18-39** UML class diagram of class candidateType