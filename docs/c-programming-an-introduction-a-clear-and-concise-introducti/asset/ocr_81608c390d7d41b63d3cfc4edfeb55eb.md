compute the values for these variables, declaring them as double removes
any question about a loss of data. (In fact, if you do declare them as int,
the compiler will issue a warning stating that there may be a loss of data
when assigning a floating-point value to an integer variable).

Next we need to find the total number of valid votes:

```
```cpp
validVotes = totalVotes - (totalVotes * inValidPercent);
```
```

Since the number of invalid votes equals 15 percent of the total
votes, then if we subtract that 15 percent from the total number of votes
we'll get the total number of valid votes. Then we can easily compute the
number of votes the candidate received and display the result:

```
```cpp
candVotes = validVotes * candVotePercent;
cout << "The candidate received " << candVotes
     << " votes.";
```
```

Here is the complete C++ program:

```
```cpp
// votePercent.cpp : main project file.
#include "stdafx.h"
using namespace System;
#include <iostream>
using namespace std;

int main(array<System::String ^> ^args)
{
    const int totalVotes = 500000;
    const double candVotePercent = .60;
    const double inValidPercent = .15;
    double validVotes, candVotes;
    validVotes = totalVotes - (totalVotes *
                 inValidPercent);
    candVotes = validVotes * candVotePercent;
```
```