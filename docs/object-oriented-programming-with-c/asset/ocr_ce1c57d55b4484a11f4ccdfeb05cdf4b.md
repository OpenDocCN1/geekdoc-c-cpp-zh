Program 10.2 demonstrates the use of >> and getline() for reading the strings.

# Program 10.2 Reading Strings with getline()

```
#include <iostream>
using namespace std;

int main()
{
int size = 20;
char city[20];

cout << "Enter city name: \\n";
cin >> city;
cout << "City name:" << city << "\\n";

cout << "Enter city name again: \\n";
cin.getline(city, size);
cout << "City name now: " << city << "\\n";

cout << "Enter another city name: \\n";
cin.getline(city, size);
cout << "New city name: " << city << "\\n";

return 0;
}
```

The output of Program 10.2 would be:

First run
Enter city name: