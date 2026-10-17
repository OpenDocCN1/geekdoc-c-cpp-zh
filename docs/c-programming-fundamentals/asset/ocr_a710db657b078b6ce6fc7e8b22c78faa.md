```
int main()
{
    PublicChild obj1;
    cout << "\nPrivate : adharnumber digit is inaccessible as
              it is not inherited " << endl;
    cout << "\nProtected<->Protected :avg salary is "
         << obj1.pro() << endl;
    cout << "\nPublic<->Public : age is " << obj1.agep << endl;
    cout<< "\n";

    return 0;
}
```

# Output:

Private: adharnumber digit is inaccessible as it is not inherited
Protected<->Protected :avg salary is 43000
Public<->Public : age is 52

# Code Debriefing

+   - As you can see from the code, we have established a relationship between two classes using public inheritance.
+   - The public child class will now be able to inherit and even modify properties from the parent class members, as their access is declared in the base class.
+   - An object of the child class can access all the members except the private ones of the base or parent class.

**2. Private:** If a class is inherited as private, then the access defined for the data members in the base class changes to private in the derived class. That is, all public, protected, and private members have private(inaccessible) ranks.

# Code: Using Private Classes

```
#include <iostream>
using namespace std;
class parentc
{
    public :
        int agep=52;
    protected :
        int avgSal=43000;
```