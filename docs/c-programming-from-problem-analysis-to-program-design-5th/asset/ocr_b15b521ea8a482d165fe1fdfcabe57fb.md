```
```cpp
#include <iostream>
using namespace std;

class clockType
{
public:
    void setTime(int, int, int);
    void getTime(int&, int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;

private:
    int hr;
    int min;
    int sec;
};

int main()
{
    clockType myClock;
    clockType yourClock;

    int hours;
    int minutes;
    int seconds;

    //Set the time of myClock
    myClock.setTime(5, 45, 30);                         //Line 1

    cout << "Line 2: myClock: ";                       //Line 2
    myClock.printTime();  //print the time of myClock   //Line 3
    cout << endl;                                      //Line 4

    cout << "Line 5: yourClock: ";                     //Line 5
    yourClock.printTime(); //print the time of yourClock //Line 6
    cout << endl;                                      //Line 7

    //Set the time of yourClock
    yourClock.setTime(5, 45, 16);                       //Line 8

    cout << "Line 9: After setting, yourClock: ";      //Line 9
    yourClock.printTime(); //print the time of yourClock //Line 10
    cout << endl;                                      //Line 11

    //Compare myClock and yourClock
    if (myClock.equalTime(yourClock))                  //Line 12
        cout << "Line 13: Both times are equal."
             << endl;                                  //Line 13
}
```
```