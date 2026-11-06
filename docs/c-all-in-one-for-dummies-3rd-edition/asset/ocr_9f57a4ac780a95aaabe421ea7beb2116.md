# Listing 5-1 *(continued)*

```
```cpp
if (full)
{
    out << "High Voltage Radiation: ";
    out << oven.HighVoltageRadiation << endl;
    out << "Radioactive Food Count: ";
    out << oven.RadioactiveFoodCount << endl;
    out << "Leak Level: ";
    out << oven.LeakLevel << endl;
    out << "Oven Name: ";
    out << oven.OvenName;
}
else
{
    out << oven.HighVoltageRadiation << ",";
    out << oven.RadioactiveFoodCount << ",";
    out << oven.LeakLevel << ",";
    out << oven.OvenName;
}
return out;
}

istream &operator >>(istream &in, MicrowaveOven &oven)
{
    in >> oven.HighVoltageRadiation;
    in >> oven.RadioactiveFoodCount;
    in >> oven.LeakLevel;
    return in;
}

struct FullOvenManip {};

void FullOvenInfo(FullOvenManip x) {
typedef void (*FullPtr) (FullOvenManip);
}

ostream & operator << (ostream &out, FullPtr)
{
    MicrowaveOven::Flags[out] = true;
    return out;
}

struct MinOvenManip {};

void MinOvenInfo(MinOvenManip x) {
typedef void (*MinPtr) (MinOvenManip);
}

ostream & operator << (ostream &out, MinPtr)
{
    MicrowaveOven::Flags[out] = false;
    return out;
}

int main()
{
    MicrowaveOven myoven;
    myoven.HighVoltageRadiation = 9832;
    myoven.RadioactiveFoodCount = 7624;
    myoven.LeakLevel = 3793;
    myoven.OvenName = "Burnmaster";
```
```