# ### Program 11.2 File person.h (Continued)

```
```cpp
private:
    long identity;
public:
    Person ();
    Person (long identity);
    ~Person();
    Person (const Person& person);
    void print () const;
};
#endif
```
```

Program 11.3 shows the implementation file for the *Person* class.

# ### Program 11.3 File person.cpp

```
```cpp
/*************************************************************
 * The implementation file for the Person class            *
 *************************************************************/
#include "person.h"

// Default constructor
Person :: Person ()
: identity (0)
{
}
// Parameter constructor
Person :: Person (long id)
: identity (id)
{
  assert (identity >= 100000000 && identity <= 999999999);
}
// Copy constructor
Person :: Person (const Person& person)
: identity (person.identity)
{
}
// Destructor
Person:: ~Person()
{
}
// Accessor member function
void Person :: print () const
{
  cout << "Identity: " << identity << endl;
}
```
```