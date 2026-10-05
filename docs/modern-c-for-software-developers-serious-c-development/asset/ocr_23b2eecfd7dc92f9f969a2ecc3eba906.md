# Storing Class Objects in a Vector

Any type of object can be stored in a Vector including objects of classes that we create, providing that they have a constructor and implement the comparison operators > and ==.

```
// Store class objects in a vector.
#include <iostream>
#include <vector>
#include <cstdlib>

using namespace std;
class DailyTemperature {
    int temperature;
    public:
        // constructors
        DailyTemperature() { temperature = 0; }
        DailyTemperature(int x) { temperature = x; }
        DailyTemperature& operator=(int x) {
            temperature = x; return *this;
        }

        double get_temperature() { return temperature; }
};
```

bool operator<(DailyTemperature a, DailyTemperature b) {
return a.get_temperature() < b.get_temperature();
}

bool operator==(DailyTemperature a, DailyTemperature b) {
return a.get_temperature() == b.get_temperature();
}

```
int main() {
    vector<DailyTemperature> v;
    Size_t i;
    for(i = 0; i < 7; i++)
        v.push_back(DailyTemperature(60 + rand()%30));

    cout << "Fahrenheit temperatures:\n";
    for ( i = 0; i < v.size(); i++)
        cout << v[i].get_temperature() << " " << "";
    cout << endl;

}
```

// convert from Fahrenheit to Centigrade