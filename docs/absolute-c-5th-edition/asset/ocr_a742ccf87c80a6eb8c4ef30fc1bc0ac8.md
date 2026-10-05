# 888 CHAPTER 19 Standard Template Library

Display 19.14 Program Using the map Template Class (part 1 of 2)

```
//Program to demonstrate use of the map template class.
#include <iostream>
#include <map>
#include <string>
using std::cout;
using std::endl;
using std::map;
using std::string;

int main() {
    map<string, string> planets;

planets["Mercury"] = "Hot planet";
planets["Venus"] = "Atmosphere of sulfuric acid";
planets["Earth"] = "Home";
planets["Mars"] = "The Red Planet";
planets["Jupiter"] = "Largest planet in our solar system";
planets["Saturn"] = "Has rings";
planets["Uranus"] = "Tilts on its side";
planets["Neptune"] = "1500 mile-per-hour winds";
planets["Pluto"] = "Dwarf planet";

cout << "Entry for Mercury - " << planets["Mercury"] << endl;

if (planets.find("Mercury") != planets.end())
    cout << "Mercury is in the map." << endl;

if (planets.find("Ceres") == planets.end())
    cout << "Ceres is not in the map." << endl;

cout << "Iterating through all planets: " << endl;
for (auto *iter = planets.begin(); iter != planets.end(); iter++) {
    cout << iter->first << " : " << iter->second << endl;
}
return 0;
}
```

> The iterator will output the map sorted by the key. In this case, output will be listed alphabetically by planet.

Sample Dialogue

Entry for Mercury - Hot planet
Mercury is in the map.
Ceres is not in the map.