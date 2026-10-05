```
p = mp.begin();

// iterate over the map getting keys and values

for (; p != mp.end(); ++p) {
    cout << "key: " << p->first << "\n";
    cout << "value: " << p->second << "\n";
}

```

# Getting A Map Key And A Key Value

Given a map iterator, p points to a pair object {key, value}. p->first points to the key and p->second points to the key value.

The following program creates a telephone book map, mapping names to telephone numbers.

# A Map Container Example

```
#include <iostream>
#include <map>
#include <string>

using namespace std;

int main() {
    map<string, string> tel;

    // insert elements into the map
    tel.insert({"alice smith", "555-555-5555"});
    tel.insert({"john brown", "656-890-9080"});

    map<string, string> iter;

    // given a name, find the tel number
    iter = tel.find("alice smith");

    if(iter != tel.end()) {
        cout << "name: " << iter->first << endl;
        cout << "telephone number is: " << iter->second << endl;
    }

```