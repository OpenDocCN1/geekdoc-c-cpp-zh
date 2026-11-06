# Listing 6-5: Using the carparts.cpp File

```
```cpp
#include <iostream>
#include "mediator.h"
#include "carparts.h"

using namespace std;

Mediator::Mediator()
{
    MyEngine = new Engine(this);
    MyElectric = new Electric(this);
    MyRadio = new Radio(this);
    MyWheels = new Wheels(this);
    MyBrakes = new Brakes(this);
    MyHeadlights = new Headlights(this);
    MyAirConditioner = new AirConditioner(this);
    MyRoad = new Road(this);
}

void Mediator::PartChanged(CarPart *part)
{
    if (part == MyEngine)
    {
        if (MyEngine->RPM == 0)
        {
            MyWheels->Speed = 0;
            return;
        }

        if (MyEngine->Revamount == 0)
        {
            return;
        }

        // If engine increases, increase the electric output
        MyElectric->ChangeOutputBy
            (MyEngine->Revamount / 10);

        if (MyEngine->Revamount > 0)
        {
            MyWheels->Accelerate(
                MyEngine->Revamount / 50);
        }
    }
    else if (part == MyElectric)
    {
        // Dim or brighten the headlights
        if (MyHeadlights->Brightness > 0)
            MyHeadlights->Adjust(MyElectric->ChangedBy / 20);

        if (MyRadio->Volume > 0)
            MyRadio->AdjustVolume(MyElectric->ChangedBy / 30);
    }
    else if (part == MyBrakes)
    {
        MyWheels->Decelerate(MyBrakes->Pressure / 5);
    }
}
```
```