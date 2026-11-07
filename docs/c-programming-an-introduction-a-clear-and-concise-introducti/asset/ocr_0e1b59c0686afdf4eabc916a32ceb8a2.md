```
```cpp
<< endl;
Console::ReadKey();
return 0;
}
```
```

Here is the output:

The total amount of change is: $1.67

# Voting Percentages

Here is a problem taken from a junior high mathematics book: In an election, a candidate got 60% of the total valid votes. 15% of the total votes were declared invalid. If the total number of votes is 500,000, find the number of valid votes polled in favor of the candidate.

As usual, the first thing we need to do is decide what our variables are going to be. The facts we know for sure we can enter as constants, so we have three constants:

```
```cpp
const int totalVotes = 500000;
const double candVotePercent = .60;
const double invalidPercent = .15;
```
```

Now we need variables for the total number of valid votes and the number of valid votes the candidate received:

```
```cpp
double validVotes, candVotes;
```
```

It may seem odd to declare these two variables as double, but since we will be working with floating-point values in the expressions used to