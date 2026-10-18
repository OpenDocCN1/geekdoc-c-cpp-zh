19. struct Score
{
    int homeTeam;
    int opponent;
};
Score game[10];

```
//Reads in 5 amounts of money, doubles each amount,
//and outputs the results.
#include <iostream>

<The definitions for the Money class go here.>

int main()
{
    using namespace std;
    Money amount[5];
    int i;
    cout << "Enter 5 amounts of money:\n";
    for (i = 0; i < 5; i++)
        cin >> amount[i];
    for (i = 0; i < 5; i++)
        amount[i] = amount[i] + amount[i];
    cout << "After doubling, the amounts are:\n";
    for (i = 0; i < 5; i++)
        cout << amount[i] << " ";
    cout << endl;
    return 0;
}
```

(You cannot use 2 * amount[i], since * has not been overloaded for operands of type Money.)

21. See answer 22.

22. This answer combines the answers to this and the previous Self-Test Exercise. The class definition would change to the following. (We have deleted some comments from Display 11.10 to save space, but you should include them in your answer.)

```
class TemperatureList
{
public:
    TemperatureList();

    int getSize() const;
    //Returns the number of temperatures on the list.

    void addTemperature(double temperature);

    double getTemperature(int position) const;
```