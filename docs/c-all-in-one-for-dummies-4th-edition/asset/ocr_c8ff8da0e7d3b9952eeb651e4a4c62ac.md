![](bbox=[0.164, 0.094, 0.226, 0.16])

Typically, you want to use this approach when you have a container class that holds multiple instances of another class. For example, you may have a class called `Peripheral`. You may also have a container class called `PeripheralList`, which holds instances of `Peripheral`. You may later derive a new class from `Peripheral`, called `Printer`, and a new class from `PeripheralList`, called `PrinterList`. If `PeripheralList` has a function that returns an instance of `Peripheral`, you would override that function in `PrinterList`. But instead of having it return an instance of `Peripheral`, you would have it return an instance of `Printer`. The Overriding-Derived example, shown in Listing 4-1, shows how to perform this task.

# LISTING 4-1: Overriding and Returning a Derived Class

```
```cpp
#include <iostream>
#include <map>

using namespace std;

class Peripheral {
public:
  string Name;
  int Price;
  int SerialNumber;
  Peripheral(string aname, int aprice, int aserial) :
    Name(aname), Price(aprice),
    SerialNumber(aserial) {}
};

class Printer : public Peripheral {
public:
  enum PrinterType {laser, inkjet};
  PrinterType Type;
  Printer(string aname, PrinterType atype, int aprice,
    int aserial) :
    Peripheral(aname, aprice, aserial), Type(atype) {}
};

typedef map<string, Peripheral *> PeripheralMap;

class PeripheralList {
public:
  PeripheralMap list;
  virtual Peripheral *GetPeripheralByName(string name);
  void AddPeripheral(string name, Peripheral *per);
};
```
```