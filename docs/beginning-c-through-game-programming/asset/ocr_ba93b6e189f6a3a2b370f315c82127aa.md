4. What are the advantages and disadvantages of returning a reference?

5. Should game AI cheat in order to create a more worthy opponent?

# EXERCISES

1. Improve the Mad Lib game from Chapter 5 by using references to make the program more efficient.

2. What’s wrong with the following program?

```
int main()
{
    int score;
    score = 1000;
    float& rScore = score;
    return 0;
}
```

3. What’s wrong with the following function?

```
int& plusThree(int number)
{
    int threeMore = number + 3;
    return threeMore;
}
```