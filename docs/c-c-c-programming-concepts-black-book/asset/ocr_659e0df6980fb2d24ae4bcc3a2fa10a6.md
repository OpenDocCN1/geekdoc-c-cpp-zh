```
```cpp
mapInitiator::~mapInitiator()
{
    //Don't forget to delete the pointer
    delete phonenums;
}

int main()
{
    mapInitiator aClass;
    aClass.createMultiMap();

    //Insert key, value as pairs
    aClass.insertElements(pair<string, int>("SUVANKAR",3839));
    aClass.insertElements(pair<string, int>("PRINON",8483));
    aClass.insertElements(pair<string, int>("ISHAN",8373));
    aClass.insertElements(pair<string, int>("SUVANKAR",8275));
    aClass.insertElements(pair<string, int>("PRINON",9287));
    aClass.insertElements(pair<string, int>("ISHAN",9463));

    aClass.printer();

    return 0;
}
```
```

The output of the preceding program is:

![](bbox=[0.27, 0.44, 0.71, 0.6])

+   5. Implement a C++ program to exemplify the use of multimap.

```
```cpp
#include<iostream>
#include<map>
#include <string>

using namespace std;

//forward declaration
void printer(multimap<string, int> PR);

int main()
{
    multimap<string, int> TEL_NO;
```
```