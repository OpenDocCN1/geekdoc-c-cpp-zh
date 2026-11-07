![](bbox=[0.369, 0.089, 0.914, 0.301])

**Figure 11.6** Classes with both data members and member functions

used. We add one getter and one setter function to each class. We use a more extended UML diagram with another compartment defining the member functions, as shown in Figure 11.6. Based on Figure 11.6, we can see another advantage. The object of the *Student* class must set and get the *identity* value, but the *identity* is already defined in the *Person* class and the *Student* class does not need to set or get it.

# EXAMPLE 11.3

Program 11.1 shows the idea in a simple program. Later we show how to use inheritance to obtain separate compilation.

# **Program 11.1** Public inheritance

```
```cpp
/*****************************************************************
 * The program shows how we can let the class Student inherit    *
 * from the class Person because a student is a person.         *
 *****************************************************************/

#include <iostream>
#include <cassert>
#include <string>
using namespace std;

/*****************************************************************
 * The class definition for the Person class                    *
 *****************************************************************/
class Person
{
private:
    long identity;
public:
    void setId (long identity);
```
```