```
obj2.values();
r= obj1*obj2;
r.display();
return 0;
}
```

# Output:

Enter any number
48

Enter any number
122

Your Result is 5856

# Code Debriefing

In this code, we created a class with a few methods.

+   The values() method is used to accept input for data members from the user.

+   Here, the binary operator * used to perform multiplication is overloaded and used with objects.

+   An extra temporary object for our class is created inside the function that stores changed values.

+   This overloading takes one parameter and the values stored in the object get changed.

+   The code now displays the changes made. The overloading was performed successfully.

# Code: Working with Binary Operators

```
#include <iostream>
#include<string.h>
using namespace std;
class concat
{
    char str[20];
    public:
    void input()
    {
```