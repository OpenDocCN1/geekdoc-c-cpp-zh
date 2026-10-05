```
void updateBalance();
/*
 rest of the class Account
 */

/*End of Account.h*/

/*Beginning of Account.cpp*/
#include "Account.h"
float Account::interest_rate=4.5;
void Account::updateBalance()
{
    if (end_of_year)
        balance=balance*interest_rate/100;
}
/*
definitions of the rest of the functions of class Account
 */
/*End of Account.cpp*/
```

The object-to-member access operator can be used to refer to the static data member of a class with respect to an object. The class name with the scope resolution operator can do this directly.

```
f=a1.interest_rate; //a1 is an object of the class Account
Account::interest_rate;
```

There are some static data members can do but non-static data members cannot.

+   A static data member can be of the same type as the class of which it is a member. Listing 2.36.

Listing 2.36 Static data members can be of the same type as their class

```
class A
{
    static A A1; //OK : static
    A *Ptr; //OK : pointer
    A A2; //ERROR!! : non-static
}
```

+   A static data member can appear as the default value for the formal arguments of member functions of its class. See Listing 2.37.

Listing 2.37 A static data member can appear as the default argument in the member functions

```
class A
{
    static int x;
    int y;
public:
    void abc(int=x); //OK
    void def(int=y); //ERROR!! : object required
}
```