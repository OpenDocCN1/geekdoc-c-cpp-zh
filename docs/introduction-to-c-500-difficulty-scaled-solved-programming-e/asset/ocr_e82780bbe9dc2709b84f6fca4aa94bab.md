# 13 • Structures and Unions 383

```
for(ptr = cities; ptr < cities+SIZE; ptr++) { /* When ptr increases
to the next element of the array, that is, to the next structure. */
{
    cout << "\nCity: \";
    getline(cin, ptr->name);

    cout << "\Country: \";
    cin >> ptr->cntr;

    cout << "\Population: \";
    cin >> ptr->pop;
    cin.get();
}

cout << "\nter country to search: \";
getline(cin, cntr);

cout << "\Population: \";
cin >> pop;

found = 0; for(i = 0; i < SIZE; i++) {
    if((cities[i].cntr == cntr) && (cities[i].pop > pop)) {
        found = 1;
        cout << cities[i].name << ' ' << cities[i].pop << '\n';
    }
}
if(found == 0)
    cout << "\nNo city is found\n";
return 0;
}

```

**C.13.3** Define the structure Time with members: hours, minutes, and seconds. Write a function that takes
as parameter a pointer to an integer and converts that to hours, minutes, and seconds. These values should
be stored into the members of the structure of type Time, and the function should return that structure. Write a
program that reads a number of seconds, calls the function, and displays the members of the returned structure.

```
#include <iostream>

struct Time {
    int hours;
    int mins;
    int secs;
};

Time mk_time(const int *ptr);

int main() {
    int secs;
    Time t;

std::cout << "Enter seconds: \";
    std::cin >> secs;

```