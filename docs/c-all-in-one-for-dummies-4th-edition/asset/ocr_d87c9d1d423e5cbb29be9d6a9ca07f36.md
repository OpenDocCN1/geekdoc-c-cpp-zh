```
```cpp
{
    cout << endl;
    continue;
}
    cout << i * 2 << endl;
}
cout << "All Finished!" << endl;
return 0;
}
```
```

# Nesting loops

Many times, you need to work with more than one loop. For example, you may have several groups of friends, and you want to bilk the individual friends of each group for all you can get. You may host a party for the first group of friends and make them each give you as much money as they have. Then, the next week, you may hold another party with a different group of friends. You would do this for each group of friends. You can draw out the logic like this:

```
```
For each group of friends,
    for each person in that group
        bilk the friend for all he or she is worth
```
```

This is a nested loop. But if you do this, don’t be surprised if this is the last time your friends visit your nest.

A nested loop is simply a loop inside a loop. Suppose that you want to multiply each of the numbers 1 through 10 by 1 and print the answer for each multiplication, and then you want to multiply each of the numbers 1 through 10 by 2 and print the answer for each multiplication, and so on, up to a multiplier of 10. Your C++ code would look like the ForLoop5 example:

```
```cpp
#include <iostream>

using namespace std;

int main()
{
    for (int x = 1; x <= 10; x++)
    {
        cout << "Products of " << x << endl;
        for (int y = 1; y <= 10; y++)
```
```