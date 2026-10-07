# Beginning with a Simple Class

```
using std::string;
// simple base class
class TableTennisPlayer {
private:
    string firstname;
    string lastname;
    bool hasTable;
public:
    TableTennisPlayer(const string& fn = "none",
const string& ln = "none", bool ht = false);
    void Name() const;
    bool hasTable() const { return hasTable; };n    void SetTable(bool v) { hasTable = v; };
};
#endif
```

Listing 13.2 tabtenn0.cpp

```
//tabtenn0.cpp -- simple base-class methods
#include "tabtenn0.h"
#include <iostream>
```

```
TableTennisPlayer::TableTennisPlayer(const string& fn,
const string& ln, bool ht) : firstname(fn),
lastname(ln), hasTable(ht) {}

void TableTennisPlayer::Name() const
{
    std::cout << lastname << " " << firstname;
}
```

All the TableTennis class contains some fields to keep track of the players' names and whether they have tables. There are a couple of points to notice. First, the class uses the standard string class to hold the names. This is more convenient, flexible, and safer than using a character array. And it is rather more professional than the String class of Chapter 12, "Classes and Dynamic Memory Allocation.\ Second, the constructor uses the initializer list syntax introduced in Chapter 12. You could also do this:

```
TableTennisPlayer::TableTennisPlayer(const string& fn,
const string& ln, bool ht)
{
    firstname = fn;
    lastname = ln;
    hasTable = ht;
}
```