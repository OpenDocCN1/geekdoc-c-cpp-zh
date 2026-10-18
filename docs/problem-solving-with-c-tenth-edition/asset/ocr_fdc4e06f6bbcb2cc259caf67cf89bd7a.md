# DISPLAY 11.10 Program for a Class with an Array Member (part 1 of 2)

```
//This is a definition for the class
//TemperatureList. Values of this type are lists of Fahrenheit temperatures.

#include <iostream>
#include <cstdlib>
using namespace std;

const int MAX_LIST_SIZE = 50;

class TemperatureList
{
public:
    TemperatureList();
    //Initializes the object to an empty list.

    void addTemperature(double temperature);
    //Precondition: The list is not full.
    //Postcondition: The temperature has been added to the list.

    bool full() const;
    //Returns true if the list is full; false otherwise.

    friend ostream& operator<<(ostream& outs,
        const TemperatureList& theObject);
    //Overloads the << operator so it can be used to output values of
    //type TemperatureList. Temperatures are output one per line.
    //Precondition: If outs is a file output stream, then outs
    //has already been connected to a file.
private:
    double list[MAX_LIST_SIZE]; //of temperatures in Fahrenheit
    int size; //number of array positions filled
};

//This is the implementation for the class TemperatureList.

TemperatureList::TemperatureList() : size(0)
{
    //Body intentionally empty.
}
void TemperatureList::addTemperature(double temperature)
{//Uses iostream and cstdlib:
    if ( full() )
    {
        cout << "Error: adding to a full list.\n";
        exit(1);
    }

```