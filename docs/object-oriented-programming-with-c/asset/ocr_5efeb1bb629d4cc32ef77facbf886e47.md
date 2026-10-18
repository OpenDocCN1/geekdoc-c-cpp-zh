Program 5.7 illustrates the use of objects as function arguments. It performs the addition of time in the hour and minutes format.

# Program 5.7  Objects as Arguments

```
```cpp
#include <iostream.h>
using namespace std;
class time
{
int hours;
int minutes;
public:
void gettime(int h, int m)
{ hours = h; minutes = m; }
void puttime(void)
{
    cout << hours << “ hours and “;
    cout << minutes << “ minutes “ << “\n”;
}
void sum(time, time);  // declaration with objects as arguments
};
void time :: sum(time t1, time t2) // t1, t2 are objects
{
minutes = t1.minutes + t2.minutes;
hours = minutes/60;
minutes = minutes%60;
hours = hours + t1.hours + t2.hours;
}
int main()
{
time T1, T2, T3;

T1.gettime(2,45);  // get T1
T2.gettime(3,30);  // get T2
```
```